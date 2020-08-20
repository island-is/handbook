# Documentation
API documentation should be targeted for the developer that will consume your
API.  A good documentation is one of the single most important quality of an 
a API.  It makes it much easier for other developers to use services and 
reduces significantly implementation time for API consumers. The API developer 
is responsible for keeping it up to date.

To help with keeping documentation up to date consider using automatic 
generation tools.

**Note** - To be able to register a **REST** service to *Viskuausan* 
the service **MUST** provide a [OPENAPI 3] service description.  
Here you can see an [example] about such description.

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
 - Create example codes on how to call a get `/ping` method in your service.
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
Use [OPENAPI 3] specification to describe *REST* services.
Tools like [Swagger] and [Swagger-editor] can help with the documentation.

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

  [Errors]: ./errors.md
  [HTTP status codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
  [Swagger]: http://swagger.io/
  [Swagger-editor]: https://editor.swagger.io/
  [example]: https://github.com/nordic-institute/X-Road/blob/0d0a65663daa8f3a94a4993d7948d4655d31b376/doc/Protocols/pr-rest_x-road_message_protocol_for_rest.md#appendix-1-example-service-definition
  [docusaurus]: https://v2.docusaurus.io/
  [NextJS + Remark]: https://github.com/vercel/next.js/tree/canary/examples/blog-starter-typescript
  [APIDOC]: https://apidocjs.com/
  [semantic versioning]: https://semver.org/
  [TechWriter]: https://techwriter.me/techwriter.aspx
  [oxygen XML Editor]: https://www.oxygenxml.com/xml_editor/wsdl_documentation.html
  [Altova XMLSpy]: https://www.altova.com/xmlspy-xml-editor/wsdl-editor
  [OPENAPI 3]: https://swagger.io/specification/
  [DocFX]: https://dotnet.github.io/docfx/
  [Doxygen]: https://www.doxygen.nl/index.html
  [Postman]: https://www.postman.com/api-documentation-tool/
    [graphql-docs]: https://www.npmjs.com/package/graphql-docs
  [graphiql]: https://github.com/graphql/graphiql
  [date and time]: ../design-principles/data-definitions.md#date-and-time