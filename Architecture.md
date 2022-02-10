**On this page:**

- [Infrastructure](#infrastructure)
- [Database Structure](#database-structure)
- [Code Design](#code-design)

## Infrastructure

The Common Hosted Form Service (CHEFS) is designed to be a cloud-native containerized microservice. CHEFS is intended to be operated within a Kubernetes/OpenShift container ecosystem, where it can scale based on incoming load and demand. The following diagram provides a general overview of how the three main components relate to one another, and how network traffic generally flows between the components.

![CHEFS Architecture](images/chefs_infra_architecture.png)  
**Figure 1 - The general infrastructure and network topology of CHEFS**

### High Availability

The CHEFS API and database are all designed to be highly available within the OpenShift environment. The Database achieves this by leveraging [Patroni](https://patroni.readthedocs.io/en/latest/). On the OCP4 platform, depending on  load, there can be between 2 to 16 running replicas. These replicas allow the service to handle a large variety of request volumes and scale resources to meet demand.

### Network Connectivity

In general, all network traffic follows the standard OpenShift Route to Service pattern. When a client connects to the CHEFS API, they will be going through OpenShift's router and load balancer. The router and load balancer forward that connection to one of the CHEFS API pod replicas. Figure 1 shows the general network traffic direction using the outlined fat arrows. The direction of those arrows represents which component is initializing the TCP/IP connection.

Since this service depends on persistent database connections, we have them configured to leverage a network pool. The network pool allows the service to avoid making a TCP/IP-3way handshake on every new connection. Instead, the service can leverage existing pipeline traffic and improve general efficiency. We pool connections from CHEFS to Patroni within our architecture. The OpenShift 4 Route and load balancer follow the general default scheduling behaviour as defined by Kubernetes.

## Database Structure

The Postgres database is written and handled via managed, code-first migrations as specified in the repository. We generally store tables regarding users, forms, submissions, and how they relate to each other. Since CHEFS itself is relatively agnostic to form technology used in the frontend, we went with an explicit black-box approach to storing form schemas and submission content Although we use form.io for form rendering and management, CHEFS can support arbitrary schemas and formats as well.

The key is how CHEFS stores form content: form and submission data are treated as a single, black-box payload for most intents and purposes. The Postgres database stores form content in JSONB columns because they offer reverse indexing and searching support. This method allows us to do simple JSON structured searches for data to a certain degree. JSONB is also generally better than JSON fields in Postgres because it handles whitespaces and other edge cases more cleanly.

## Code Design

While CHEFS itself is a compact microservice with a focused approach to handling and managing forms, not all design choices are self-evident just from inspecting the codebase. The following section will cover some of our major coding decisions. 

### Pooling

We introduced network pooling for Patroni connections because as our traffic volume increased, creating, and destroying network connections for each transaction was time-consuming and costly. While low volumes of traffic can operate without any apparent delay to the user, we started encountering issues scaling up and improving total transaction flow within CHEFS.

By reusing connections whenever possible, we were able to avoid the TCP/IP 3-way handshake that must be done on every new connection and instead leverage existing connections to pipeline traffic and improve general efficiency. While this doesn't seem significant, when we switched to pooling in our testing, we observed up to an almost 3x performance increase in total transaction volume flow.

### Horizontal Autoscaling

To make sure our application could scale horizontally, we had to ensure that all processes in the application were self-contained and atomic. Since we do not have any guarantees of which pod instance would be handling what task at any specific moment. We can only ensure that every unit of work is defined and atomic to prevent situations where there is deadlock or double executions.

While implementing Horizontal Autoscaling is relatively simple by using a [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) construct in OpenShift. We can only take advantage of it if the application can handle the different lifecycles. Based on usage metrics such as CPU and memory load, the HPA can increase or decrease the number of replicas on the platform to meet the demand.

We found that we could scale up to around 17 pods in our testing before we began to crash out our Patroni database. We haven't been able to isolate the cause of this issue. We suspect that the underlying Postgres database can only handle up to 100 concurrent connections (and is thus ignoring Patroni's max connection limit of 500). It might also be that the database containers are simply running out of memory before they can handle more connections. This limitation is why we decided to cap our HPA to a maximum of 16 pods at this time.

Our current limiting factor for scaling higher is the ability of our database to support more connections for some reason or another. Suppose we get into the situation where we need to scale past 16 pods. In that case, we will need to consider more managed solutions for pooling dB connections such as [PgBouncer](https://www.pgbouncer.org/).
