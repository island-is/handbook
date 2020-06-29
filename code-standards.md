# Code standards

We use [Prettier] and [ESLint] to automatically enforce most of our Code
Standards. Most of our rules follow recommendations from both project with
these additions and changes:

- Prettier is configured with single quotes, no semicolons, arrow parens and
 all trailing commas.
- ESLint is configured to catch likely errors but otherwise provide warnings to
encourage best practices without stopping the developer.The base configuration
comes from NX.

Code standard changes can be proposed to the larger team in discipline
meetings. For any new rule, we should try to enforce it automatically, even
if it means creating a new ESLint rule from scratch.

## Language

All code, documentation and API interfaces should be written in British English.
This makes the project more inclusive, and reduces awkward mixing of languages.

This can be challenging when dealing with government domain words. However,
the goal is to provide all of our services in English as well as Icelandic,
so we need to find good translations anyways.

When in doubt, check out the [Glossary]. If something is missing from it, you
can ask for suggestions in the team. Just remember to add any new
translations to the Glossary.

When integrating with a web service that has its interface in Icelandic, all
endpoints and fields should be translated to and from English in the integration
layer, so other parts of the system can use English-language objects and
functions. 

### Fail

```typescript
const kennitala = '...'

const typeDefs = gql`
  Mutation {
    applyForVegabref: VegabrefPayload!
  }
`
```

### Pass

```typescript
const nationalId = '...'

const typeDefs = gql`
  Mutation {
    applyForPassport: PassportPayload!
  }
`
```

## Naming conventions

Adapted from [StyleGuide].

Whenever possible the name should make further explanations such as code comments unnecessary. If that is not possible provide comments.

### Services
Use ```PascalCase``` for services.
> Reason: Fairly conventional in standard JavaScript. Purpose of class is obvious.

Use nouns affixed with Service to distinguish it from models. Should be short and descriptive when possible.

#### Bad
```javascript
class Foos { };
class barService {};
```

#### Good
```javascript
class FooService {};
class BarService {};
```

### Variable and function
Use ```camelCase``` for variable and function names.
> Reason: Conventional JavaScript. Distinguishes from class names.

#### Bad
```javascript
var FooVar;
function BarFunc() {}
```

#### Good
```javascript
var fooVar;
function barFunc() {};
```

### Models
Use ```PascalCase``` for models.
> Reason: Fairly conventional in standard JavaScript. Distinguishes it from variables and functions.

Should be descriptive single case noun.

#### Bad
```javascript
class Foos {}
class bar {}
```

#### Good
```javascript
class Foo {}
class Bar {}
```

### Properties and methods
Use ```camelCase``` for properties and methods.
> Reason: Conventional JavaScript and improved readability.

#### Bad
```javascript
class Foo {
  Bar: number;
  Baz() { }
}
```

#### Good
```javascript
class Foo {
  bar: number;
  baz() {}
}
```

### Global variables and constants
Use ```UPPERCASE``` for global variables.
> Reason: Conventional JavaScript and many other programming languages.

#### Bad
```javascript
const pi: number = 3.14;
declare var foo: string = "Foo";
```

#### Good
```javascript
const PI: number = 3.14;
declare var FOO: string = "Foo";
```

[Prettier]: https://prettier.io/
[ESLint]: https://eslint.org/
[Glossary]: glossary.md
[StyleGuide]: https://basarat.gitbook.io/typescript/styleguide
