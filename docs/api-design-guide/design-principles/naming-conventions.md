# Naming Conventions
TODO
* Describe naming conventions for:
  * The api/service itself
  * Resources, data definitions & data fields
  * Methods/operations
  
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
