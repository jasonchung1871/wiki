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

[Click here to download chefs_build.zip](https://api.media.atlassian.com/file/dce82925-cfbd-4bac-8b22-b245dd188d2e/binary?client=5b2c3105-a87a-4395-a5fc-204b3ef786d8&collection=contentId-962166785&dl=true&max-age=2592000&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiI1YjJjMzEwNS1hODdhLTQzOTUtYTVmYy0yMDRiM2VmNzg2ZDgiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpjb2xsZWN0aW9uOmNvbnRlbnRJZC05NjIxNjY3ODUiOlsicmVhZCJdfSwiZXhwIjoxNjY3MjM2MzA4LCJuYmYiOjE2NjcyMzM0Mjh9.ddNwfWeUNfWXHAzJInEowpNqAAfZRhYCP3aFuDoxCmo)

[Click here to download local.json](https://api.media.atlassian.com/file/9f568054-0ec6-43c6-a88f-53d8c74036fa/binary?client=5b2c3105-a87a-4395-a5fc-204b3ef786d8&collection=contentId-962166785&dl=true&max-age=2592000&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiI1YjJjMzEwNS1hODdhLTQzOTUtYTVmYy0yMDRiM2VmNzg2ZDgiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpjb2xsZWN0aW9uOmNvbnRlbnRJZC05NjIxNjY3ODUiOlsicmVhZCJdfSwiZXhwIjoxNjY3MjM2MzA4LCJuYmYiOjE2NjcyMzM0Mjh9.ddNwfWeUNfWXHAzJInEowpNqAAfZRhYCP3aFuDoxCmo)

[Or download the files from our Confluence page](https://bcdevex.atlassian.net/wiki/spaces/CCP/pages/962166785/Local+CHEFS+Instance+Setup)

All the files are now configured and you can run Keycloak and PostgreSQL.

Note that `realm-export.json` is configured with the SSO integration for the “Development” environment, and will only work with the **resource** and **secret** from the Development JSON.

***

# Build

1. Start Docker, open a terminal in the `/chefs_build` directory, and run the following command:

```bash
docker compose up
```
This will start up an instance for your Keycloak and PostgreSQL containers. If you don’t want to keep the terminal open, you can append a `-d` to the end of the command above.

2. Next, open a terminal in the directory `/common-hosted-form-service/app` and run the following commands:
```bash
npm install
npm run migrate
npm run seed:run
npm run serve
```
This will start the process for the CHEFS API.

3. Open another terminal in the directory /common-hosted-form-service/app/frontend and run the following commands:
```bash
npm install
npm run serve
```
This will start the process for the CHEFS front end.

***

View the [additional resources](https://bcdevex.atlassian.net/wiki/spaces/CCP/pages/1002012675) page for troubleshooting common errors.