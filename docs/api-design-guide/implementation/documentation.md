# Documentation
API documentation should be targeted for the developer that will consume your
API.  A good documentation is one of the single most important quality of an 
a API.  It makes it much easier for other developers to use services and 
reduces significantly implementation time for API consumers. The API developer 
is responsible for keeping it up to date.

To help with keeping documentation up to date consider using automatic 
generation tools. 

## Consider using markdown
Markdown is recommended, but not required when writing documentation about an
API service. You could use a tool like [docusaurus] or [NextJS + Remark]
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

Consider creating a **Getting Started** document where you can describe
how a client can start using your service.  

Something to consider for a Getting Started page:
 - Who to contact to get access, give:
   - a link to a application form or 
   - email or 
   - who to call to get access to your service.
 - Describe if a client will need to authenticate him self.
   - Will he need to be issued a certificate?
   - Will he need to apply for a user and password?
 - Create example codes on how to call the [/info] method in your service.
   - Create a Node.js example.
   - Create a Microsoft .NET Core example.
   - Create examples for other frameworks your current clients are using or other 
     common frameworks.

### Example requests and responses
A automatic generation tools like [Swagger] could help with these examples, 
but it's automatic generation is not always enough.  A good practice would be to
provide a table for describing elements or properties that need further 
explanation.

If a requests or responses support multiple representations, such as HTTP, XML, 
and JSON a good practice would be to show example for at least these three.

When you use tables you will need to provided links to other tables for nested 
elements or objects.  When this is the case (for simple objects/elements), you
could also provide the the description as a list allowing you to intent for each 
element or object.

#### Here is a example of a table describing elements in a request or a response
| Name     | Type    | Description                           | Remarks                     |
| :---     | :---    | :----------                           | :-------                    |
| name     | String  | Name of the person                    | Max length is 32 characters |
| age      | Number  | How many years has the person lived   | A child can be of 0 age but age will never be negative |
| address  | String  | Location where the person lives       | Max length is 36 characters |

## Describe Error handling
Describe how your application handles errors.  Provide information on which 
[HTTP status codes] a client consuming your service, can expect the API to 
return and provide information on application defined errors and how the errors 
are presented to clients. See [Errors] for recommendations.

## Provide feedback mechanism
Provide users with a way to comment on your documentation.  This will help 
with finding concepts that need further explanation and keeping the 
documentation up to date.

## Automatic documentation generation 
  Using tools for Automatic documentation generation, will help API developers
  with maintaining and keeping the documentation up to date. API consumers will
  also benefit with structured and readable documentation.

### REST
It is recommended using the [OpenAPI] Specification to describe *REST* services.
Tools like [Swagger] can then be used to help with the documentation. Other 
tools like [Postman] are available but are not as well known as Swagger.

### JSON-RPC
  [open-rpc] is a possible solution for automatic document generation for 
  *JSON-RPC 2.0* APIs.

### SOAP
For *SOAP* APIs, there are number of automatic generation documentation tools 
available to help with documentation generation from WSDL files.  To name few
[TechWriter], [oxygen XML Editor] and [Altova XMLSpy] are such tools.

### GraphQL
When documenting a GraphQL service automatically you could use the
[graphql-docs] npm package.

You could also do it directly from your API by printing the GraphQL schema 
language using [graphiql]. ([Source](https://stackoverflow.com/questions/39504986/document-a-graphql-api))

Example code:
```javascript
var graphql = require('graphql');
var introspectionSchema = {}; // paste schema here
console.log(graphql.printSchema(graphql.buildClientSchema(introspectionSchema)));
```

Example result could look something like this:
```
# An author
type Author {
  id: ID!

  # First and last name of the author
  name: String
}

# The schema's root query type
type Query {

  # Find an author by name (must match exactly)
  author(name: String!): Author
}
```

### Source code documentation generation
You could also use tools to generate detailed documentation about your 
application.  But this documentation is more for the API developer, not the API
consumer.

To name few [DocFX],[APIDOC] and [Doxygen] could be used to to generate detailed 
documentation from the application code.



---------------------------------------------------------

## info method
For API management all APIs **MUST** implement a GET `/info` method which should
provide a API information object.   The API Catalog (Viskuausan) uses this
method when listing available services at island.is.

The returned object should provide the following fields:
 - **version**  (*String*) to distinguish API versions following 
   [semantic versioning] specification.
 - **title** (*String*) as (unique) identifying, functional descriptive name of 
   the API.
 - **description** (*String*) containing a short but proper description of the 
   API.
 - **access** (*List of String*) Who can have access to the service.  Possible
   string values are `open`, `islykill`, `trusted`, `trustedPriority` and
   `trustedEssential`.
 - **type** (*String*) What kind of a service is this? Possible values:
   `rest`,`graphql`,`json-rpc`,`xml-rpc`,`soap` or something else not mentioned 
   here.
 - **data** (*List of String*) What kind of data does this service work with.
   `open`,`official`,`personal`,`health`,`financial`.
 - **price** (*List of String*) Cost of using this service
   `free`,`usage`,`daly`,`monthly`,`yearly`,`custom`.
 - **links** (*Object*) Links regarding the service
     - **documentation** (*String*) a fully qualified url to the API 
       documentation page.
     - **responsibleParty** (*String*) a fully qualified url to a online page 
       containing information about the responsible party/owner of the service. 
     - **bugReport** (*String*) a fully qualified url to a online page or form a 
       consumer can report bugs about the service.
     - **featureRequest** (*String*) a fully qualified url to a online page or 
       form a consumer can ask for a new feature in api service.
 - **upTime** (*Object*) When can clients consuming the service expect the 
   service to be available.     
     - **percentage** (*Number*) a decimal number representing the up time 
       promise this service makes.  If 0 is returned as a value, it means that 
       no up time promise is maid for this service.  If no `weekly` object is
       provided, clients can assume that the percentage value applies to all 
       days, all the time.
     - **weekly** (*Object*) this is an _optional_ element which can be returned 
       if the service up time promise will only be maid for specific days in the
       week (f.example workdays).
       - **weekdays** (*List of numbers*) where each number represents a weekday
         where sunday is `0`, monday is `1` and saturday is `6`.
       - **from** (*String*) from what time during each day is the upTime 
         promise made.  See [date string format].
       - **to** what time during each day will the service upTime promise stop.
         See [date string format].
 - **responseTime** (*Number*) a positive integer which contains information on 
   what is the longest possible time in milliseconds a client consuming the 
   service will have to wait for a response.  If `0` is returned as a value, 
   it means that the response time is undetermined.
 - **contact**  (*Object*) quick information, who to contact when an issue about
   the service arises.
     - **name** (*String*) name of the person
     - **email** (*String*) fully qualified email
     - **phone** (*String*) a phone number starting with the `+` sign, followed 
     by the country code, a space and the phone number.



Example response from the `/info` method.  Json representation is preferred, 
but xml is also an option.

Json representation example 
```json
{
    "version"              : "1.0.2",
    "title"                : "Awesome service",
    "description"          : "Provides access to the awesome database allowing you to query and submit methods on, how to better the world.",
    "access"               : ["trustedPriority,trustedEssential"],
    "type"                 : "rest", 
    "data"                 : ["official","personal"],
    "price"                : ["usage","custom"]  ,
    "links"                : {
        "documentation"      : "https://moa.is/documentation/api-awesome/v1",
        "responsibleParty" : "https://api-awesome/responsible",
        "bugReport"        : "https://github.com/moa.is/api-awesome/issues/new?assignees=&labels=&template=bug_report.md",
        "featureRequest"   : "https://github.com/moa.is/api-awesome/issues/new?assignees=&labels=&template=feature_request.md"  
    },
    "contact": {
        "name": "Johann spuck",
        "email": "spuck@moa.com",
        "phone": "+354 864-5470"
      },                 
    "upTime"               : {
        "value"            : 99.8,
        "weekly"           :
        {
          "weekdays"       : [1,2,3,4,5],
          "from"           : "2020-04-23T17:09:00.000Z",
          "to"             : "2020-04-23T17:17:00.000Z"
        }
    },
    "responseTime"         : 200,
}
```

Xml representation example 
```xml
<?xml version="1.0" encoding="UTF-8" ?>
	<version>1.0.2</version>
	<title>Awesome service</title>
	<description>Provides access to the awesome database allowing you to query and submit methods on, how to better the world.</description>
	<access>trustedPriority,trustedEssential</access>
	<type>rest</type>
	<data>official</data>
	<data>personal</data>
	<price>usage</price>
	<price>custom</price>
	<links>
		<documentation>https://moa.is/documentation/api-awesome/v1</documentation>
		<responsibleParty>https://api-awesome/responsible</responsibleParty>
		<bugReport>https://github.com/moa.is/api-awesome/issues/new?assignees=&amp;labels=&amp;template=bug_report.md</bugReport>
		<featureRequest>https://github.com/moa.is/api-awesome/issues/new?assignees=&amp;labels=&amp;template=feature_request.md</featureRequest>
	</links>
	<contact>
		<name>Johann spuck</name>
		<email>spuck@moa.com</email>
		<phone>+354 864-5470</phone>
	</contact>
	<upTime>
		<value>99.8</value>
		<weekly>
			<weekdays>1</weekdays>
			<weekdays>2</weekdays>
			<weekdays>3</weekdays>
			<weekdays>4</weekdays>
			<weekdays>5</weekdays>
			<from>2020-04-23T17:09:00.000Z</from>
			<to>2020-04-23T17:17:00.000Z</to>
		</weekly>
	</upTime>
	<responseTime>200</responseTime>
  ```

  [Errors]: ./errors.md
  [HTTP status codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
  [Swagger]: http://swagger.io/
  [docusaurus]: https://v2.docusaurus.io/
  [NextJS + Remark]: https://github.com/vercel/next.js/tree/canary/examples/blog-starter-typescript
  [APIDOC]: https://apidocjs.com/
  [semantic versioning]: https://semver.org/
  [date string format]: https://tools.ietf.org/html/rfc3339#section-5.6
  [TechWriter]: https://techwriter.me/techwriter.aspx
  [oxygen XML Editor]: https://www.oxygenxml.com/xml_editor/wsdl_documentation.html
  [Altova XMLSpy]: https://www.altova.com/xmlspy-xml-editor/wsdl-editor
  [OpenAPI]: https://swagger.io/specification/
  [open-rpc]: https://github.com/open-rpc/open-rpc
  [DocFX]: https://dotnet.github.io/docfx/
  [Doxygen]: https://www.doxygen.nl/index.html
  [Postman]: https://www.postman.com/api-documentation-tool/
  [/info]: #info-method
  [graphql-docs]: https://www.npmjs.com/package/graphql-docs
  [graphiql]: https://github.com/graphql/graphiql