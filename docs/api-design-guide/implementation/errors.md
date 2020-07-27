# Errors
TODO
* Describe exception handling of apis
* Describe correct use of http status codes for rest services
* ...

## REST
Describe correct use of http status codes for rest services

## JSON-RPC
JSON-RPC APIs should follow the [JSON-RPC] specification, [2.0] is preferred but
[1.0] is allowed.

### Error Response
The two specifications differ on what needs to be in a error response object.
 - [1.0] The response must contain the following fields.
   - `result` - Must be null. 
   - `error` - *Should* include a [Error object].
   - `id` - Must be the same id as the request it is responding to.

- [2.0] The response must contain the following fields.  Note that the `result`
  field must not exists in a error response.
   - `jsonrpc` - Must be exactly `"2.0"`. 
   - `error` - *Must* include a [Error object].
   - `id` - Must be the same id as the request it is responding to.  If there 
     was an error in detecting the *id* in the Request object (e.g. Parse error/
     Invalid Request), it MUST be null.

#### Error object
When a rpc call encounters an error, the Response Object MUST contain the error
member with a value that is a Object with the following members:

 - `code` A Number that indicates the error type that occurred. 
   This MUST be an integer.  (see possible values: [JSON-RPC error codes])
   
 - `message` A String providing a short description of the error.
  The message SHOULD be limited to a concise single sentence.
 - `data` (*optional*) A Primitive or Structured value that contains additional 
   information about the error.  This may be omitted.

The value of this member is defined by the Server (e.g. detailed error information, nested errors etc.).
and the result field must be null JSON-RPC 1.0 object 

##### JSON-RPC error response example
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

##### JSON-RPC error codes
The error codes from and including -32768 to -32000 are reserved for pre-defined 
errors. Any code within this range, but not defined explicitly below is reserved
for future use.

| code            | message           | meaning  |
| :---            | :---              | :---     |
| 32700           | Parse error       | Invalid JSON was received by the server. An error occurred on the server while parsing the JSON text. |
| 32600	        | Invalid Request	| The JSON sent is not a valid Request object. |
| 32601	        | Method not found	| The method does not exist / is not available.|
| 32602	        | Invalid params	| Invalid method parameter(s).                 |
| 32603	        | Internal error	| Internal JSON-RPC error.                     |
| 32000 to -32099 | Server error      | Reserved for implementation-defined server-errors. |



## XML-RPC

### Fault element
When an error occurs calling a XML-RPC method a fault element should exist within the 
a XML-RPC API response.  This element should be structured with two members 
named `code` and `message`.  The `code` value should include a 32 bit integer 
value and the `message` should contain a text string describing what went wrong. 

#### Fault example
```xml
<?xml version="1.0"?>
<methodResponse>
   <fault>
      <value>
         <struct>
            <member>
               <name>code</name>
               <value><int>26</int></value>
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
### XML-RPC fault codes
[XML-RPC] protocol doesn't standardize fault codes(error codes) but the 
[XML-RPC Fault Code] specification should be followed when possible, but that is
not required.

[XML-RPC Fault Code] specification states the following:

Error codes range -32768 .. -32000 are reserved.  XML-RPC APIs should not allow
the application to set an error code within this range. 

| Code  |  message                                              | 
| ---   | :---                                                  | 
| 32700 | parse error. not well formed                          |
| 32701 | parse error. unsupported encoding                     |
| 32702 | parse error. invalid character for encoding           |
| 32600 | server error. invalid xml-rpc. not conforming to spec.|
| 32601 | server error. requested method not found              |
| 32602 | server error. invalid method parameters               |
| 32603 | server error. internal xml-rpc error                  |
| 32500 | application error                                     |
| 32400 | system error                                          |
| 32300 | transport error                                       |

In addition, the range -32099 .. -32000, is reserved for implementation defined
server errors. Server errors which do not cleanly map to a specific error 
defined by this spec should be assigned to a number in this range.



[JSON-RPC]: https://www.jsonrpc.org/specification
[2.0]: https://www.jsonrpc.org/specification
[1.0]: https://www.jsonrpc.org/specification_v1
[Error object]: #error-object.  
[JSON-RPC error codes]: #error-codes
[XML-RPC fault Code]: http://xmlrpc-epi.sourceforge.net/specs/rfc.fault_codes.php

[XML-RPC]: https://en.wikipedia.org/wiki/XML-RPC