# Ísland.is

[This repository](https://github.com/island-is/island.is) is the center of development for digital government services on `island.is`. It is managed by the [Digital Iceland](https://stafraent.island.is/) department inside the [Ministry of Finance and Economic Affairs](https://www.government.is/ministries/ministry-of-finance-and-economic-affairs/).

These solutions are [FOSS](https://en.wikipedia.org/wiki/Free_and_open-source_software) and open to contributions, but most development is performed by teams that win tenders to develop new functionality for Digital Iceland.

## How to contribute

We are working on documentation and workflows to help external developers understand and run these solutions locally.

For now, we appreciate assistance with security reviews (more eyes = better), documentation and smaller fixes.

### Reading material

For more information about the big picture of the whole project make sure to read the [technical overview](../technical-overview/README.md).

You can also read up on our development stack and preferred tools:

#### General

| Tool                                          | Description                         |
| --------------------------------------------- | ----------------------------------- |
| [NodeJS](https://nodejs.org/en/)              | scripts and server-side framework   |
| [TypeScript](https://www.typescriptlang.org/) | programming language                |
| [NX](https://nx.dev/react)                    | monorepo tools and code scaffolding |

#### Frontend

| Tool                                                          | Description                                                |
| ------------------------------------------------------------- | ---------------------------------------------------------- |
| [React](https://reactjs.org/)                                 | UI framework                                               |
| [NextJS](https://nextjs.org/)                                 | front-end framework with routing and server side rendering |
| [Treat](https://seek-oss.github.io/treat/)                    | css-in-js                                                  |
| [Storybook](https://storybook.js.org/)                        | develop and document React components in isolation         |
| [Apollo Client](https://www.apollographql.com/docs/react/)    | graphql client                                             |
| [GraphQL Code Generator](https://graphql-code-generator.com/) | generate GraphQL clients and types                         |
| [Cypress](https://www.cypress.io/)                            | automated browser testing tool                             |
| [MirageJS](https://miragejs.com/)                             | API mocking for webapps                                    |

#### Backend

| Tool                                                 | Description                                 |
| ---------------------------------------------------- | ------------------------------------------- |
| [NestJS](https://nestjs.com/)                        | server-side framework for NodeJS            |
| [Sequelize](https://sequelize.org/)                  | database object relational mapper           |
| [OpenAPI Generator](https://openapi-generator.tech/) | generate clients and types for OpenAPI APIs |

#### Code Quality

| Tool                             | Description            |
| -------------------------------- | ---------------------- |
| [Jest](https://jestjs.io/)       | automated testing tool |
| [ESLint](https://eslint.org/)    | code checker           |
| [Prettier](https://prettier.io/) | code formatter         |

#### Protocols and specifications

| Tool                                           | Description                            |
| ---------------------------------------------- | -------------------------------------- |
| [GraphQL](https://graphql.org/)                | api protocol for our frontend projects |
| [OpenAPI](https://www.openapis.org/)           | specification to describe rest apis    |
| [Open ID Connect](https://openid.net/connect/) | authentication protocols               |

#### Repositories

| Tool                                      | Description                        |
| ----------------------------------------- | ---------------------------------- |
| [PostgreSQL](https://www.postgresql.org/) | SQL database                       |
| [Contentful](https://www.contentful.com/) | headless content management system |

#### Infrastructure

| Tool                                 | Description                                                          |
| ------------------------------------ | -------------------------------------------------------------------- |
| [Docker](https://www.docker.com/)    | virtual machine containers for continuous integration and deployment |
| [Kubernetes](https://kubernetes.io/) | host docker containers in production                                 |
| [Helm](https://helm.sh/)             | kubernetes deployment configuration                                  |

## Repository structure

The repository is a [monorepo](../technical-overview/monorepo.md) that has multiple apps (something that can be built and run) and libraries (which other apps and libraries can depend on).

Our system architecture generally includes frontend projects, a graphql API gateway, and service APIs. Many of these projects are in early development.

Featured projects:

- [Island.is website](./apps/web)
- [Application system](./apps/application-system)
- [Service Portal](./apps/service-portal)
- [Shared GraphQL API](./apps/api)
- [Island UI design system](./libs/island-ui)

Other projects:

- [Digital Judicial System](./apps/judicial-system)
- [Travel Gift](./apps/gjafakort)
- [Air Discount Scheme](./apps/air-discount-scheme)
- [COVID Activities](./apps/adgerdir)
