## Methods

TODO

- Describe different methods for services
- i.e. for REST is LIST, GET, CREATE, UPDATE, DELETE and how the
  map to corresponding HTTP verbs
- How should this be in SOAP, gRPC, JSON-RPC, GraphQL?

Methods are operations a client can take on resources. Follow
[resource-oriented] design when developing methods for APIs. Emphasize
resources (data model) over the methods performed on the resources
(functionality). A typical resource-oriented API exposes a large number of
resources with a small number of methods.

Most API services
support the following 5 operations: `LIST`, `GET`, `CREATE`, `UPDATE`, and
`DELETE` on all resources, also known as the **standard methods** ([CRUD]). Create
**custom methods** to provide a means to express arbitrary actions that are
difficult to model using only the **standard methods**.

A photo album service, for example, may provide the following methods:

| Method                        | Resource                                                                         |
| :---------------------------- | :------------------------------------------------------------------------------- |
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

| Method   | HTTP Request Method (Verb) |
| :------- | :------------------------- |
| `LIST`   | `GET`                      |
| `GET`    | `GET`                      |
| `CREATE` | `POST`                     |
| `UPDATE` | `PATCH`/`PUT`              |
| `DELETE` | `DELETE`                   |
| -------- | ----------                 |
| `Custom` | `POST` (usually)           |

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

#### Response codes from HTTP methods

Try to minimize the number of HTTP status codes a _REST_ API returns. When
more details are needed in a error response use application defined errors
and supply them in a _Rest error object_, described in the [errors] document.

For each HTTP method, you should try to use only status codes marked with **X**
in the following table.

| Code | Meaning      | GET | POST | PUT | PATCH | DELETE |
| :--- | :----------- | :-: | :--: | :-: | :---: | :----: |
| 200  | OK           |  X  |      |     |       |        |
| 201  | Created      |     |  X   |     |       |        |
| 202  | Accepted     |     |      |     |       |        |
| 204  | No Content   |     |      |  X  |   X   |   X    |
| 400  | Bad Request  |  X  |  X   |  X  |   X   |        |
| 401  | Unauthorized |     |      |     |       |        |
| 403  | Forbidden    |     |      |     |       |        |
| 404  | Not Found    |  X  |      |  X  |   X   |        |
| 500  | Server error |  X  |  X   |  X  |   X   |   X    |

- `GET` for retrieving a resource or a collection of resources. On success,
  status code `200` should be returned . If a collection asked for, is empty
  `200` is still to be returned. When a resource asked for is not found, `404`
  should be returned.

- `POST` for creating a resource. If the resource did not previously exist and
  was created the response should be http status code `201` and in the response
  body a resource identifier to the created resource.

- `PUT` for updating a existing resource. After a successful execution there
  is usually no need for a additional content so `204` should be returned. In
  the rare case a response is needed in the body the `200` status code should be
  returned. If a resource to be updated is not found `404` should be returned.

- `PATCH` for making a partial update on a resource. After a successful
  execution `204` should be returned. Patch should only return content in a
  response body when a error occurs.

- `DELETE` for removing a resource. After a successful execution `204` should
  be returned. If a client asks for the removal of a resource already deleted
  `204` should be returned, **not** `404`, because clients usually do not care
  if a resource was previously deleted.

[resource-oriented]: ../design-principles/resource-oriented-design.md
[errors]: ./errors.md#rest
[crud]: https://en.wikipedia.org/wiki/Create,_read,_update_and_delete
