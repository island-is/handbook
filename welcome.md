# Welcome

Hi there, you are probably new to the project. Here you can find a quick overview of what you can expect and what is expected from you as a contributor.

## General info

[island.is](https://github.com/island-is/island.is) is open-source software. The license is MIT.
The project is a [monorepo](monorepo.md) which means the code for all custom-written services is stored in there.

## Technology

The codebase is all TypeScript and NodeJS. For more info please see the [Technical Direction](technical-direction.md)

The tool we use to manage the monorepo structure is called [NX](https://nx.dev).

For the backend we use NestJS. Use the pre-packaged setup that we have.
For the frontend we use React or NextJS.
For testing we use Jest.
For database access we use [Sequalize](https://sequelize.org).

You can find the latest and greatest in how we setup a backend in our [reference-backend](https://github.com/island-is/island.is/blob/master/apps/reference-backend)

Applications are composed of services that are packaged in Docker containers and then deployed in a Kubernetes cluster using Helm. You will hardly need to know about this if you follow the path everyone else in the organization is walking.

## Practices

To contribute you need to follow the standard GitHub Pull Request(PR) workflow. When you open a PR, your code will be run through the CI process automatically. Ask for a [code-review](code-reviews.md) and when you get an approval, merge to master. Rinse and repeat.

When a code change gets on `main`, that will create Docker containers for all services and everything will get deployed to `Dev` env. For more info please see the [CD process](continuous-delivery.md)

We expect you to deliver the following:

- the business logic
- the tests
- documentation
- logs
- metrics

## Starting a new project/application

If you are adding a new application, please follow the instructions in the [monorepo README](https://github.com/island-is/island.is/blob/master/README.md).

## Dockerizing

You simply need to add an NX target to your service to enable creating a Docker image for it. For more info see [dockerizing](dockerizing.md)

## Kubernetes

We have a Helm chart template that should fit most services. You pretty much only need to add your ingress (optional), environment variables(optional) and secrets(optional) and your service can get deployed to Dev. For more info, please see [Helm charts](https://github.com/island-is/helm).
