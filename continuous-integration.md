# Continuous Integration

- Status: draft
- Deciders: devs, devops
- Date: 11.05.2020

## Context and Problem Statement

We need to maintain the quality of the codebase, minimize the time between introducing quality degradation and discovering it and make sure we have deployable artefacts at all times.

## Decision Drivers (Policy)

- The code integration process needs to be independent from CI platform integration
  - Benefits
    - Easier troubleshooting of the process
    - Easier migration to a different CI platform
    - Easier experimentation
    - Easier to run as part of the development process
  - Drawbacks
    - Needs more knowledge and experience
- We use Docker as much as possible to implement the steps in the integration process
  - Benefits
    - Platform independence
    - Repeatability
    - Security
  - Drawbacks:
    - TBD
- We support only Linux as a target operating system when we cannot use Docker
  - Benefits
    - Same as the OS we use in our production environment, which minimizes the chances of failure because of OS differences
    - We minimize the effort and complexity of supporting different operating systems
    - Linux tooling works on all major other OSs today - macOS and Windows
  - Drawbacks:
    - Devs that use non-Linux OS might need to install additional software and customizations

## Considered Options

We only considered hosted solutions at this time to minimize the number of systems we need to maintain.

- GitHub Actions
- Circle CI
- AWS CodeBuild

## Decision Outcome

GitHub Actions

- Number 1 CI platform at the time of this writing
- Easy customization of which parts of the CI process to run depending on branching patterns and pull requests
- Good integration of code health with the pull request process
- As an enterprise customer, we have a large number of "compute"-minutes that come as a part of the package we are buying
- Supports parallelisation of the process which can be pretty important in the context of monorepo
- Support using own runners which can be helpful to maximize speed, minimize costs and increase security.
