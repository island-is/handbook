# Branching and release strategy

* Status: proposed
* Deciders: devs, devops
* Date: 2020-05-24

## Context and Problem Statement

How do we want to organise work in branches and how should changes be released? How should different branches be continuously deployed for QA?

## Decision Drivers

* We need to have confidence in our releases.
* We want more structured releases while we're still getting our footing in a shared monorepo.
* It should work well with our agile work environment.

## Considered Options

Branching strategies:

* [Git Flow]
* [GitHub Flow]
* [OneFlow]

Release strategies:

* [Continuous delivery]
* [Release trains]

## Decision Outcome

Chosen option: "OneFlow" because it provides a single eternal branch with well structured releases.

We'll implement OneFlow with these details:

* Release branches are set up the Monday after each sprint. This is sometimes called release trains, where features line up for different release trains.
* Release and quality managers from each team are responsible for reviewing and approving releases.
* Releases apply to all apps in the monorepo.
* Releases are versioned like this: `1.{sprint}.<hotfix>`. So version 1.32.2 is the release after sprint 32, with two hot fixes applied.
* Feature branches are merged using "Squash and merge", so they can be easily reverted.
* Feature branches should be short-lived. Features that are not ready to go live should be disabled with feature flags.
* If a project needs to deploy updates outside of the sprint rhythm, they should use hotfix branches.

Later we may embrace GitHub Flow, with continuous deployment into production, but only when we have enough confidence in the health of the monorepo, eg with intensive testing.

### Continuous deployment

Environment | CD                    | Databases/services | Features
------------|-----------------------|--------------------|----------
dev         | master                | Test               | All
staging     | master                | Prod               | All
pre-prod    | release/hotfix branch | Prod               | Finished
prod        | latest release tag    | Prod               | Finished

In addition to these, we also want CD for feature branches, but this has additional requirements/complications so it's out of scope for now.

## Pros and Cons of Branching Options

### Git Flow

* Good, when there needs to be multiple versions in production.
* Good, because it enforces an easy to comprehend naming convention for branches.
* Good, because it has good support in popular git tools.
* Bad, because the git history becomes unreadable.
* Bad, because the master/develop split is redundant.

### GitHub Flow

* Good, because it fits well with Continuous Delivery and Continuous Integration.
* Good, a simpler alternative to Git Flow.
* Good, when we need to maintain a single version in production.
* Bad, because production code can become unstable most easily.
* Bad, if we need release plans.

### One Flow

* Good, because it has a clean git history (with squash-and-merge).
* Good, because it has a structured release process without multiple long running branches.
* Good, because it has good parts from GitHub Flow (simple history with one branch + feature branches) and Git Flow (releases and hot fixes).
* Bad, because it makes continuous integration more difficult.

## Pros and Cons of Release Options

### Continous Delivery

* Good, because it is simpler and leaner, allowing changes to be deployed quicker.
* Bad, because it can easily break something in production if our CI isn't good enough.

### Release trains

* Good, because it has more structured releases, which helps with planning and QA.
* Good, because it can be synchronised to organisational schedule.
* Good, because it gives us a process to verify and test each release.
* Bad, because it is fairly rigid and complicated to implement organisation-wide.

## Links

* [4 branching workflows for Git](https://medium.com/@patrickporto/4-branching-workflows-for-git-30d0aaee7bf)
* [Branching patterns - Martin Fowler](https://martinfowler.com/articles/branching-patterns.html)

[Git Flow]: https://nvie.com/posts/a-successful-git-branching-model/
[GitHub Flow]: https://guides.github.com/introduction/flow/
[OneFlow]: https://www.endoflineblog.com/oneflow-a-git-branching-model-and-workflow
[Continuous delivery]: https://martinfowler.com/bliki/ContinuousDelivery.html
[Release trains]: https://martinfowler.com/articles/branching-patterns.html#release-train
