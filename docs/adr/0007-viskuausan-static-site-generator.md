# Viskuausan Static Site Generator
* Status: accepted
* Deciders: devs
* Date: 2020-06-29

## Context and Problem Statement

We're going to create a web app for Viskuausan (API Catalog).
Viskuausan's static content will be written using markdown.
The problem statement is therefore: 
> What static site generator to use that has markdown support
> and aligns as well as possible to the technical direction?

## Decision Drivers

* Should conform to Stafrænt Íslands technical direction
* Should be able to support markdown content
* Should be open source
* Should be customizable to island.is UI design

## Considered Options

* [Docusaurus v2](https://v2.docusaurus.io/)
* [GatsbyJS](https://www.gatsbyjs.org/)
* [NextJS + Remark](https://github.com/vercel/next.js/tree/canary/examples/blog-starter-typescript)

## Decision Outcome

Chosen option: Docusaurus

It is a SSG that focuses on doing documentation sites really well.
It has support for markdown and mdx out-of-the-box and has quick setup.
Being built on React provides the options to do custom pages and add more 
complex logic later on if needed.


## Pros and Cons of the Options
All of the considered options are built using React, are open source and popular
site generators.

### Docusaurus v2
* Good, because it focuses on documentation
* Good, because it supports TypeScript
* Good, because it is extendable via plugins & themes
* Good, because it is ready for translations
* Good, because it supports document versioning
* Good, because it has content search out-of-the-box
* Bad, because it is still in beta
* Bad, because it requires manual setup for typescript compile-time type checking


### Gatsby
 * Good, because it has rich ecosystem of plugins
 * Good, because it supports TypeScript
 * Good, because it is really flexible
 * Good, because it has GraphQL support for external data
 * Bad, because it has high project complexity
 * Bad, because it has high learning curve
 * Bad, becuase it requires manual setup for TypeScript compile time type checking

### NextJS + Remark
* Good, because it is really flexible
* Good, because it supports TypeScript 
* Good, because it is already in use in the monorepo 
* Bad, because it is slower in setup
* Bad, because it needs custom implementation for all components

### Other honourable mentions
* [Docz](https://www.docz.site/)  
  Built using Gatsby so we would rather go with Gatsby than Docz so unneccessary to
  list as an option
