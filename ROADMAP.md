# Road map for CES2 Platform

This is the roadmap for the CES2 platform, which aims to be the leading open-source platform for community exchange systems. The team has documented the requirements in this repository's [issue tracker](https://github.com/community-exchange-network/ces2/issues). The roadmap has been structured in several stages. Each stage is a milestone defined in the [milestone tracker](https://github.com/community-exchange-network/ces2/milestones).

 - [**v0-mvp: Integration**](https://github.com/community-exchange-network/ces2/milestone/1): The first stage focuses on integrating the Komunitin to the existing CES database. At the end of this stage we should have a test instance of the Komunitin app connected to a database with the schema of the CES database.
 - [**v1-mvp: UX and UI**](https://github.com/community-exchange-network/ces2/milestone/2): The second stage defines the basis for the app design and user experience including app layout and navigation, styling (colors, fonts, etc), help, terminology, internationalization. Placing the UX stage at the beginning of the roadmap allows for a more user-centered design process.
 - [**v2-mvp: User features**](https://github.com/community-exchange-network/ces2/milestone/3): The goal of this stage is to have all essential user features, including sign up, profile management, offers and wants management, account management, basic search.
 - [**v3-mvp: Admin features**](https://github.com/community-exchange-network/ces2/milestone/4): This stage focuses on the essential admin features such as user management and exchange settings. At the end of this stage we will have the CES2 MVP, with all essential features for users and administrators but still missing some important features.
 - [**v4: Federation**](https://github.com/community-exchange-network/ces2/milestone/5): This stage develops the features required for a user to interact with other exchanges, meaning being able to browse offers and wants from other exchanges, and to make transactions with them. Additionally, this stage should include the APIs for third-party apps to interact with the CES2 platform.
 - [**v5: More features**](https://github.com/community-exchange-network/ces2/milestone/6): This stage includes all user features that were not included in the MVP, such as fees, demurrage, additional communication features, announcements, mailing.
 - [**v6: Migration**](https://github.com/community-exchange-network/ces2/milestone/7): This stage focuses on migrating existing CES users to the new platform. At the end of this stage we should be able to discontinue the old CES platform without losing any significant features or data.
 - [**v7: Search**](https://github.com/community-exchange-network/ces2/milestone/8): This stage focuses on implementing a search engine for the CES2 platform allowing both semantic full-text search and geographic search. This stage also includes recommendation features.

## v0-mvp: Integration

This road map outlines the steps for version zero of the Minimum Viable Product for the CES2 platform. The goal is to connect the [Komunitin](https://docs.komunitin.org/) app to the existing CES database, enabling CES users to access their accounts via the existing CES (desktop and mobile) frontends, or the new app.

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
