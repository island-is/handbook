# Resource Oriented Design

The data (resource) should control the design of the service. As the data is 
the key player and the service is centered around making the data accessable.

## Design flow

The Design Guide suggests taking the following steps when designing resource- 
oriented APIs.

  - Determine what types of resources an API provides.
  - Determine the relationships between resources.
  - Decide the resource name schemes based on types and relationships.
  - Decide the resource schemas.
  - Attach minimum set of methods to resources.

## Resources
A resource-oriented API is generally modeled as a resource hierarchy, where 
each node is either a simple resource or a collection resource. For convenience, 
they are often called a resource and a collection, respectively.

  - A collection contains a list of resources of the same type. For example, 
    a user has a collection of photos.
  - A resource has some state and zero or more sub-resources. Each sub-resource 
    can be either a simple resource or a collection resource.

Resource name consists of the resource’s type, its identifier, the resource name of
its parent and the name of the API service. The type is known as the Collection ID, 
and the identifier is known as the Resource ID. Resource IDs are usually random 
strings assigned by the API service, though it is also OK to accept custom 
resource IDs from clients. **Collection ID's must be must be the plural form of 
the noun used for the resource** and **Resource ID's should be immutable**.

Below are two examples of valid resource names:

A user
```
       //my-service.island.is / users / 1
                  |               |     |
                  |               |      \
                  |               |       Resource ID
                  |                \  
                  |                 Collection ID 
                   \                   (type)
                    API service name
```

A photo
```
       //my-service.island.is / users / 1 / photos / 1
                  |               |           |      |
                  |               |           |       \
                  |               |           |        Resource ID 
                  |               |           |          (type)   
                  |               |            \  
                  |               |              Collection ID
                  |               |                 (type)
                  |                \     
                   \                Resource name of parent resource
                    API service name
       
```

Resource names are referenced throughout your API service. For HTTP RESTful API services, 
resource names will become the HTTP endpoints (HTTP URL paths); 
[gRPC API services](https://grpc.io/docs/what-is-grpc/) use these values in the requests 
and responses directly.

## Fields
A resource may have one or more fields, and resources of the same type share the same 
collection of fields. For example, a resource of type users may have field `name`, 
`display_name`, `email` associated with it. Note that one of these fields must be its
resource name, a string that uniquely identifies the resource in the service; usually 
field name is reserved for this purpose.

There are three types of fields:
| Type     | Description                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------|
| Required | Required fields must be populated by clients.                                                                     |
| Optional | Optional fields can be populated by clients. If left empty, they will be automatically filled by the server.      |
| Reserved | Reserved fields are only populated by server. API services should ignore user-provided values in reserved fields. |

It is up to developers themselves to determine the types of fields. There is an exception though: the `name` field 
**should always be a reserved field**.


## Methods
Methods are operations a client can take on resources. Most API services support the 
following 5 operations: `LIST`, `GET`, `CREATE`, `UPDATE`, and `DELETE` on all resources, 
also known as the **standard methods**. Create **custom methods** to provide a means to 
express arbitrary actions that are difficult to model using only the **standard methods**. 
Note, _APIs should prefer **standard methods** over **custom methods**_ when possible.


A photo album service, for example, may provide the following methods:
| Method                          | Resource                                                                |
|---------------------------------|-------------------------------------------------------------------------|
| `CREATE` (Creates a user)       | `//my-service.island.is/users/` (a collection of `User` resources)                 |
| `GET` (Gets a user)             | `//my-service.island.is/users/my-user` (a single `User` resource)                  |
| `UPDATE` (Updates a user)       | `//my-service.island.is/users/my-user` (a single `User` resource)                  |
| `LIST` (Lists photos of a user) | `//my-service.island.is/users/my-user/photo` (a collection of `Photo` resources)   |
| `DELETE` (Deletes a photo)      | `//my-service.island.is/users/my-user/photos/my-photo` (a single `Photo` resource) |


For obvious reasons, operation `CREATE` and `LIST` always work on a resource collection, 
and `GET`, `UPDATE` and `DELETE` a single resource. Note, **You should never define a
 method with no associated resource**.

### Methods in HTTP RESTful API services
In HTTP RESTful API services, each method must be mapped to an HTTP verb 
([HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)). 

The following table specifies the mappings between standard- and custom methods and HTTP verbs:
| Method   | HTTP Request Method (Verb) |
|----------|----------------------------|
| `LIST`   | `GET`                      |
| `GET`    | `GET`                      |
| `CREATE` | `POST`                     |
| `UPDATE` | `PATCH`                    |
| `DELETE` | `DELETE`                   |
| `Custom` | `POST` (usually)           |

To map a custom method, pick the HTTP verb closest to the nature of your custom method. Note that when developers call the custom method, its method name must be attached to the end of the resource name so as to help the API service distinguish between standard methods and custom methods. Google Cloud Functions, for example, supports a custom method, `generateDownloadUrl`, for downloading the source code of a Cloud Function, and the method is mapped to the HTTP verb `POST`; to call this method on Cloud Function hello-world, one must pass an HTTP `POST` request to
```
https://cloudfunctions.googleapis.com/v1/hello-world:generateDownloadUrl
```


## Remote procedure calls (RPC)
For [RPC](https://en.wikipedia.org/wiki/Remote_procedure_call) See 
[RPC - Resource-oriented design](./rpc-resource-oriented-design.md)

#### References
- [Google: Resource Oriented Design](https://cloud.google.com/apis/design/resources)
- [Ratros Y: Designing APIs](https://medium.com/@ratrosy/designing-apis-4eed43409f93)



