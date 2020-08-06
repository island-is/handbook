# Error Handling

This document describes how [REST], [SOAP], [JSON-RPC] and [XML-RPC] APIs should
present errors to clients consuming these services.

When a error occurs in a API, the service should return the error to the calling
client in a informative and structured manner. The API should return
information about the error in the body part of a response.

## HTTP status codes

**[SOAP] over http** APIs MUST always return the http status code **500** -
_Internal Server Error_ when errors occur.

**[REST]** APIs services MUST respond with a [HTTP status code] in a response
to every request.

These are the recommended error status codes to use for REST APIs.

| Code | Meaning                                                                                        |
| :--- | :--------------------------------------------------------------------------------------------- |
| 400  | **Bad Request** — The request is malformed, or don’t pass validation. Used with GET, POST, PUT |
| 401  | **Unauthorized** — No authentication credentials provided or credentials are invalid.          |
| 403  | **Forbidden** — Authenticated user is not authorized to access the resource                    |
| 404  | **Not Found** — The requested resource was not found                                           |

### Response body

When errors occur in a [SOAP] or an [REST] API add additional information about
the errors to the body part of the returned response.

## REST

When an error occurs, a REST API should respond with a [HTTP status code]s and
the response should contain a [REST error object].

### REST error object

This object should be in a REST API response when an error occurs. The response
should contain the key `error` and it's value should be a json object containing
at least the two keys, `code` and `message`. If there were multiple errors, the
values of `code` and `message` should contain the values describing the first
error.

- `error` The key of the error object
  - `code` _(Number)_ A integer number that indicates the error type that
    occurred. This field value will usually represent the HTTP response code.
  - `message` _(String)_ A human readable string providing more details about the error.
  - `errors` _(Array)_ **(Optional)** A more detailed information about the
    error(s). API developers can structure each object in the array as they
    like, but should when ever possible, use that structure through out the
    application. For example, the following fields in each object of the
    array could be included.
    - `help` **(Optional)** Url to a page explaining the error and possible
      solutions.
    - `trackingId` **(Optional)** Identifier for mapping failures to service
      internal codes.
    - `param` **(Optional)** Name of the parameter which was incorrect.
    - `code` and `message` **(Optional)** could provide more detailed
      information about a specific error, like when parsing parameters.

#### REST error response examples

A simple response

```json
{
  "error": {
    "code": 404,
    "message": "File Not Found"
  }
}
```

More detailed response

```json
{
  "error": {
    "code": 400,
    "message": "Bad Request - parameter incorrect",
    "errors": [
      {
        "code": 87,
        "message": "Parameter is incorrectly formatted",
        "help": "https://www.moa.is/awesome/documetation/devices",
        "trackingId": "5d17a8ada52a2327f02c6a1a",
        "param": "deviceId"
      },
      {
        "code": 85,
        "message": "Parameter missing",
        "help": "https://www.moa.is/awesome/documetation/devices",
        "trackingId": "5d17a8ada52a2327f02c6a1c",
        "param": "deviceName"
      }
    ]
  }
}
```

## SOAP

**SOAP over http** is here after referrer to as SOAP.

In case of a SOAP error while processing the request, the SOAP HTTP server MUST
issue an HTTP 500 "Internal Server Error" response and include a SOAP message in
the response containing a [SOAP 1.1 Fault Element] or a [SOAP 1.2 Fault Element]
indicating the SOAP processing error.

### SOAP 1.1 Fault Element

According to the specification a [SOAP 1.1 Fault] element should be returned in
the body part of a response when a error occurs.

The Fault element must have the following sub-elements

- `faultCode` It is a text code used to indicate a class of errors. The
  predefined fault codes are:
  - `SOAP-ENV:VersionMismatch` Found an invalid namespace for the SOAP
    Envelope element.
  - `SOAP-ENV:MustUnderstand` An immediate child element of the Header element,
    with the mustUnderstand attribute set to "1", was not understood.
  - `SOAP-ENV:Client` The message was incorrectly formed or contained
    incorrect information.
  - `SOAP-ENV:Server` There was a problem with the server, so the message
    could not proceed.
- `faultString` It is a text message explaining the error.
- `faultActor` It is a text string indicating who caused the fault. It is
  useful if the SOAP message travels through several nodes in the SOAP message
  path, and the client needs to know which node caused the error. A node that
  does not act as the ultimate destination must include a faultActor element.
- `detail` It is an element used to carry application-specific error messages.
  The detail element can contain child elements called detail entries.

### SOAP 1.2 Fault Element

According to the specification a [SOAP 1.2 Fault] element should be returned in
the body part of a response when a error occurs.

The Fault element has the following sub-elements:

- `Code` [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultcodeelement)
  - `Value` [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultvalueelement)
    is one of the SOAP Fault Codes defined
    in [this table](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#tabsoapfaultcodes)
    of the standard.
  - `Subcode` _(Optional)_ [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultsubcodeelement)
    - `value` [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultsubvalueelem)
      an application defined subcategory of the value of the Value child
      element. Format: `xs:QName`.
    - `Subcode` _(Optional)_ (Same as above)
- `Reason` [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultstringelement)
  is intended to provide a human-readable explanation of the fault. `Reason`
  has one or more `Text` elements.
  - `Text` [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#reasontextelement)
    intended to carry the text of a human-readable explanation of the fault.
- `Node` _(Optional)_ [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultactorelement) intended to provide information about which SOAP node on the SOAP message path caused the fault to happen.
- `Role` _(Optional)_ [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultroleelement) identifies the role the node was operating in at the point the fault occurred.
- `Detail` _(Optional)_ [Element](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#faultdetailelement)
  is intended for carrying application specific error information. The Detail
  element information item MAY have any number of character information item
  children.

#### SOAP 1.1 Fault Example

The client has requested a method named ValidateCreditCard, but the service does
not support such a method. This represents a client request error, and the
server returns the following SOAP response.

```xml
<?xml version = '1.0' encoding = 'UTF-8'?>
<SOAP-ENV:Envelope
   xmlns:SOAP-ENV = "http://schemas.xmlsoap.org/soap/envelope/"
   xmlns:xsi = "http://www.w3.org/1999/XMLSchema-instance"
   xmlns:xsd = "http://www.w3.org/1999/XMLSchema">

   <SOAP-ENV:Body>
      <SOAP-ENV:Fault>
         <faultcode xsi:type = "xsd:string">SOAP-ENV:Client</faultcode>
         <faultstring xsi:type = "xsd:string">
            Failed to locate method (ValidateCreditCard) in class (examplesCreditCard) at
               /usr/local/ActivePerl-5.6/lib/site_perl/5.6.0/SOAP/Lite.pm line 1555.
         </faultstring>
      </SOAP-ENV:Fault>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### SOAP 1.2 Fault Response Example A

```xml
<?xml version="1.0"?>
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope"
              xmlns:enc="http://www.w3.org/2003/05/soap-encoding">
  <env:Body>
    <env:Fault>
      <env:Code>
        <env:Value>env:Sender</env:Value>
        <env:Subcode>
          <env:Value>enc:MissingID</env:Value>
        </env:Subcode>
      </env:Code>
      <env:Reason>
        <env:Text xml:lang="en-US">
          Violation of id and ref information items
        </env:Text>
      </env:Reason>
      <env:detail>
        A ref attribute information item and an id attribute information
        item MUST NOT appear on the same element information item.
      </env:detail>
    </env:Fault>
 </env:Body>
</env:Envelope>
```

#### SOAP 1.2 Fault Response Example B

```xml
<?xml version="1.0" ?>
<env:Envelope xmlns:env="http://www.w3.org/2003/05/soap-envelope">
  <env:Body>
    <env:Fault>
      <env:Code>
        <env:Value xmlns:ns1="http://www.w3.org/2003/05/soap-envelope">
          ns:Sender
        </env:Value>
        <env:Subcode>
          <env:Value xmlns:ns2="http://www.w3.org/2003/05/soap-rpc">
            ns:BadArguments
          </env:Value>
        </env:Subcode>
      </env:Code>
      <env:Reason>
        <env:Text xml:lang="en">Missing parameter.</env:Text>
      </env:Reason>
    </env:Fault>
  </env:Body>
</env:Envelope>
```

## JSON-RPC

According to the [JSON-RPC specification], error code should be in a response
message. Http server should respond with status code 200, even if there is an
error and therefore clients consuming the service will need to handle errors
with that in mind.

JSON-RPC APIs should follow the preferred JSON-RPC [2.0] specification, but
[1.0] is allowed.

### Error Response

The two specifications differ on what needs to be in a error response object.

- [1.0] The response must contain the following fields.

  - `result` - Must be null.
  - `error` - _Should_ include a [Error object].
  - `id` - Must be the same id as the request it is responding to.

- [2.0] The response must contain the following fields. Note that the `result`
  field must not exists in a error response.
  - `jsonrpc` - Must be exactly `"2.0"`.
  - `error` - _Must_ include a [Error object].
  - `id` - Must be the same id as the request it is responding to. If there
    was an error in detecting the _id_ in the Request object (e.g. Parse error/
    Invalid Request), it MUST be null.

#### Error object

When a rpc call encounters an error, the Response Object MUST contain the
`error` member with a value that is a Object, with the following members:

- `code` _(Number)_ that indicates the error type that occurred.
  This MUST be an integer. (see possible values: [JSON-RPC error codes])

- `message` _(String)_ providing a short description of the error.
  The message SHOULD be limited to a concise single sentence.
- `data` **(Optional)** A Primitive or Structured value that contains additional
  information about the error. The value of this member is defined by the
  Server (e.g. detailed error information, nested errors etc.).

If the API is a JSON-RPC [1.0] service the response must include a `result`
member and it's value must be `null`.

##### JSON-RPC error codes

The error codes from and including -32768 to -32000 are reserved for pre-defined
errors. Any code within this range, but not defined explicitly below is reserved
for future use.

| code            | message          | meaning                                                                                               |
| :-------------- | :--------------- | :---------------------------------------------------------------------------------------------------- |
| 32700           | Parse error      | Invalid JSON was received by the server. An error occurred on the server while parsing the JSON text. |
| 32600           | Invalid Request  | The JSON sent is not a valid Request object.                                                          |
| 32601           | Method not found | The method does not exist / is not available.                                                         |
| 32602           | Invalid params   | Invalid method parameter(s).                                                                          |
| 32603           | Internal error   | Internal JSON-RPC error.                                                                              |
| 32000 to -32099 | Server error     | Reserved for implementation-defined server-errors.                                                    |

##### JSON-RPC error response example

This is a example where an API is returning an error after an unsuccessful
execution of a response from a client.

```json
{
    "jsonrpc": "2.0",
    "error": {
            "code": -32601,
            "message": "Method not found"},
            "id": "1"
    }
}
```

## XML-RPC

When an error occurs calling a [XML-RPC](https://en.wikipedia.org/wiki/XML-RPC)
method a fault element should exist within the a XML-RPC API response.

### Fault element

This element should include the two member elements named `code` and `message`.

- `code` should include a 32 bit integer _fault code_ value and the
- `message` should contain a text string describing what went wrong.

### XML-RPC fault codes

XML-RPC protocol doesn't standardize fault codes(error codes) but the
[XML-RPC Fault Code] specification should be followed when possible.

[XML-RPC Fault Code] specification states the following:

Error codes range -32768 .. -32000 are reserved. XML-RPC APIs should not allow
the application to set an error code within this range.

| Code  | message                                                |
| ----- | :----------------------------------------------------- |
| 32700 | parse error. not well formed.                          |
| 32701 | parse error. unsupported encoding.                     |
| 32702 | parse error. invalid character for encoding.           |
| 32600 | server error. invalid xml-rpc. not conforming to spec. |
| 32601 | server error. requested method not found.              |
| 32602 | server error. invalid method parameters.               |
| 32603 | server error. internal xml-rpc error.                  |
| 32500 | application error.                                     |
| 32400 | system error.                                          |
| 32300 | transport error.                                       |

In addition, the range -32099 .. -32000, is reserved for implementation defined
server errors. Server errors which do not cleanly map to a specific error
defined by this spec should be assigned to a number in this range.

#### XML-RPC error response example

This is a example where an API is returning an error after an unsuccessful
execution of a response from a client.

```xml
<?xml version="1.0"?>
<methodResponse>
    <fault>
        <value>
            <struct>
                <member>
                    <name>code</name>
                    <value><int>32601</int></value>
                </member>

                <member>
                    <name>message</name>
                    <value><string>No such method!</string></value>
                </member>

            </struct>
        </value>
    </fault>
</methodResponse>
```

[rfc-2616]: https://www.ietf.org/rfc/rfc2616.txt
[json-rpc specification]: https://www.jsonrpc.org/specification
[2.0]: https://www.jsonrpc.org/specification
[1.0]: https://www.jsonrpc.org/specification_v1
[error object]: #error-object
[rest]: #rest
[soap]: #soap
[soap 1.1 fault]: https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383507
[soap 1.2 fault]: https://www.w3.org/TR/2007/REC-soap12-part1-20070427/#soapfault
[soap 1.1 fault element]: #soap-11-fault-element
[soap 1.2 fault element]: #soap-12-fault-element
[json-rpc error codes]: #error-codes
[xml-rpc fault code]: http://xmlrpc-epi.sourceforge.net/specs/rfc.fault_codes.php
[json-rpc]: #json-rpc
[xml-rpc]: #xml-rpc
[rest error object]: #rest-error-object
[http status code]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes
[soap protocol 1.1]: https://www.w3.org/TR/2000/NOTE-SOAP-20000508
