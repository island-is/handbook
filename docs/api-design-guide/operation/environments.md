# Environments

This document describes different environments and their purpose.

- Development Environment -
- Test Environment (for Providers of API) -
- Sandbox Environment (for Consumers of API) -
- Production Environment -

## Development Environment

The Development Environment used to develop API's should contain set of processes and programing tools to develop functional API.
The developed assets should be connected to revision control and build process to create functional API. The functional API can then be deployed to other test and production environments.

## Test Environment (for Providers of API)

The purpose of the test environment is to exercise new and changed code via either automated checks or non-automated techniques.
This is to validate that the functionality of provided API is correct before moving it to production and sandbox.

This environment is not used for consumers of the API, only the provider.

## Sandbox Environment (for Consumer of API)

The purpose of the sandbox environment is for consumer / subscribers of API to test and develop applications using this API.
Consumer can then test their application against supported version of the API.

Data used for API in consumer test environment can be either Production Test Data or Synthetic data.

### Synthetic test data

Synthetic test data does not use any actual data from the production data store and sources. It is artificial data based on the data model for that database.
Synthetic test data can be generated automatically by a synthetic test data generation.

### Production test data

Production test data is a copy of a production database that has been masked, or obfuscated, and subsetted to represent a portion of the database that is relevant to test the API.

## Production Environment

The live system hosting the API. Consumer of API uses this environment to call API's with live authentication and actual data.

There are lots of other test tools available, list above is not final.

#### References

- [Software Testing News: When to use production vs. synthetic data for software testing](https://www.softwaretestingnews.co.uk/when-to-use-production-vs-synthetic-data-for-software-testing)
