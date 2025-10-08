# Road map for CES2 Platform

This is the roadmap for the CES2 platform, which aims to be the leading open-source platform for community exchange systems. The team has documented the requirements in this repository's [issue tracker](https://github.com/community-exchange-network/ces2/issues). The roadmap has been structured in several stages. Each stage is a milestone defined in the [milestone tracker](https://github.com/community-exchange-network/ces2/milestones).

## Stages

 - [**v0-mvp: UX and UI**](https://github.com/community-exchange-network/ces2/milestone/2): The second stage defines the basis for the app design and user experience including app layout and navigation, styling (colors, fonts, etc), help, terminology, internationalization. Placing the UX stage at the beginning of the roadmap allows for a more user-centered design process.
 - [**v1-mvp: Integration**](https://github.com/community-exchange-network/ces2/milestone/1): The first stage focuses on integrating the Komunitin to the existing CES database. At the end of this stage we should have a test instance of the Komunitin app connected to a database with the schema of the CES database.
 - [**v2-mvp: User features**](https://github.com/community-exchange-network/ces2/milestone/3): The goal of this stage is to have all essential user features, including sign up, profile management, offers and wants management, account management, basic search.
 - [**v3-mvp: Admin features**](https://github.com/community-exchange-network/ces2/milestone/4): This stage focuses on the essential admin features such as user management and exchange settings. At the end of this stage we will have the CES2 MVP, with all essential features for users and administrators but still missing some important features.
 - [**v4: Federation**](https://github.com/community-exchange-network/ces2/milestone/5): This stage develops the features required for a user to interact with other exchanges, meaning being able to browse offers and wants from other exchanges, and to make transactions with them. Additionally, this stage should include the APIs for third-party apps to interact with the CES2 platform.
 - [**v5: More features**](https://github.com/community-exchange-network/ces2/milestone/6): This stage includes all user features that were not included in the MVP, such as fees, demurrage, additional communication features, announcements, mailing.
 - [**v6: Migration**](https://github.com/community-exchange-network/ces2/milestone/7): This stage focuses on migrating existing CES users to the new platform. At the end of this stage we should be able to discontinue the old CES platform without losing any significant features or data.
 - [**v7: Search**](https://github.com/community-exchange-network/ces2/milestone/8): This stage focuses on implementing a search engine for the CES2 platform allowing both semantic full-text search and geographic search. This stage also includes recommendation features.

## v0-mvp: UX and UI

This roadmap outlines the goals and deliverables for the first milestone of the CES2 platform MVP, focused on establishing the visual identity, usability, and core navigation for the application. The objective is to build a strong user experience foundation and ensure user engagement from the start, and also have an early tangible prototype to further discuss the UX with the whole team.

At this stage, the app will be visually cohesive and user-friendly, but we will have only the features already provided by the existing system and it won't be connected to the main CES database.

### 1. App Layout and Navigation

**Goal**: Design and implement the fundamental navigation structure for the CES2 app, ensuring seamless usability on both mobile and large screens.

* Create a bottom navigation bar optimized for mobile devices.
* Implement a top app bar with profile and settings buttons.
* Add a navbar suitable for large screens.

### 2. New home page and page refactoring

**Goal**: Create a new home page having a mix of both offers and needs with basic filtering and searching capabilities.

* Build the new combined feed for home page.
* Create the new home page
* Add filtering features to home page
* Refactor the Transactions page.
* Refactor the Members page.

### 3. Deployment

**Goal**: Establish a deployment pipeline for the CES app flavour to support rapid iteration and user feedback.

* Modernize the build pipeline to use Vite bundler
* Develop a mechanism to compile multiple app flavours based on build-time environment variables, with different styles, assets, texts and feature flags.
* Have a CES flavour and a Komunitin flavour.
* Contuinuously deploy the CES flavour into a public staging server.

### 4. Visual Identity and Theming

**Goal**: Establish a consistent visual language for the application.

* Validate the existing CES style guide.
* Apply the CES style guide including colors, typography and general style.
* Allow for Local Group branding customization.

### 5. Terminology and Languages

**Goal**: Have a coherent and philosophically aligned terminology.

* Build a glossary of main terms and metaphors, as discussed with the rest of the team.
* Have two corpus of texts: one following "record activities" metaphor and another following the "send tokens" metaphor. The first one will be the default in the CES flavoured app and the second willm be the defauilt in Komunitin' flavour.
* Translate the new texts to existing languages.
* Add new languages: Dutch & Japanese.

### 6. Help and Feedback

**Goal**: Have contextual help and enable end users to provide feedback.

* Add in-app help features and help pages for end users.
* Integrate a mechanism for end user feedback.
---

This milestone creates the essential look-and-feel, navigation, and support infrastructure for the CES2 app, laying the foundation for subsequent development stages.

## v1-mvp: Integration

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
