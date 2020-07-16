# Versioning
**Under Construction**

TODO
* Describe versioning strategy for apis and how to deprecate older
  versions

Versioning APIs should follow the the  [semantic versioning](https://semver.org/) specification.

## Summary
Given a version number MAJOR.MINOR.PATCH, increment the:
 1. MAJOR version when you make incompatible API changes,
 2. MINOR version when you add functionality in a backwards compatible manner, and
 3. PATCH version when you make backwards compatible bug fixes.
Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.


All APIs must provide a major, minor and patch version numbers.  The **major** version number must be included as the first part of the URI path for APIs. If an API introduces a breaking change, such as removing or renaming a field, it must increment its API version number to ensure that existing user code does not suddenly break.

## Urls
In all URLs with no exceptions, APIs must expose the **major** version number, with the character `v` as a prefix.  The **minor** and **patch** version numbers should not be exposed in URLs.

### Good
```
  https://my-service.island.is/v1/users
```
### Bad
```
  https://my-service.island.is/users
  https://my-service.island.is/v1.2/users
  https://my-service.island.is/v1.2.3/users
```

