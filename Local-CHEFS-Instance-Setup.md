This document will help developers looking to install CHEFS on their local machines for testing and development. Following this documentation will set up an isolated sandbox CHEFS instance for investigation and research prior to preparing pull requests or code commits. 


# Prerequisites

An IDIR account is required to access CHEFS. 

Request an SSO Integration from the [Common Hosted Single Sign-on (CSS)](https://bcgov.github.io/sso-requests) page in order to obtain a resource and secret that will be used for authentication when building CHEFS. View the [detailed documentation](https://github.com/bcgov/common-hosted-form-service/wiki/Pathfinder-SSO-client) about requesting the Pathfinder SSO integration. 

Ensure that [Docker](https://www.docker.com/get-started/) is installed on your local machine. Using Docker allows for a quick CHEFS build on your local machine however this is not how the production environment is hosted. 

# Setup

Start by cloning the [CHEFS source code](https://github.com/bcgov/common-hosted-form-service) onto your local machine and download `build_package.zip` linked below.

[build_package.zip](https://github.com/bcgov/common-hosted-form-service/files/9973552/build_package.zip)

Unzip the file and move the `local.json` file such that the CHEFS directory structure follows `/common-hosted-form-service/app/config/local.json` .The `chefs_build` directory contains the directory structure and docker file for building CHEFS.

Open `realm-export.json`  located at `chefs_build/docker/imports/keycloak` and search for `XXXXXXXXXXXX`. This value must match the `clientSecret` value in `local.json` so that the CHEFS API can connect to your Keycloak instance. By default, these are set to be equal and don’t need to be altered.

Navigate to the [CSS](https://bcgov.github.io/sso-requests) page, log in with your IDIR, and download the ‘Development’ Installation JSON from your SSO Integration. 

Back in the `realm-export.json` file, search for `YYYYYYYYYYYY` and replace it with the resource you obtained from the downloaded JSON file. Search for `ZZZZZZZZZZZZ` and replace it with the secret. 

All the files are now configured and you can run Keycloak and PostgreSQL. 

Note that realm-export.json is configured with the SSO integration for the “Development” environment, and will only work with the resource and secret from the Development JSON. 

# Build
Start Docker, open a terminal in the `/chefs_build` directory, and run the following command:

    docker compose up

This will start up an instance for your Keycloak and PostgreSQL containers. If you don’t want to keep the terminal open, you can append a -d to the end of the command above.

Next, open a terminal in the directory `/common-hosted-form-service/app` and run the following commands:

    npm install
    npm run migrate
    npm run seed:run
    npm run serve

This will start the process for the CHEFS API.

Open another terminal in the directory `/common-hosted-form-service/app/frontend` and run the following commands:

    npm install
    npm run serve

This will start the process for the CHEFS front end.
