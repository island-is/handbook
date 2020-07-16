# Resource Oriented Design

The data (resource) should control the design of the service. As the data is 
the key player and the service is centered around making the data accessable.

## Design flow

The Design Guide suggests taking the following steps when designing resource- 
oriented APIs (more details are covered in specific sections below):

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

Resource name consists of the resource’s type, its identifier, the resource name of its parent and the name of the API service. The type is known as the Collection ID, and the identifier is known as the Resource ID. Resource IDs are usually random strings assigned by the API service, though it is also OK to accept custom resource IDs from clients. 
**Collection ID's must be plural** and **Resource ID's should be immutable**.

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

## Fields
A resource may have one or more fields, and resources of the same type share the same collection of fields. For example, a resource of type users may have field `name`, `display_name`, `email` associated with it. Note that one of these fields must be its resource name, a string that uniquely identifies the resource in the service; usually field name is reserved for this purpose.

There are three types of fields:
| Type     | Description                                                                                                       |
|----------|-------------------------------------------------------------------------------------------------------------------|
| Required | Required fields must be populated by clients.                                                                     |
| Optional | Optional fields can be populated by clients. If left empty, they will be automatically filled by the server.      |
| Reserved | Reserved fields are only populated by server. API services should ignore user-provided values in reserved fields. |

## RPC
For RPC See [RPC - Resource-oriented design](./rpc-resource-oriented-design.md)

#### References
- [Google: Resource-oriented design](https://google.aip.dev/121)
- [Ratros Y: Designing APIs](https://medium.com/@ratrosy/designing-apis-4eed43409f93)



