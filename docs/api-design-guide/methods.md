# Methods

Methods are operations a client can take on resources. Follow
[resource-oriented design] when developing methods for APIs. Emphasize
resources (data model) over the methods performed on the resources
(functionality). A typical resource-oriented API exposes a large number of
resources with a small number of methods.

Most API services support the following 5 operations: `LIST`, `GET`,
`CREATE`, `UPDATE`, and `DELETE` on all resources, also known as the
**standard methods** ([CRUD]). Create **custom methods** to provide
a means to express arbitrary actions that are difficult to model
using only the **standard methods**.

A photo album service, for example, may provide the following methods:

| Method                          | Resource                                                  |                                    |
| :------------------------------ | :-------------------------------------------------------- | :--------------------------------- |
| `CREATE` _Creates a user_       | `//my-service.island.is/v1/users`                         | a collection of `User` resources   |
| `GET` _Gets a user_             | `//my-service.island.is/v1/users/:userId`                 | a single `User` resource           |
| `UPDATE` _Updates a user_       | `//my-service.island.is/v1/users/:userId`                 | a single `User` resource           |
| `LIST` _Lists photos of a user_ | `//my-service.island.is/v1/users/:userId/photos`          | a collection of `Photos` resources |
| `DELETE` _Deletes a photo_      | `//my-service.island.is/v1/users/:userId/photos/:photoId` | a single `Photo` resource          |

For obvious reasons, operation `CREATE` and `LIST` always work on a resource
collection, and `GET`, `UPDATE` and `DELETE` a single resource.  
**Note:** _You should never define a method with no associated resource_.

## Methods mapping to HTTP verbs

In HTTP RESTful API services, each method must be mapped to an HTTP verb
([HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)).

The following table specifies the mappings between standard and custom methods
and HTTP verbs:

| Method   | HTTP Request Method (Verb) |
| :------- | :------------------------- |
| `LIST`   | `GET`                      |
| `GET`    | `GET`                      |
| `CREATE` | `POST`                     |
| `UPDATE` | `PATCH`/`PUT`              |
| `DELETE` | `DELETE`                   |
| `Custom` | `POST` (usually)           |

## Custom methods

APIs should prefer standard methods over custom methods. But in the real world
there is often need to provide custom methods. A custom method is an action
that does not cleanly map to any of the standard methods. The way to add custom
methods to your API is to nounify the action and make it a sub-resource.

### Example

An API has a `Message` resource and it provides the standard [CRUD] methods like:

```
GET    https://api.island.is/v1/messages
GET    https://api.island.is/v1/messages/{messageId}
POST   https://api.island.is/v1/messages
PUT    https://api.island.is/v1/messages/{messageId}
DELETE https://api.island.is/v1/messages/{messageId}
```

Then there is a requirement to provide a functionality to be able to archive and
unarchive a single message and a batch of messages. The archiving and unarchiving
a single message is then provided by:

```
POST   https://api.island.is/v1/messages/{messageId}/archives
DELETE https://api.island.is/v1/messages/{messageId}/archives
```

The batch archiving is provided by

```
POST   https://api.island.is/v1/messages/archives
DELETE https://api.island.is/v1/messages/archives
```

_Note:_ The `POST` methods accepts list af message Ids in the request body.

## HTTP Status Response codes

Try to minimize the number of HTTP status codes a REST API returns. When
more details are needed in a error response use application defined errors
and supply them in a response error object, described in the [errors] document.

For each HTTP method, you should try to use only status
codes marked with **X** in the following table.

| Code | Meaning      | GET | POST | PUT | PATCH | DELETE |
| :--- | :----------- | :-: | :--: | :-: | :---: | :----: |
| 200  | OK           |  X  |      |  X  |   X   |   X    |
| 201  | Created      |     |  X   |     |       |        |
| 204  | No Content   |     |      |  X  |   X   |   X    |
| 400  | Bad Request  |     |  X   |  X  |   X   |        |
| 401  | Unauthorized |  X  |  X   |  X  |   X   |   X    |
| 403  | Forbidden    |  X  |  X   |  X  |   X   |   X    |
| 404  | Not Found    |  X  |      |  X  |   X   |        |
| 500  | Server error |  X  |  X   |  X  |   X   |   X    |

- General for all methods

  - `401` should be returned when client fails to authenticate.
  - `403` should be returned when client is authenticated but does not have
  necessary permission to perform the operation.
  - `500` should be returned when the server encounters some unexpected error,
  preferably along with an [errors] object.

- `GET` for retrieving a resource or a collection of resources.

  - `200` should be returned on success.
    If a collection asked for is empty, `200` is still to be returned.
  - `404` should be returned when a resource asked for is not found.

- `POST` for creating a resource.

  - `201` should be returned if the resource was created. The response
    body should contain a resource identifier to the created resource.
  - `400` should be returned if the request is invalid, i.e. the resource
    already exists or contains invalid fields.

- `PUT` for updating a existing resource.

  - `200` should be returned after a successful execution,
    when there is a need for content in the response.
  - `204` should be returned after a successful execution,
    as usually there is no need for content in the response.
  - `400` should be returned if the request is invalid,
    i.e. the resource contains invalid fields.
  - `404` should be returned if the resource to be updated is not found.

- `PATCH` for making a partial update on a resource.

  - `200` should be returned after a successful execution,
    when there is a need for content in the response.
  - `204` should be returned after a successful execution,
    as usually there is no need for content in the response.
  - `400` should be returned if the request is invalid,
    i.e. the resource contains invalid fields.
  - `404` should be returned if the resource to be updated is not found.

- `DELETE` for removing a resource.
  - `200` can be returned after a successful execution,
    when there is a need for a content in the response.
  - `204` should be returned after a successful execution  
    **Note:** If a client asks for the removal of a resource already deleted
    `204` should be returned, **not** `404`, because clients usually do not care
    if a resource was previously deleted.

[resource-oriented design]: ./resource-oriented-design.md
[errors]: ./errors.md#rest
[crud]: https://en.wikipedia.org/wiki/Create,_read,_update_and_delete
