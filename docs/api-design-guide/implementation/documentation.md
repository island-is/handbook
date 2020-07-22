# Documentation
---------------------------------------------------------
Under construction - TODO:
* Describe how to document services
* Describe how to document for different technologies
  * OpenAPI for REST
  * WSDL for SOAP
  * What to use for GraphQL, gRPC / JSON-RPC, etc.
---------------------------------------------------------

## All APIs must be documented
API documentation should be targeted for the developer that will consume your
API.  A good documentation is one of the single most important quality of an 
a API.  This makes it much easier for other developers to use services and 
reduces significantly implementation time for API consumers. The API developer 
is responsible for keeping it up to date.

## Allow users to provide feedback
Provide users with a way to comment on your documentation.  This will help 
with finding concepts that need further explanation and keeping the 
documentation up to date.

## Consider using markdown
Markdown is recommended, but not required when writing documentation about an
API service. You could use a tool like [docusaurus](https://v2.docusaurus.io/) 
or [NextJS + Remark](https://github.com/vercel/next.js/tree/canary/examples/blog-starter-typescript) 
to make your markdown documents searchable and more accessible.

When documenting with markdown try to keep text lines no longer than 80 
characters for easier reading when markdown  documents are read from text 
editors.  Editors often support showing you the 80 line character limit.  For
example, in VS Code, you can add `"editor.rulers": [80]` to your 
preferences -> settings to make it show this limit.

## Write examples
The quickest way for a consumer to learn from documentation is from example 
codes.  You should figure out, which programming languages are mostly used by
the API consumers and give examples for those languages.

### Example requests and responses
A tool like [Swagger](http://swagger.io/) could help with these examples, but
it's automatic generation is not always enough.  A good practice would be to 
provide a table for describing elements or properties that need further 
explanation.

If a requests or responses support multiple representations, such as 
HTTP, XML, and JSON a good practice would be to show example for at 
least these three.

#### Here is a example of a table describing elements requests or responses
| Name     | Type    | Description                           | Remarks                     |
| :---     | :---    | :----------                           | :-------                    |
| name     | String  | Name of the person                    | Max length is 32 characters |
| age      | Number  | How many years has the person lived   | A child can be of 0 age but age will never be negative |
| address  | String  | Location where the person lives       | Max length is 36 characters |

Don't forget to describe possible errors and 
error codes your API methods can return.

## Consider using open source API specification
It is recommended using tools like [Swagger](http://swagger.io/), to help with
the documentation.  Using such tools, will help API developers with maintaining
and keeping the documentation up to date.  API consumers will also benefit with
structured and readable documentation.

You could also use tools like [APIDOC](https://apidocjs.com/) to generate 
detailed documentation about your application.  But this documentation is 
more for the API developer, not the API consumer.


## APIs must provide a information object about the service
For API management all APIs should implement a GET `/info` method which should
provide a API information object.   The API Catalog (Viskuausan) uses this
method when listing available services at island.is.

The returned object should provide the fields:
 - `version`  to distinguish API versions following [semantic versioning](https://semver.org/) specification.
 - `title` as (unique) identifying, functional descriptive name of the API.
 - `description `  containing a proper description of the API.
 - `documentation` a fully qualified url to the API documentation page.
 - `owner` the owner of the service.
 - `contact`  containing the responsible team.
   - `name`
   - `email` 

Example response from the `/info` method.  Json representation is preferred, 
but xml is also an option.

Json representation
```json
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

Xml representation
```xml
<?xml version="1.0" encoding="UTF-8" ?>
	<version>1.0.2</version>
	<title>Awesome service</title>
	<description>Provides access to the awesome database allowing you to query and submit methods on, how to better the world.</description>
	<documentation>https://moa.is/documentation/api-awesome/v1</documentation>
	<owner>Ministry Of Awesomeness</owner>
	<contact>
		<name>Johann spuck</name>
		<email>spuck@moa.com</email>
		<phone>864-5470</phone>
	</contact>
  ```