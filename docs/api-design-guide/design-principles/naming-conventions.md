# Naming Conventions

Adapted from [StyleGuide].

In order to provide consistent developer experience across many APIs and over a long period of time, all names used by an API should be:

* simple
* intuitive
* consistent

Since many developers are not native English speakers, one goal of these naming conventions is to ensure that the majority of developers can easily understand an API. It does this by encouraging the use of a simple, consistent, and small vocabulary when naming methods and resources.

Names used in APIs should be in correct American English. For example, license (instead of licence), color (instead of colour).
Commonly accepted short forms or abbreviations of long words may be used for brevity. For example, API is preferred over Application Programming Interface.
Use intuitive, familiar terminology where possible. For example, when describing removing (and destroying) a resource, delete is preferred over erase.
Use the same name or term for the same concept, including for concepts shared across APIs.
Avoid name overloading. Use different names for different concepts.
Avoid overly general names that are ambiguous within the context of the API and the larger ecosystem of Google APIs. They can lead to misunderstanding of API concepts. Rather, choose specific names that accurately describe the API concept. This is particularly important for names that define first-order API elements, such as resources. There is no definitive list of names to avoid, as every name must be evaluated in the context of other names. Instance, info, and service are examples of names that have been problematic in the past. Names chosen should describe the API concept clearly (for example: instance of what?) and distinguish it from other relevant concepts (for example: does "alert" mean the rule, the signal, or the notification?).
Carefully consider use of names that may conflict with keywords in common programming languages. Such names may be used but will likely trigger additional scrutiny during API review. Use them judiciously and sparingly.

Whenever possible the name should make further explanations such as code comments unnecessary. If that is not possible provide comments.

## Services
Use ```PascalCase``` for services.
> Reason: Fairly conventional in standard JavaScript. Purpose of class is obvious.

Use nouns affixed with Service to distinguish it from models. Should be short and descriptive when possible.

### Bad
```javascript
class Foos { };
class barService {};
```

### Good
```javascript
class FooService {};
class BarService {};
```

## Variable and function
Use ```camelCase``` for variable and function names.
> Reason: Conventional JavaScript. Distinguishes from class names.

### Bad
```javascript
var FooVar;
function BarFunc() {}
```

### Good
```javascript
var fooVar;
function barFunc() {};
```

## Models
Use ```PascalCase``` for models.
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
Use ```camelCase``` for properties and methods.
> Reason: Conventional JavaScript and improved readability.

### Bad
```javascript
class Foo {
  Bar: number;
  Baz() { }
}
```

### Good
```javascript
class Foo {
  bar: number;
  baz() {}
}
```

## Enums
Use ```PascalCase``` for enum names.
> Reason: Similar to Class. Is a Type.

### Bad
```javascript
enum color {
}
```

### Good
```javascript
enum Color {
}
```

## Global variables and constants
Use ```UPPERCASE``` for global variables.
> Reason: Conventional JavaScript and many other programming languages.

### Bad
```javascript
const pi: number = 3.14;
declare var foo: string = "Foo";
```

### Good
```javascript
const PI: number = 3.14;
declare var FOO: string = "Foo";
```

[StyleGuide]: https://basarat.gitbook.io/typescript/styleguide
