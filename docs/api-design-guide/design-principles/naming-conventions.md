# Naming Conventions

Adapted from [StyleGuide] and [Google].

This document describes API naming conventions related to services and resources,
with focus on the general consumer experience. For further information about
our naming conventions related to developer experience please refer to our
[coding standard].

## General

In order to provide consistent consumer experience across the government API ecosystem and over a long period of time, all names used by an API should be:

- simple
- intuitive
- consistent

One goal of these naming conventions is to ensure that the majority of consumers
can easily understand an API. It does this by encouraging the use of simple, consistent and small vocabulary when naming methods and resources.
It also enforces names to be in British English. A developer should use our [glossary] list when in trouble finding the appropriate English translation of
an Icelandic concept.

Commonly accepted short forms or abbreviations of long words may be used for
brevity. For example, API is preferred over Application Programming Interface.
Use intuitive, familiar terminology where possible. For example, when describing
removing (and destroying) a resource, delete is preferred over erase.
Use the same name or term for the same concept, including for concepts
shared across the ecosystem.

Name overloading should be avoided. Use different names for different concepts.  
_Developer should use [Viskuausan] to look up existing
concepts before naming services and resources._

Overly general names that are ambiguous within the context of the
API and the government's larger API ecosystem should be avoided.
They can lead to misunderstanding of API concepts.
Specific names that accurately describe the API concept and distinguish it
from other relevant concepts should be used.
There is no definitive list of names to avoid, as every name must be
evaluated in their context.

**Bad**

```
Info     // info about what?
Service  // service for what?
```

**Good**

```
Order        // Info about Order object
OrderService // Service that works with the Order resource
```

Carefully consider use of names that may conflict with keywords in common
programming languages. Such names may be used but will likely trigger
additional scrutiny during API review. Use them judiciously and sparingly.

## Services

Use `PascalCase` for services.

> Reason: Fairly conventional in standard JavaScript. Purpose of class is obvious.

Use nouns affixed with Service to distinguish it from models.
Should be short and descriptive when possible.

### Bad

```javascript
class Foos {}
class barService {}
```

### Good

```javascript
class FooService {}
class BarService {}
```

## Models

Use `PascalCase` for models.

> Reason: Fairly conventional in standard JavaScript. Distinguishes it from variables and functions.

Should be descriptive single case noun.

### Bad

```javascript
class Foos {}
class bar {}
```

### Good

```javascript
class Foo {}
class Bar {}
```

## Properties and methods

Use `camelCase` for properties and methods.

> Reason: Conventional JavaScript and improved readability.

### Bad

```javascript
class Foo {
  Bar: number;
  Baz() {}
}
```

### Good

```javascript
class Foo {
  bar: number;
  baz() {}
}
```

## URI

The [URI] defined in [RFC3986] consists of the five components scheme,
authority, path, query and fragment.

```
https://example.com:8042/over/there?name=ferret#nose
\___/   \______________/\_________/ \_________/ \__/
  |            |            |            |        |
scheme     authority       path        query   fragment
```

Example URI of a authority and a path component

```

//example.com/users/1/photos/121
  \_________/ \___/   \____/ \_/
      |         |        |    \
      |         |        |      Resource ID
      |         |        |         (type)
      |         |         \
      |         |           Collection ID
      |         |              (type)
      |          \
      |            Resource name of parent resource
       \
         API service name
```

Please follow the following naming conventions

- Do not end a path with a trailing forward slash (`/`).
- When convenient, lowercase letters are preferred in URI paths since capital
  letters can sometimes cause problems.
- Use the forward slash (`/`) in a path to indicates hierarchical relationship
  between resources.
- [Resource names and collection ID's] must be the plural form of the noun used
  for the resource.

<!-- URLs -->

[coding standard]: https://github.com/island-is/handbook/blob/feature/add-api-design-guide-structure/code-standards.md
[styleguide]: https://basarat.gitbook.io/typescript/styleguide
[google]: https://cloud.google.com/apis/design/naming_convention
[glossary]: https://github.com/island-is/handbook/blob/feature/add-api-design-guide-structure/glossary.md
[viskuausan]: https://viskuausan.island.is/
[uri]: https://en.wikipedia.org/wiki/Uniform_Resource_Identifier
[rfc3986]: https://tools.ietf.org/html/rfc3986
[resource names and collection id's]: https://github.com/island-is/handbook/blob/feature/add-api-design-guide-structure/docs/api-design-guide/design-principles/resource-oriented-design.md#user-content-resources
