# Testing

This document describes how an API should be tested.
The purpose of API testing is to verify that APIs exposed by your application
operate as expected.

## Different types of tests

- Unit testing — the API code unit is doing things right.
- End to End testing — tests the entire software product from beginning to end 
  to ensure the application flow behaves as expected.
- Integration testing — the integration of more than one API code units is doing
the right thing.
- Functionality testing — the API works and does exactly what it’s supposed to do.
- Reliability testing — the API can be consistently connected to and lead to
consistent results.
- Load testing — the API can handle a large amount of calls.
- Creativity testing — the API can handle being used in different ways.
- Security testing — the API has defined security requirements including
authentication, permissions and access controls. See some API security tips for
protecting vital data.
- Proficiency testing — the API increases what developers are able to do.
- API documentation testing — also called discovery testing, the API documentation
easily guides the user.
- Negative Testing — checking for every kind of wrong input the user can
possibly supply.

## API testing

Testing of provided APIs should be:

- Repeatable
- Automated
- Performed on all supported API versions.

### Repeatable tests

Create repeatable test steps, so the same test steps can be executed on the API.
The test steps should provide consistent results.

### Test automation

Consider creating automated tests to run and evaluate the outcome of the
repeatable steps by using data driven test automation tools.

### Supporting different API versions

Tests should be performed for every supported version of the API.
When a new version of an API is released, regression tests of the latest version 
of the API and all previous versions should be applied.
This ensures that legacy clients using older versions of the API don't need
to make any changes.

## Testing tools

Depending on the technology used for an API services backend, tools for testing
backend code may vary.
For the exposed API, there are a wide variety of (Open Source) tools available
for API testing:

- Jest - [Jest] is a great testing tool for unit testing JavaScript REST APIs.
- Cypress - [Cypress] is a good tool for end-to-end testing.
- SoapUI - SoapUI is the Open Source Functional Testing tool for API Testing.
It supports multiple protocols such as SOAP, REST, HTTP, JMS etc. You can
download SoapUI from https://www.soapui.org/downloads/soapui.html
- Postman - Postman is an application for interacting with HTTP APIs. It presents
you with a friendly GUI for constructing requests and reading responses.
You can download Postman from https://www.getpostman.com/
- cURL - cURL is a tool for working with URLs. cURL lets you query a URL from the
command line. It lets you post form data. With cURL you can try out new APIs easily.
You can download cURL from the command line on Linux by typing
`sudo yum install curl`
- Apache benchmark - The ApacheBench tool (ab) can load test servers by sending
an arbitrary number of concurrent requests. You can download the Apache benchmark
from the command line on Linux by typing `yum install httpd-tools`
- Swagger – The Swagger editor can be used to validate your Swagger definition
prior to importing it into an API Manager.

There are a lot of other test tools available, the list above is not final.  

For REST APIs, we recommend using [Jest] for unit 
testing and [Cypress] for end-to-end testing.

#### References

- [Australian Government: Testing](https://api.gov.au/standards/national_api_standards/testing.html)
- [UK Government: Writing API reference documentation, Testing documentation](https://www.gov.uk/guidance/writing-api-reference-documentation#testing-your-documentation)
- [SoapUI: API Functional Testing Best Practices](https://www.soapui.org/learn/functional-testing/)
- [SoapUI: API Testing 101: Learn the basics](https://www.soapui.org/learn/functional-testing/api-testing-101/)


[Jest]: https://jestjs.io/
[Cypress]: https://www.cypress.io/
