# Documentation
---------------------------------------------------------
TODO
* Describe how to document services
* Describe how to document for different technologies
  * OpenAPI for REST
  * WSDL for SOAP
  * What to use for GraphQL, gRPC / JSON-RPC, etc.
---------------------------------------------------------

## All APIs must be documented
API documentation should be targeted for the developer that will consume your API.  A good documentation is one of the single most important quality of an a API.  This makes it much easier for other developers to use services and reduces significantly implementation time for API consumers. The API developer is responsible for keeping it up to date.

## Allow users to provide feedback
Provide users with a way to comment on your documentation.  This will help with keeping the 
documentation up to date.

## Consider using markdown
Markdown is recommended, but not required when writing documentation about an API service.
You could use a tool like [docusaurus](https://v2.docusaurus.io/) or [NextJS + Remark](https://github.com/vercel/next.js/tree/canary/examples/blog-starter-typescript) to make your markdown documents searchable and more accessible.

## Write examples
### Example code
The quickest way for a consumer to learn from documentation is from example codes.  You should
figure out, which programming languages are mostly used by the API consumers and give examples for those languages.
### Example Requests and Responses
A tool like [Swagger](http://swagger.io/) could help with these examples, but it's automatic generation is not always enough.  A good practice would be to provide a table for describing 
elements or properties.

If a requests or responses support multiple representations, such as HTTP, XML, and JSON a good practice would be to give example for at least these three.

#### Here is a example of a table describing elements requests or responses
| Name     | Type    | Description                           | Remarks                     |
| :---     | :---    | :----------                           | :-------                    |
| name     | String  | Name of the person                    | Max length is 32 characters |
| age      | Number  | How many years has the person lived   | A child can be of 0 age but age will never be negative |
| address  | String  | The name of the place where the person lives | Max length is 36 characters |

## Consider using open source API specification
It is recommended using tools like [Swagger](http://swagger.io/), to help with the documentation.  Using such tools, will help API developers with maintaining and keeping the documentation up to date.  API consumers will also benefit with structured and readable documentation.

You could also use tools like [APIDOC](https://apidocjs.com/) to generate detailed documentation
about your application.  But this documentation is more for the API developer, not the API consumer.


### APIs must provide a information object about the service
For API management all APIs should implement a GET `/info` method which should provide a API information object.   The API Catalog (Viskuausan) uses this method when listing available services at island.is.

The returned object should provide the fields:
 - `version`  to distinguish API specifications versions following semantic rules.
 - `title` as (unique) identifying, functional descriptive name of the API.
 - `description `  containing a proper description of the API.
 - `documentation` a fully qualified url to the API documentation page.
 - `owner` the owner of the service.
 - `contact`  containing the responsible team.
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

