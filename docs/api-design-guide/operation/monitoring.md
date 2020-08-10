# Monitoring

This document describes logging and monitoring for API services

## Logging

The following is based on best practice in logging from OWASP Foundation.
Insufficient logging and monitoring is one of top 10 API security vulnerability’s in 2019 version.

### Logging mechanism

Use standard and easily configured logging framework.
It is preferred to have specific data source to store log events.
Ensure low latency on logging functions.
Log data should be generated in a format suitable for centralized log management.

### Log Events

The level and content of security monitoring, alerting and reporting needs to be set during the requirements and design stage of projects, and should be proportionate to the information security risks. This can then be used to define what should be logged.

There is no one size fits all solution, and a blind checklist approach can lead to unnecessary "alarm fog" that means real problems go undetected.

Where possible, always log:

- Input validation failures e.g. protocol violations, unacceptable encodings, invalid parameter names and values
- Output validation failures e.g. database record set mismatch, invalid data encoding
- Authentication successes and failures
- Authorization (access control) failures
- Session management failures e.g. cookie session identification value modification
- Application errors and system events e.g. syntax and runtime errors, connectivity problems, performance issues, third party service error messages, file system errors, file upload virus detection, configuration changes
- Application and related systems start-ups and shut-downs, and logging initialization (starting, stopping or pausing)
- Use of higher-risk functionality e.g. network connections, addition or deletion of users, changes to privileges, assigning users to tokens, adding or deleting tokens, use of systems administrative privileges, access by application administrators, all actions by users with administrative privileges, access to payment cardholder data, use of data encrypting keys, key changes, creation and deletion of system-level objects, data import and export including screen-based reports, submission of user-generated content - especially file uploads
- Legal and other opt-ins e.g. permissions for mobile phone capabilities, terms of use, terms & conditions, personal data usage consent, permission to receive marketing communications

Optionally consider if the following events can be logged and whether it is desirable information:

- Sequencing failure
- Excessive use
- Data changes
- Fraud and other criminal activities
- Suspicious, unacceptable or unexpected behavior
- Modifications to configuration
- Application code file and/or memory changes

### Attributes on Log Event

Each log entry needs to include sufficient information for the intended subsequent monitoring and analysis. It could be full content data, but is more likely to be an extract or just summary properties.

The application logs must record "when, where, who and what" for each event.

The properties for these will be different depending on the architecture, class of application and host system/device, but often include the following:

- When
  _ Log date and time (international format)
  _ Event date and time - the event timestamp may be different to the time of logging e.g. server logging where the client application is hosted on remote device that is only periodically or intermittently online \* Interaction identifier Note A
- Where
  _ Application identifier e.g. name and version
  _ Application address e.g. cluster/hostname or server IPv4 or IPv6 address and port number, workstation identity, local device identifier
  _ Service e.g. name and protocol
  _ Geolocation \* Code location e.g. script name, module name
- Who (human or machine user)
  _ Source address e.g. user's device/machine identifier, user's IP address, cell/RF tower ID, mobile telephone number
  _ User identity (if authenticated or otherwise known) e.g. user database table primary key value, user name, license number
- What
  _ Type of event Note B
  _ Severity of event (See logging levels below)
  _ Security relevant event flag (if the logs contain non-security event data too)
  _ Description

Additionally, consider recording:

- Secondary time source (e.g. GPS) event date and time
- Action - original intended purpose of the request e.g. Log in, Refresh session ID, Log out, Update profile
- Object e.g. the affected component or other object (user account, data resource, file) e.g. URL, Session ID, User account, File
- Result status - whether the ACTION aimed at the OBJECT was successful e.g. Success, Fail, Defer
- Reason - why the status above occurred e.g. User not authenticated in database check ..., Incorrect credentials
- HTTP Status Code - the status code returned to the user (often 200 or 301)
- Request HTTP headers or HTTP User Agent
- User type classification e.g. public, authenticated user, CMS user, search engine, authorized penetration tester, uptime monitor (see "Data to exclude" below)
- Analytical confidence in the event detection Note B e.g. low, medium, high or a numeric value
- Responses seen by the user and/or taken by the application e.g. status code, custom text messages, session termination, administrator alerts
- Extended details e.g. stack trace, system error messages, debug information, HTTP request body, HTTP response headers and body
- Internal classifications e.g. responsibility, compliance references
- External classifications e.g. NIST Security Content Automation Protocol (SCAP), Mitre Common Attack Pattern Enumeration and Classification (CAPEC)

### Data to exclude

Never log data unless it is legally sanctioned. For example intercepting some communications, monitoring employees, and collecting some data without consent may all be illegal.

Never exclude any events from "known" users such as other internal systems, "trusted" third parties, search engine robots, uptime/process and other remote monitoring systems, pen testers, auditors. However, you may want to include a classification flag for each of these in the recorded data.

The following should not usually be recorded directly in the logs, but instead should be removed, masked, sanitized, hashed or encrypted:

- Application source code
- Session identification values (consider replacing with a hashed value if needed to track session specific events)
- Access tokens
- Sensitive personal data and some forms of personally identifiable information (PII) e.g. health, government identifiers, vulnerable people
- Authentication passwords
- Database connection strings
- Encryption keys and other master secrets
- Bank account or payment card holder data
- Data of a higher security classification than the logging system is allowed to store
- Commercially-sensitive information
- Information it is illegal to collect in the relevant jurisdictions
- Information a user has opted out of collection, or not consented to e.g. use of do not track, or where consent to collect has expired

Sometimes the following data can also exist, and whilst useful for subsequent investigation, it may also need to be treated in some special manner before the event is recorded:

- File paths
- Database connection strings
- Internal network names and addresses
- Non sensitive personal data (e.g. personal names, telephone numbers, email addresses)
- Consider using personal data de-identification techniques such as deletion, scrambling or pseudonymization of direct and indirect identifiers where the individual's identity is not required, or the risk is considered too great.

In some systems, sanitization can be undertaken post log collection, and prior to log display.

### Logging levels

Common log types are Informational, Verbose, Warning and Error. It should be configurable if Verbose logging is on or off.

#### Informational (Info)

Record the general information talks about the progress and flow of the process.
For instance, Start/stop of service, intermediate checkpoints, etc. This type should be default ON into Production systems.

#### Verbose

More than general information which records granular steps. For instance, each iteration of for loops with different parameters logged, any other system information which is only needed in specific scenarios. This type of log is not recommended to keep ON.
This should be enabled only in certain circumstances where informational logs are not enough to debug.

#### Warning

Any potential warning may cause side-effects, but it will not abort the execution of process.

#### Error

Any errors/exceptions which will abort the further execution of the process. Generally, this type of logs is recorded into a try catch block where exception handling is needed.

### End to end correlation

Each API request should have a unique identifier that should be tied up with all log statements related to this request.
Correlation id or request-id are common unique identifier. The Http request receives the unique identifier in its request header.

## Monitoring

Some of the metrics we want to be monitored in API, can be observed by hosting the API on defined API Gateway and use API Gateway analytics tools.
If the service is not hosted on defined these metrics must be obtained from service application and runtime logs.
Other metrics needs to be obtained from the API service application logs.

By defining the application log data in a format suitable for centralized log management, both analytics and monitoring data can be obtained from the log management system.

The core needs of what monitoring an API should return, is the answer to these two questions.

- What do I want to know?
- How do I want to act on that information?

For API's we want to monitor the following metrics.
Responsible party needs to be alerted on critical changes, i.e. if monitoring on the API indicates a critical problem that needs to be addressed.
Alerting should be provided for uptime, performance and error rate on API.

### API Uptime

What is the uptime of API? Is it less than predefined SLA? Does the API need improvement for stability?

### API Performance

Is the performance of the service changing? Is the response time acceptable? Should we get alert if the service is not performing fast enough?

### Usage per User / Application

What users or applications are using the API, is the usage increasing or decreasing? Has the user stopped using this API. Is the user’s application calling the API to rapidly?

### Success Rate / Error Rate

Is error rate of API growing? Is the quality of the API intact? Is error rate unacceptable?

### Security violations

Is there a threat or attack on the API? Can user retrieve unauthorized data?

### API Retention

Is this API not valuable enough?

### API Calls per business transaction

Are too many API calls involved in business transaction? Do we need to modify API for simpler usage?

### Correctness of data

Is API returning correct data? If not why, and what need to be fixed?

#### References

- [OWASP API Security Project](https://owasp.org/www-project-api-security/)
- [OWASP Logging Guide](https://owasp.org/www-pdf-archive/OWASP_Logging_Guide.pdf)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/index.html)
