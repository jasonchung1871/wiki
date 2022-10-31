This page has an intended audience of developers and other technical team members looking to install CHEFS on their local machines for testing and development. Following this documentation will set up an isolated sandbox CHEFS instance for investigation and research prior to preparing pull requests or code commits.

***

# Prerequisites

1. An IDIR account is required to access CHEFS. 
2. Request an SSO Integration from the [Common Hosted Single Sign-on (CSS)](https://bcgov.github.io/sso-requests) page in order to obtain a **resource** and **secret** that will be used for authentication when building CHEFS. View the [detailed documentation](https://github.com/wiki/spaces/CCP/pages/961675282) about requesting the Pathfinder SSO integration. 
3. Ensure that [Docker](https://www.docker.com/get-started/) is installed on your local machine. Using Docker allows for a quick CHEFS build on your local machine however this is not how the production environment is hosted.

***

# Setup

1. Start by cloning the [CHEFS source code](https://github.com/bcgov/common-hosted-form-service) onto your local machine and download the `local.json` file below such that the directory structure follows `/common-hosted-form-service/app/config/local.json` 
2. Download `chefs_build.zip` which contains directory structure and docker file for building CHEFS.
3. Open `realm-export.json`  located at `chefs_build/docker/imports/keycloak` and search for `XXXXXXXXXXXX`. This value must match the `clientSecret` value in `local.json`  so that the CHEFS API can connect to your Keycloak instance. By default, these are set to be equal and don’t need to be altered.
4. Navigate to the [CSS](https://bcgov.github.io/sso-requests) page, login with your IDIR, and download the ‘Development’ Installation JSON from your SSO Integration. 
5. Back in the `realm-export.json` file, search for `YYYYYYYYYYYY` and replace it with the **resource** you obtained from the downloaded JSON file. Search for `ZZZZZZZZZZZZ` and replace it with the **secret**.

