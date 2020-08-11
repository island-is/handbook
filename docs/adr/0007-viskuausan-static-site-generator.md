# Viskuausan Static Site Generator

- Status: proposed
- Deciders: devs
- Date: 2020-08-11

We're going to create a web app for Viskuausan (API Catalog).
Viskuausan consists of three main components:

- Web service catalogue
  - Displays an overview of web services.
  - Displays details about each web service.
- Data definition catalogue
  - Displays an overview of data definitions
  - Displays details about each data definition
- Design guidelines
  - Static text content describing best practices for API development

The two catalogue components require:

- Data storage
- API communication
- Other custom implementations and integration

The design guidelines component require:

- Static content written in markdown

## Context and Problem Statement

Viskuausan is proving to be more complex and larger platform than just
a simple documentation site from static content.
Which React framework provides the most out-of-the-box features that we need?

## Decision Drivers

- Should conform to Stafrænt Íslands technical direction
- Should be able to support markdown content rendered to HTML
- Should be open source
- Should be customizable to island.is UI design

## Considered Options

- [Docusaurus v2](https://v2.docusaurus.io/)
- [GatsbyJS](https://www.gatsbyjs.org/)
- [NextJS](https://github.com/vercel/next.js/)

## Decision Outcome

Chosen option: NextJS

NextJS is the chosen web framework for all island.is websites.
NextJS is more suitable for larger and more dynamic websites than
Docusaurus. As Docusaurus is focused on doing only static
markdown documentation really well, NextJS provides the tools
(database ORM, unit testing, dependency injection) needed for building
bigger platform. It is easy to add markdown support in NextJS using [Remark].

## Pros and Cons of the Options

All of the considered options are built using React, are open source
and popular site generators.

### Docusaurus v2

- Good, because it focuses on documentation
- Good, because it supports TypeScript
- Good, because it is extendable via plugins & themes
- Good, because it is ready for translations
- Good, because it supports document versioning
- Good, because it has content search out-of-the-box
- Bad, because it is still in beta
- Bad, because it requires manual setup for typescript compile-time type checking
- Bad, because it needs manual setup for ORM, dependency injection, testing and more.
- Bad, because it is not suitable for larger websites which needs more backend
  api functionality.

### Gatsby

- Good, because it has rich ecosystem of plugins
- Good, because it supports TypeScript
- Good, because it is really flexible
- Good, because it has GraphQL support for external data
- Bad, because it has high project complexity
- Bad, because it has high learning curve
- Bad, because it requires manual setup for TypeScript compile time type checking

### NextJS + Remark

- Good, because it is really flexible
- Good, because it supports TypeScript
- Good, because it is already in use in the monorepo
- Good, because it provides out-of-the-box
  - ORM for database connection
  - Dependency injection for separation of concerns and easier unit testing
  - Test suite
- Bad, because it needs custom implementation for all components

### Other honorable mentions

- [Docz](https://www.docz.site/)  
  Built using Gatsby so we would rather go with Gatsby than Docz so
  unnecessary to list as an option

[remark]: https://github.com/remarkjs/remark
