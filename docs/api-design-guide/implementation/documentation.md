# Documentation
API documentation should be targeted towards the developer that will consume your
API. A good documentation is one of the single most important quality of an API.
It makes it much easier for other developers to use services and significantly
reduces implementation time for API consumers. The API developer is responsible
for keeping the documentation up to date.

To help with keeping documentation up to date consider using automatic 
generation tools.

**Note** - To be able to register a **REST** service to *Viskuausan* 
the service **MUST** provide an [OPENAPI 3] service description.

The following fields are required for services to be automatically imported to _Viskuausan_

- info
  - description — short but proper description of the API.
  - version — to distinguish API versions following [semantic versioning]
    specification.
  - title — descriptive name of the API.
  - contact — quick information, who to contact when an issue about the service arises.
    - name — of the person or a department.
    - email — fully qualified email.
  - x-access — (*comma separated list*) Who can use this service.
    Possible values: `open`, `islykill`, `trusted`, `trustedPriority`,
    `trustedEssential`.
  - x-dataCategory — (*comma separated list*) What kind of data does this 
    service work with. Possible values: `open`, `official`,`personal`,`health`,
    `financial`.
  - x-pricing —  (*comma separated list*) Cost of using this service.  
    Possible values:  `free`,`usage`,`daly`,`monthly`,`yearly`,`custom`.
  - x-links — Links regarding the service
    - responsibleParty — a fully qualified url to a online page containing
      information about the responsible party/owner of the service.
    - documentation —  (*Optional*) a fully qualified url to the API 
       documentation page.
    - bugReport (*Optional*) — a fully qualified url to a online page or 
      form a consumer can report bugs about the service.
    - featureRequest (*Optional*) — a fully qualified url to a online page
      or form a consumer can ask for a new feature in api service.

## Example

```
openapi: 3.0.3
servers:
  - url: https://development.my-service.island.is
    description: Development server
  - url: https://staging.my-service.island.is
    description: Staging server
  - url: https://production.my-service.island.is
    description: Production server
info:
  description: |-
    This is a sample OpenAPI 3.0 for Digital Iceland.
  version: 0.0.1
  title: Digital Iceland - OpenAPI 3.0
  termsOfService: ""
  contact:
    name: Digital Iceland
    url: https://stafraent.island.is/
    email: stafraentisland@fjr.is
  license:
    name: MIT
    url: "https://opensource.org/licenses/MIT"
  x-dataAccess: free
  x-dataCategory:
    - personal
  x-links:
    documentation: "https://docs.my-service.island.is"
    responsibleParty: "https://my-service.island.is/responsible"
    bugReport: "https://github.com/island-is/handbook/issues/new?assignees=&labels=&template=bug_report.md"
    featureRequest: "https://github.com/island-is/handbook/issues/new?assignees=&labels=&template=feature_request.md"
paths:
  /individuals:
    get:
      description: |
        Returns all individuals registered
      operationId: getIndividuals
      parameters:
        - name: dateOfBirth
          in: query
          description: Find all individuals born after set date
          required: false
          schema:
            type: string
            format: date
      responses:
        "200":
          description: |
            Returns an array of individuals, either it returns all individuals or individuals born after a specific date
          content:
            application/json:
              schema:
                type: object
                properties:
                  individuals:
                    type: array
                    items:
                      $ref : "#/components/schemas/Individual"
        "400":
          $ref: "#/components/responses/BadRequest"
        "500":
          $ref: "#/components/responses/InternalServerError"
        default:
          description: Unexpected error
          content:
            application/json:
              schema:
                type: object
                properties:
                  error:
                    $ref: "#/components/schemas/Error"
  /individuals/{id}:
    get:
      description: |
        Returns individual based on a single ID
      operationId: getIndividual
      parameters:
        - name: id
          in: path
          description: UUID of an individual
          required: true
          schema:
            type: string
            format: UUID
      responses:
        "200":
          description: |
            Returns an individual with a specific id
          content:
            application/json:
              schema:
                type: object
                properties:
                  individuals:
                    type: array
                    items:
                      $ref : "#/components/schemas/Individual"
        "400":
          $ref: "#/components/responses/BadRequest"
        "404":
          $ref: "#/components/responses/NotFound"
        "500":
          $ref: "#/components/responses/BadRequest"
components:
  responses:
    BadRequest:
      description: Bad request
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                $ref: '#/components/schemas/Error'
    Unauthorized:
      description: Unauthorized
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                $ref: '#/components/schemas/Error'
    NotFound:
      description: The specified resource was not found
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                $ref: '#/components/schemas/Error'
    InternalServerError:
      description: The specified resource was not found
      content:
        application/json:
          schema:
            type: object
            properties:
              error:
                $ref: '#/components/schemas/Error'
  schemas:
    Individual:
      type: object
      properties:
        id:
          type: string
          description: Unique UUID
          format: UUID
        nationalId:
          type: string
          minLength: 12
          maxLength: 12
          pattern: '^\d{12}$'
          description: National security number
        firstName:
          type: string
          minLength: 1
          maxLength: 250
          description: First name and middle name
        lastName:
          type: string
          minLength: 1
          maxLength: 250
          description: Last name
        dateOfBirth:
          type: string
          format: date-time
          description: UTC date of birth
      example:
        id: "BA84DAF1-DE55-40A8-BF35-8A76C7F936F6"
        nationalId: "160108117573"
        firstName: "Quyn G."
        lastName: "Rice"
        dateOfBirth: "2019-03-29T18:00:58.000Z"
        address: "377-8970 Vitae Rd."
    Error:
      type: object
      required:
        - code
        - message
      properties:
        code:
          type: integer
        message:
          type: string
        errors:
          type: array
          items:
            $ref: "#/components/schemas/ErrorDetail"
      example:
        code: 400
        message: "Bad request"
        errors:
          - code: 87
            message: "Parameter is incorrectly formatted"
            help: "https://www.moa.is/awesome/documetation/devices"
            trackingId: "5d17a8ada52a2327f02c6a1a"
            param: "deviceId"
          - code: 85
            message: Parameter missing
            help: 'https://www.moa.is/awesome/documetation/devices'
    ErrorDetail:
      type: object
      required:
        - message
      properties:
        code:
          type: integer
        message:
          type: string
        help:
          type: string
        trackingId:
          type: string
        param:
          type: string
```
## Consider using markdown
Markdown is recommended, but not required when writing documentation about an
API service. You could use a tool like [docusaurus] or [NextJS + Remark]
to make your markdown documents searchable and more accessible.

When documenting with markdown try to keep text lines no longer than 80 
characters for easier reading when markdown documents are read from text 
editors. Editors often support showing you the 80 line character limit. For
example, in VS Code, you can add `"editor.rulers": [80]` to your 
preferences -> settings to make it show this limit.

## Write examples
The quickest way for a consumer to learn from documentation is from example
codes. You should figure out which programming languages are mostly used by
the API consumers and give examples for those languages.

Consider creating a **Getting Started** document where you can describe
how a client can start using your service.

Something to consider for a Getting Started page:
- Who to contact to get access, give:
  - a link to an application form or
  - email or
  - who to call to get access to your service.
- Describe if a client will need to authenticate himself.
  - Will he need to be issued a certificate?
  - Will he need to apply for a user and password?
- Create example codes on how to call a get `/ping` method in your service.
  - Create a Node.js example.
  - Create a Microsoft .NET Core example.
  - Create examples for other frameworks your current clients are using or other
    common frameworks.

### Example requests and responses
An automatic generation tool like [Swagger] could help with these examples, 
but its automatic generation is not always enough. A good practice would be to
provide a table for describing elements or properties that need further 
explanation.

If a request or response supports multiple representations, such as HTTP, XML, 
and JSON a good practice would be to show examples for at least these three.

When you use tables you will need to provide links to other tables for nested 
elements or objects. When this is the case (for simple objects/elements), you
could also provide the the description as a list allowing you to intend for each 
element or object.

#### Here is an example of a table describing elements in a request or a response

| Name    | Type   | Description                         | Remarks                                                |
| :------ | :----- | :---------------------------------- | :----------------------------------------------------- |
| name    | String | Name of the person                  | Max length is 32 characters                            |
| age     | Number | How many years has the person lived | A child can be of 0 age but age will never be negative |
| address | String | Location where the person lives     | Max length is 36 characters                            |

## Describe error handling
Describe how your application handles errors. Provide information on which 
[HTTP status codes] a client consuming your service can expect the API to 
return, and provide information on application defined errors and how the errors 
are presented to clients. See [Errors] for recommendations.

## Provide feedback mechanism
Provide users with a way to comment on your documentation. This will help 
with finding concepts that need further explanation and keeping the 
documentation up to date.

## Automatic documentation generation 
Using tools for Automatic documentation generation will help API developers
maintain and keep the documentation up to date. API consumers will also benefit 
with structured and readable documentation.

Use the [OPENAPI 3] specification to describe *REST* services.
Tools like [Swagger] and [Swagger Editor] can help with the documentation.

[errors]: ./errors.md
[http status codes]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
[Swagger]: http://swagger.io/
[Swagger Editor]: https://editor.swagger.io/
[example]: https://github.com/nordic-institute/X-Road/blob/0d0a65663daa8f3a94a4993d7948d4655d31b376/doc/Protocols/pr-rest_x-road_message_protocol_for_rest.md#appendix-1-example-service-definition
[docusaurus]: https://v2.docusaurus.io/
[NextJS + Remark]: https://github.com/vercel/next.js/tree/canary/examples/
[apidoc]: https://apidocjs.com/
[openapi 3]: https://swagger.io/specification/
[postman]: https://www.postman.com/api-documentation-tool/
[date and time]: ../design-principles/data-definitions.md#date-and-time
[semantic versioning]: https://semver.org/
