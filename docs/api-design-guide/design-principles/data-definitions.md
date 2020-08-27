# Data Definitions and Standards
APIs should represent all texts in the [UTF-8] encoding. Attributes
representing arrays or lists should be named as plural nouns.

<!--
  Describe data transfer objects for collections to support pagination.
  {
    result: [] // collection of resource
    // pagination details
  }
 -->

## JSON
Primitive values MUST be serialized to JSON following the rules of [RFC8259] and
as stated in the standard JSON text MUST be encoded using UTF-8 [RFC3629].

JSON can represent four primitive types _strings_, _numbers_, _booleans_, and
_null_ and two structured types _objects_ and _arrays_. Concepts like
[Date and Time] need to be represented using these types.

### Response with top level JSON object
In a response body, you should return a JSON object but, not an array, as a top
level data structure to support future extensibility. This would allow you to
extend your response and for example, add server side pagination attribute at
a later time.

**Bad response body**
```
[
    { "id": "1", "name": "Einar"   },
    { "id": "2", "name": "Erlendur"},
    { "id": "3", "name": "Valdimar"}
]
```

**Good response body**
```
{
  "users":[
    { "id": "1", "name": "Einar"},
    { "id": "2", "name": "Erlendur"},
    { "id": "3", "name": "Valdimar"},
  ]
}
```

## National identifier
Icelandic individuals are uniquely identified by a national identifier called 
`kennitala`.  When referring to this identifier in URIs, requests,  or responses, 
APIs should use the name **nationalId**.  Its value is usually represented to
users on the form `######-####` but APIs should use the form `##########` at all
times.

## Language and currency
- **Languages** When specifying a language please use the [ISO-639-1]
  (two letter) standard. See: [639-1 codes].
- **Currencies** When specifying currency codes please use the [ISO-4217]
  standard. See: [4217 codes].
  - **Amount** Use the format `[0-9]+(.[0-9]+)?` to represent an amount like
    money. Separate amount and currency in different fields. Example amount:
    `1250.23`.

## Date and Time
Date and time values should be represented in a string, as described in the
[RFC3339] proposed standard. The standard defines a profile of [ISO 8601]
for use in Internet protocols. See: [Section 5.6] for Date/Time Format.

##### Summary for date and time
Date and time should be represented as a string using
the format `yyyy-MM-ddThh:mm:ss.sssZ`. Where

- **yyyy** represents year, (four-digits).
- **MM** represents month, (two-digits _01 - 12_).
- **dd** represents day of month, (two-digits _01 - 31_).
- **hh** represents hour, (two digits _00 - 24_).
- **mm** represents minute, (two digits _00 - 59_).
- **ss** represents second, (two digits _00 - 59_).
- **sss** represents a decimal fraction of a second, (one or more digits).
- **Z** represents time zone offset specified as `Z` (for [UTC]) or either
  `+` or `-` followed by a time expression `hh:mm`.

Icelandic local time can be represented with `Z` because Iceland follows
the [UTC] +00:00 all year round, which is the same as [GMT].

Examples:

- `1985-04-12T23:20:50.52Z` represents 20 minutes and 50.52 seconds after
  the 23rd hour of April 12th, 1985 in [UTC].

- `1996-12-19T16:39:57-08:00` represents 39 minutes and 57 seconds after the
  16th hour of December 19th, 1996 with an offset of -08:00 from [UTC] (Pacific
  Standard Time). Note that this is equivalent to `1996-12-20T00:39:57Z`
  in UTC.


## Data from different sources
When returning data generated from different resources, a creationTime property
should be added to the returned data.  

For example, when returning some data which contains an amount calculated using
 currency rate, a createTime should be added to the response.

[date and time]: #date-and-time
[rfc8259]: https://tools.ietf.org/html/rfc8259
[rfc3629]: https://tools.ietf.org/html/rfc3629
[utf-8]: https://en.wikipedia.org/wiki/UTF-8
[rfc3339]: https://tools.ietf.org/html/rfc3339
[section 5.6]: https://tools.ietf.org/html/rfc3339#section-5.6
[iso 8601]: https://en.wikipedia.org/wiki/ISO_8601
[utc]: https://en.wikipedia.org/wiki/Coordinated_Universal_Time
[gmt]: https://en.wikipedia.org/wiki/Greenwich_Mean_Time
[3166-1]: https://www.iso.org/iso-3166-country-codes.html
[iso-639-1]: https://www.iso.org/standard/22109.html
[639-1 codes]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
[iso-4217]: https://www.iso.org/iso-4217-currency-codes.html
[4217 codes]: https://en.wikipedia.org/wiki/ISO_4217#Active_codes
