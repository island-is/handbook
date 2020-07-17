# Documentation
TODO
* Describe how to document services
* Describe how to document for different technologies
  * OpenAPI for REST
  * WSDL for SOAP
  * What to use for GraphQL, gRPC / JSON-RPC, etc.

- TODO Should we expect new services to implement **API management** section (see example below)
### API management
APIs should implement a GET `/info` method which should provide a API information object for API management. The returned object should provide the fields:
 - `version`  to distinguish API specifications versions following semantic rules
 - `title` as (unique) identifying, functional descriptive name of the API
 - `description `  containing a proper description of the API
 - `documentation` a fully qualified url to the API documentation page
 - `owner` the owner of the service.
 - `contact`  containing the responsible team
   - `name`
   - `email` 

Example response from the `/info` method
```
{
  "version": "1.0.2",
  "title": "Awesome service",
  "description": "Provides access to the awesome database allowing you to query and submit methods on, how to better the world.",
  "documentation": "https://moa.is/documentation/api-awesome/v1",
  "owner": "Ministry Of Awesomeness",
  "contact": {
    "name": "Johann spuck",
    "email": "spuck@moa.com",
    "phone": "864-5470"
  }
}
```

