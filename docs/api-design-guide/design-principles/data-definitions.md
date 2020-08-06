# Data Definitions
TODO
* Describe how to define data definitions (schemas)
* What rules apply? Reference to applicable naming conventions
  (write them if the don't exists)
* Articles:
    - https://restful-api-design.readthedocs.io/en/latest/resources.html#resource-data
    - https://swagger.io/specification/#data-types

APIs should represent all texts in the [UTF-8] encoding.

## JSON
Primitive values MUST be serialized to JSON following the rules of [RFC8259] and
as stated in the standard JSON text MUST be encoded using UTF-8 [RFC3629].

JSON can represent four primitive types (strings, numbers, booleans, and null) 
and two structured types (objects and arrays).  Because of this concepts like
date and time needs to be represented using these types.  Below you can find
these additional representations. 

## Date and Time
Date and time values should be represented as described in the [RFC3339] 
proposed standard.  The standard defines a profile of [ISO 8601] for use in Internet protocols.  See: [Section 5.6] for Date/Time Format.

TODO:fix
 - used for /info object: [w3.org](https://www.w3.org/TR/NOTE-datetime)
 - alternitve Date Time String Format [ecma](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15)







[RFC8259]: https://tools.ietf.org/html/rfc8259
[RFC3629]: https://tools.ietf.org/html/rfc3629
[UTF-8]: https://en.wikipedia.org/wiki/UTF-8
[RFC3339]: https://tools.ietf.org/html/rfc3339
[section 5.6]: https://tools.ietf.org/html/rfc3339#section-5.6
[ISO 8601]: https://en.wikipedia.org/wiki/ISO_8601