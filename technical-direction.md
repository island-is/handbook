# Technical direction

Digital Iceland has published a document describing the [Technical Direction]
for `island.is`. It describes a technical stack and priorities for large scale
collaboration. Unfortunately it is not available in English yet but we'll
summarise the highlights here.

## Frontend

* Interactive UI with [ReactJS].
* Type safety with [TypeScript]. Especially for shared code and API interfaces.
* Design system and reusable components in [Storybook].
* End to end UI testing with [Cypress].

## Backend

* Thin [GraphQL] layer, wrapping other services.
* Written in TypeScript for [Node.JS] for consistency and easy collaboration
 with front-end.
* Integrating with government services through [X-Road].
* Unit testing with [Jest]

## Priorities

* Accessibility
* Free and open source software
* Performance
* User Experience
* Stable hosting
* Internationalisation
* Development environment
* Security

## Scope

This technical direction and stack only applies to projects developed for the
`island.is` brand. It does not apply to websites or services of other
government agencies.

It is a living document, which should be updated by the Digital Iceland teams
as the project grows and best practices evolve.

[Technical Direction]: https://samradsgatt.island.is/oll-mal/$Cases/Details/?id=1536
[ReactJS]: https://reactjs.org/
[TypeScript]: https://www.typescriptlang.org/
[Storybook]: https://storybook.js.org/
[Cypress]: https://www.cypress.io/
[Node.JS]: https://nodejs.org/en/about/
[GraphQL]: https://graphql.org/
[X-Road]: https://x-road.global/
[Jest]: https://jestjs.io/