## Methods
TODO
* Describe different methods for services
* i.e. for REST is LIST, GET, CREATE, UPDATE, DELETE and how the
  map to corresponding HTTP verbs
* How should this be in SOAP, gRPC, JSON-RPC, GraphQL?


Methods are operations a client can take on resources. Follow 
[resource-oriented] design when developing methods for APIs.  Emphasize 
resources (data model) over the methods performed on the resources 
(functionality). A typical resource-oriented API exposes a large number of 
resources with a small number of methods.

Most API services 
support the following 5 operations: `LIST`, `GET`, `CREATE`, `UPDATE`, and
`DELETE` on all resources, also known as the **standard methods**. Create
**custom methods** to provide a means to express arbitrary actions that are 
difficult to model using only the **standard methods**.

A photo album service, for example, may provide the following methods:

| Method                          | Resource                                                                           |
| :------------------------------ | :----------------------------------------------------------------------------------|
| `CREATE` Creates a user       | `//my-service.island.is/users/` a collection of `User` resources                 |
| `GET` Gets a user             | `//my-service.island.is/users/my-user` a single `User` resource                  |
| `UPDATE` Updates a user       | `//my-service.island.is/users/my-user` a single `User` resource                  |
| `LIST` Lists photos of a user | `//my-service.island.is/users/my-user/photo` a collection of `Photo` resources   |
| `DELETE` Deletes a photo      | `//my-service.island.is/users/my-user/photos/my-photo` a single `Photo` resource |


For obvious reasons, operation `CREATE` and `LIST` always work on a resource
collection, and `GET`, `UPDATE` and `DELETE` a single resource. Note, 
**You should never define a method with no associated resource**.

### Methods in HTTP RESTful API services
In HTTP RESTful API services, each method must be mapped to an HTTP verb 
([HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)). 

The following table specifies the mappings between standard- and custom methods
and HTTP verbs:

| Method    | HTTP Request Method (Verb) |
| :-------  | :------------------------- |
| `LIST`    | `GET`                      |
| `GET`     | `GET`                      |
| `CREATE`  | `POST`                     |
| `UPDATE`  | `PATCH`                    |
| `DELETE`  | `DELETE`                   |
| --------  | ----------                 |
| `Custom` | `POST` (usually)            |


#### Custom methods
APIs should prefer standard methods over custom methods; the purpose of custom 
methods is to define functionality that does not cleanly map to any of the 
standard methods. Custom methods offer the same design freedom as traditional 
RPC APIs, which can be used to implement common programming patterns, such as 
database transactions, import and export, or data analysis.

To map a custom method, pick the HTTP verb closest to the nature of your custom
method. Note that when developers call the custom method, its method name must 
be attached to the end of the resource name so as to help the API service 
distinguish between standard methods and custom methods. Google Cloud Functions,
for example, supports a custom method, `generateDownloadUrl`, for downloading
the source code of a Cloud Function, and the method is mapped to the 
HTTP verb `POST`; to call this method on Cloud Function hello-world, 
one must pass an HTTP `POST` request to `https://cloudfunctions.googleapis.com/v1/hello-world:generateDownloadUrl`.


[resource-oriented]: ../design-principles/resource-oriented-design.md

