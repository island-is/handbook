# Error Handling
This document describes how REST APIs should present errors to clients 
consuming these services.

When a error occurs in a API, the service should return the error to the calling
client in a informative and structured manner. The API should return
information about the error in the body part of a response.

## HTTP status codes
APIs services MUST respond with a [HTTP status code] 
in a response to every request.

These are the recommended error status codes to use for REST APIs.

| Code | Meaning                                                                                        |
| :--- | :--------------------------------------------------------------------------------------------- |
| 400  | **Bad Request** — The request is malformed, or don’t pass validation. Used with GET, POST, PUT |
| 401  | **Unauthorized** — No authentication credentials provided or credentials are invalid.          |
| 403  | **Forbidden** — Authenticated user is not authorized to access the resource                    |
| 404  | **Not Found** — The requested resource was not found                                           |

## Response body
When errors occur in a REST API, add additional information 
about the errors to the body part of the returned response.

When an error occurs, a REST API should respond with a [HTTP status code] and
the response should contain a error object described below.

### Error object
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