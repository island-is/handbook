# Versioning

Versioning APIs is necessary to ensure the possibility of continuous development of API services.  All APIs must provide a major, minor and patch version numbers.  The **major** version number must be included as the first part of the URI path for all APIs.


## Version changes

Developers should strive to make all changes backwards compatible 
(non-breaking changes). 

Versioning APIs should follow the the  [semantic versioning](https://semver.org/) specification.Given a version number MAJOR.MINOR.PATCH, increment the:
 1. MAJOR version when you make incompatible API changes,
 2. MINOR version when you add functionality in a backwards compatible manner, and
 3. PATCH version when you make backwards compatible bug fixes.

When a `major` version is incremented, a new instance of the API service must be made available.  See section **Deprecating API versions**  for guidelines on how to decommission the older running version of the API.

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
```

Additionally, the `https://my-service.island.is/v1/info` url should provide the property `version` with the MAJOR.MINOR.PATCH version number as a string value in the returned resource representation.

### Considerations when incrementing version numbers
If an API introduces a breaking change, such as removing or renaming a field, it must increment its API `major` version number to ensure that existing user code does not suddenly break, but incrementing the `major` version should be avoided whenever possible to avoid increasing maintenance and cost of running many versions of the same service.  Consider adding
**content versioning**(see below) to methods before deciding to make breaking changes. 

### Content versioning (content negotiation)
Versioning a single resource representation here described as content can be used to minimize the need for a `major` incrementation of a API version.

Versioning through content negotiation can be used to minimize the need for a breaking change of services, allowing existing clients to use the old content while new or targeted clients can access the new version of the content.  This can be done by allowing the new or targeted clients to add a `; version=2` string to the header of the request.  Further more when a new `major` version is released the new content version should in most cases become the default content version.

When a new client needs a new resource representation, it can be done without breaking the old client.   In the following two examples both old and new clients can get what they need.  

Example header request from a old client.
```
GET /users HTTP/1.1
Accept: application/json
...
```

Example header request from a new client.
```
GET /users HTTP/1.1
Accept: application/json; version=2
...
```

### Deprecating API versions
When there are more than one running instances of an API, the old versions need to be decommissioned at some time to reduce maintenance costs.

Please follow these guidelines when decommissioning APIs.

#### Advertise to clients when a specific API version will be discontinued
You should notify clients who use your service that the old version will stop working at a specified date.  You should give them a link to a new version of the service and provide them with information about all breaking changes between versions.

The specified date must not be less than 6 months from the time you notify your last client.  Exception from this rule can be made when you see via your logs that no calls to this API version are made anymore. 








