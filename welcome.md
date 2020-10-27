# Welcome

Hi there, you are probably new to the project. Here you can find a quick overview of what you can expect and what is expected from you as a contributor.

## General info

[island.is](https://github.com/island-is/island.is) is open-source software. The license is MIT.
The project is a [monorepo](monorepo.md) which means the code for all custom-written services is stored in there.

## Technology

The codebase is all [TypeScript](https://www.typescriptlang.org) and [NodeJS](https://nodejs.org/en/). For more info please see the [Technical Direction](technical-direction.md).

The tool we use to manage the monorepo structure is called [NX](https://nx.dev). We have one set of NodeJS modules used by all code and any changes in there affect potentially multiple services.

For the backend we use [NestJS](https://nestjs.com). Use the pre-packaged setup that we have and you will save us all some time.

For the frontend we use [React](https://reactjs.org) or [NextJS](https://nextjs.org).

For testing we use [Jest](https://jestjs.io).

For database access we use [Sequalize](https://sequelize.org).

You can find the latest and greatest in how we setup a backend in our [reference-backend](https://github.com/island-is/island.is/blob/master/apps/reference-backend)

Applications are composed of services that are [packaged in Docker containers](#dockerizing) and then deployed in a Kubernetes cluster using Helm. You will hardly need to know about this if you follow the path everyone else in the organization is walking.

[All our environments are hosted in AWS.](devops/environment-setup.md)

## Practices

To contribute you need to follow the standard [GitHub Pull Request(PR)](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) workflow. When you open a PR, your code will be run through the [CI process](docs/adr/0002-continuous-integration.md) automatically. Ask for a [code-review](code-reviews.md) and when you get an approval, merge to master. Rinse and repeat.

When a code change gets on `master`, that will create Docker containers for all services and everything will get deployed to `Dev` env. For more info please see the [Continuous Delivery process](devops/continuous-delivery.md).

We expect contributors to deliver the following:

- the business logic
- the tests
- documentation
- [logs](devops/logging.md)
- [metrics](devops/metrics.md)

## Starting a new project/application

If you are adding a new application, please follow the instructions in the [monorepo README](https://github.com/island-is/island.is/blob/master/README.md).

## Dockerizing

You simply need to add an NX target to your service to enable creating a Docker image for it. For more info see [dockerizing](devops/dockerizing.md).

## Kubernetes

We have a Helm chart template that should fit most services. You pretty much only need to add your ingress (optional), environment variables(optional) and secrets(optional) and your service can get deployed to Dev. For more info, please see [Helm charts](https://github.com/island-is/helm).
For a read-only view of the Kubernetes cluster and the services running there head over to

- [Dev](https://kubenav.dev01.devland.is)
- [Staging](https://kubenav.staging01.devland.is)
