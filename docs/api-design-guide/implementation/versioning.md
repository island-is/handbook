# Versioning
**Under Construction**

TODO
* Describe versioning strategy for apis and how to deprecate older
  versions

Versioning APIs is necessary to ensure the possibility of continuous development of API services.  All APIs must provide a major, minor and patch version numbers.  The **major** version number must be included as the first part of the URI path for all APIs.


## Version changes

Developers should strive to make all changes backwards compatible 
(non-breaking changes). 

Versioning APIs should follow the the  [semantic versioning](https://semver.org/) specification.Given a version number MAJOR.MINOR.PATCH, increment the:
 1. MAJOR version when you make incompatible API changes,
 2. MINOR version when you add functionality in a backwards compatible manner, and
 3. PATCH version when you make backwards compatible bug fixes.

### Considerations when incrementing version numbers
If an API introduces a breaking change, such as removing or renaming a field, it must increment its API version number to ensure that existing user code does not suddenly break, but incrementing the major version should be avoided whenever possible to avoid increasing maintenance and cost of running many versions of the same service.  Consider adding
content versioning to methods before deciding to make breaking changes. 

### Content versioning
Versioning a single resource representation here described as content can be used to minimize the need for a major incrementation of a API version.

Content versioning (Versioning through content negotiation) can be used to minimize the need for a breaking change of services, allowing existing clients to use the old content while new or targeted clients can access the new version of the content.  This can be done by allowing the new or targeted clients to add a `; version=2` string to the header of the request.  Further more when a new **major** version is released the new content version should become the default content version.

Example header request from a client
```
GET /hello HTTP/1.1
Accept: application/json; version=2
...
```




## Urls
In all URLs with no exceptions, APIs must expose the **major** version number, with the character `v` as a prefix.  The **minor** and **patch** version numbers should not be exposed in URLs.

### Good
```
  https://my-service.island.is/v1/users
```
### Bad
```
  https://my-service.island.is/users
  https://my-service.island.is/users?v=1
  https://my-service.island.is/users?version=1
  https://my-service.island.is/v1.2/users
  https://my-service.island.is/v1.2.3/users
  https://my-service.island.is/users?v=1
```

