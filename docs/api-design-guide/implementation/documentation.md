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

When you use tables you will need to provided links to other tables for nested 
elements/object.  When this is the case (for simple objects/elements), you could
also provide the the description as a list allowing you to intent for each 
element/object.

#### Here is a example of a table describing elements in a request or a response
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


## APIs must provide information object about the service
For API management all APIs should implement a GET `/info` method which should
provide a API information object.   The API Catalog (Viskuausan) uses this
method when listing available services at island.is.

The returned object should provide the fields:
 - **version**  (*String*) to distinguish API versions following 
   [semantic versioning](https://semver.org/) specification.
 - **title** (*String*) as (unique) identifying, functional descriptive name of the API.
 - **description** (*String*) containing a short but proper description of the API.
 - **access** (*List of String*) Who can have access to the service.  Possible
   string values are `open`, `islykill`, `trusted`, `trustedPriority` and
   `trustedEssential`.
 - **type** (*String*) What kind of a service is this? Possible values:
   `rest`,`graphql`,`json-rpc`,`xml-rpc`,`soap` or something else not mentioned here.
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
         promise made [date string w3 format](https://www.w3.org/TR/NOTE-datetime).
       - **to** what time during each day will the service upTime promise stop 
         [date string w3 format](https://www.w3.org/TR/NOTE-datetime).
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

Json representation
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

Xml representation
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