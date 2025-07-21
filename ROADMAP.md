# Roadmap for CES2 Platform

The CES2 (Community Exchange System 2) platform aspires to become the leading open-source platform for community exchange systems. The team has documented the requirements in this repository's [issue tracker](https://github.com/community-exchange-network/ces2/issues). High-priority issues are part of the MVP (Minimum Viable Product). The MVP is a significant project, with the first stage being MVP v0.

## MVP v0

This roadmap outlines the steps for version zero of the Minimum Viable Product for the CES2 platform. The goal is to connect the [Komunitin](https://docs.komunitin.org/) app to the existing CES database, enabling CES users to access their accounts via the existing CES (desktop and mobile) frontends, or the new app.

The focus is on minimal development to support local transactions and browsing local offers and wants using the CES database. Critical features like inter-exchange interactions, admin tools, advanced transaction features, and search/filtering are excluded at this stage.

After MVP v0, development will iterate to add features until the full MVP is ready for the CES community.

### 1. Authentication Service Development

**Goal**: Develop a backend web service for user authentication and access token management, validating credentials from CES or an integrated database.

* Build an HTTP web service using TypeScript and [Express.js](http://Express.js).
* Evaluate [node-oidc-provider](https://github.com/panva/node-oidc-provider) for:
  * OAuth2 provider with credentials and refresh flows.
  * JWT access tokens.
  * JWKS endpoint.
* Forgot password and change email features.
* Have a test CES DB with synthetic or anonymized data.
* Create a database abstraction layer.
* Implement the data layer with Prisma ORM and a PostgreSQL container.
* Develop a second data layer version using the test CES DB.
* Write tests for both data layers.
* Set up a CI/CD pipeline for testing and deploying a staging version.
* Provide OpenAPI documentation.

### 2. Minimal Social Service Development

**Goal**: Develop a minimal backend web service for member profiles, offers, wants, and categories.

* Build an HTTP web service using TypeScript and [Express.js](http://Express.js).
* Add an authentication layer using `express-oauth2-jwt-bearer` or similar.
* Implement the [Social API](https://petstore.swagger.io/?url=https://raw.githubusercontent.com/komunitin/komunitin-api/refs/heads/master/social/openapi.yaml) endpoints.
* Create a database abstraction layer.
* Implement the data layer with Prisma ORM and a PostgreSQL container.
* Develop a second data layer version using the test CES DB.
* Write tests for both data layers.
* Provide OpenAPI documentation.

### 3. Accounting Service Integration

**Goal**: Adapt the Komunitin accounting service to the CES DB.

* Refactor the Ledger interface for CES DB compatibility.
* Implement a CES DB version of the Ledger interface.
* Write unit tests for the CES Ledger layer.
* Run server tests with the CES Ledger.

### 4. Notifications Service Integration

**Goal**: Adapt the notifications service to the CES mailing provider.

* Integrate the CES AWS mailer provider.
* Check the authorization mechanism.

### 5. Production Deployment

**Goal**: Deploy a public-facing system connected to the production CES database, enabling users to access the new app.

* Create a continuous deployment (CD) pipeline for the CES-flavored system.
