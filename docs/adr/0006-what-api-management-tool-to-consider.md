# What API Management tool to consider

* Status: accepted
* Deciders: devs
* Date: 2020-06-11

Technical Story: Design of Api Gateway / API Portal

## Context and Problem Statement

Is there available tool that is compliant to requirements?
Can the tool provide functionality for API Gateway?
Can the tool provide functionality for API Development Portal? 

## Decision Drivers

* Vendor lock in for runtime
* Open source or not
* Installation options
* Functional ability
* Market presence

### Functional ability for decision

Functional ability to consider when evaluating the tool. The following list was taken from [wikipedia page for API Management](https://en.wikipedia.org/wiki/API_management).

* Gateway: a server that acts as an API front-end, receives API requests, enforces throttling and security policies, passes requests to the back-end service and then passes the response back to the requester. A gateway often includes a transformation engine to orchestrate and modify the requests and responses on the fly. A gateway can also provide functionality such as collecting analytics data and providing caching. The gateway can provide functionality to support authentication, authorization, security, audit and regulatory compliance.
* Publishing tools: a collection of tools that API providers use to define APIs, for instance using the OpenAPI or RAML specifications, generate API documentation, manage access and usage policies for APIs, test and debug the execution of API, including security testing and automated generation of tests and test suites, deploy APIs into production, staging, and quality assurance environments, and coordinate the overall API lifecycle.
* Developer portal/API store: community site, typically branded by an API provider, that can encapsulate for API users in a single convenient source information and functionality including documentation, tutorials, sample code, software development kits, an interactive API console and sandbox to trial APIs, the ability to subscribe to the APIs and manage subscription keys such as OAuth2 Client ID and Client Secret, and obtain support from the API provider and user and community.
* Reporting and analytics: functionality to monitor API usage and load (overall hits, completed transactions, number of data objects returned, amount of compute time and other internal resources consumed, volume of data transferred). This can include real-time monitoring of the API with alerts being raised directly or via a higher-level network management system, for instance, if the load on an API has become too great, as well as functionality to analyze historical data, such as transaction logs, to detect usage trends. Functionality can also be provided to create synthetic transactions that can be used to test the performance and behavior of API endpoints. The information gathered by the reporting and analytics functionality can be used by the API provider to optimize the API offering within an organization's overall continuous improvement process and for defining software Service-Level Agreements for APIs.
* Monetization: functionality to support charging for access to commercial APIs. This functionality can include support for setting up pricing rules, based on usage, load and functionality, issuing invoices and collecting payments including multiple types of credit card payments.

## Considered Options

* [Google Apigee Edge](https://apigee.com/about/cp/open-source-api-management)
* [Mulesoft Anypoint](https://www.mulesoft.com/platform/api-management)
* [Software AG API Management](https://softwareaggov.com/products/integration/webmethods-api-management/)
* [IBM API Connect](https://www.ibm.com/cloud/api-connect)
* [Axway Ampify](https://www.axway.com/en/products/api-management) 
* [Tibco Mashery](https://www.tibco.com/products/api-management)
* [AWS](https://aws.amazon.com/api-gateway/api-management/) 
* [Sensedia](https://sensedia.com/)
* [Kong](https://konghq.com/)
* [Red Hat 3Scale](https://www.3scale.net/)
* [WSO2](https://wso2.com/api-management/)
* [Tyk](https://tyk.io/)
* [Dell Boomi](https://boomi.com/)
* [Microsoft Azure API Management](https://azure.microsoft.com/en-us/services/api-management/)
* [Nginx Plus](https://www.nginx.com/)
* [Broadcom Layer7](https://www.broadcom.com/products/software/api-management)
* [KrakenD](https://www.krakend.io/)
* [Netflix Zool](https://github.com/Netflix/zuul)
* [Api Umbrella](https://apiumbrella.io/)
* [Express Gateway](https://www.express-gateway.io/)
* [Gravitee.io](https://gravitee.io/)

### Considered options functional matrix

The following list checks out the options. The options were checked by looking into documentation and read reviews.
A Gap in the matrix does not mean that the option does not exist, only that it was not noted in documentation.

|API Management Tools|Apigee Edge|Mulesoft Anypoint|Software AG|IBM|Axway|Tibco Mashery|AWS|Sensedia|Kong|Red Hat 3Scale|WSO2|Tyk|Boomi|Azure|Nginx Plus|Broadcom|KrakenD|Netflix Zool|API Umbrella|Express Gateway|Gravitee.io|
|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|:-------------|
|**Platform Information**||||||||||||||||||||||
|On premise installation|Yes|Yes|Yes|Yes|Yes|Yes|||Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|
|Cloud Service|Yes|Yes|Yes|Yes|Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes||Yes||||||
|Hybrid Installation|Yes|Yes|Yes|||Yes||||||||||Yes||||||
|Open Source|No|Yes/No|No||No|No|No|No|Yes|Yes|Yes|Yes|No|No|No|No|Yes|Yes|Yes|Yes|Yes|
|License model|Paid|Paid|Paid||Paid|Paid|Paid|Paid|Paid|Apache/Paid|Apache/Paid|Mozilla/Paid|Paid|Paid|Paid|Paid|Apache|Apache|MIT|Apache License|Apache License|
|Cost of usage (on premise)||||||||||||||||||||||
|Cost of usage (cloud)||||||||||||||||||||||
|Gartner 2019|#1|#2|#3||#5|#6|#12|#9|#7|#8|#10|#17|#20|#14|N/A|#13|N/A|N/A|N/A|N/A|N/A|
|Forrester 2018|#2|#10|#3||#6|#5||||#15|#5|#12|N/A|#7|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|Forrester Market precense|Large|Large|Medium|Good|Medium|Medium||Small||Medium|Medium|Small|N/A|Good|N/A|N/A|N/A|N/A|N/A|N/A|N/A|
|||||||||||||||||||||||
|**Gateway**||||||||||||||||||||||
|OAuth |Yes|Yes|Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes||Yes|Yes|Yes|
|OpenID Connect|Yes|Yes|Yes||Yes||Yes||Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|||||Yes|
|Caching|Yes|Yes|Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes||||Yes|
|Throttling / Rate limit|Yes|Yes|Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes|Yes|Yes||No|Yes|Yes|Yes|
|Analytics|Yes||Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes|Yes||No|||||
|Stages (prod/dev/test)|Yes|Yes|Yes|||Yes|Yes|||Yes|Yes||Yes|Yes|Yes|||||||
|||||||||||||||||||||||
|**Publishing Tool**|Yes|Yes|Yes||||||||Yes||||||No|||||
|OpenAPI Description|Yes|Yes|Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes|Yes||Yes||||No|Yes|
|RAML API Descriptor||Yes|||Yes|Yes||||Yes|||Yes|No||||||||
|Soap WSDL Description|Yes|Yes|Yes||Yes|Yes||||Yes|Yes|Yes|Yes|Yes||Yes||||||
|Does tool provide Life Cycle Management of Services|Yes|Yes|Yes||Yes|Yes|Yes||||Yes|||Yes|||||||Yes|
|Message Mediation / Orchestration / Transformations|Yes||Yes||Yes|Yes|Yes||Yes||Yes|Yes|Yes|Yes||Yes|||||Yes|
|Does tool provide dynamic endpoints|Yes||Yes||Yes|Yes|||Yes||Yes|Yes||||||||||
|API Interface for registration of services|Yes||||Yes||Yes||Yes||Yes|Yes||||||||||
|||||||||||||||||||||||
|**Developer portal/API store**|||||||||||||||||No|No||No||
|API Inventory|Yes|Yes|Yes||Yes|Yes|Yes||Yes|Yes|Yes|Yes|Yes||Yes|Yes|||Yes||Yes|
|Access request workflow|Yes|Yes|Yes||Yes||||||Yes|Yes||||Yes|||||Yes|
|Branding / Customize user interface|Yes|Yes|Yes|||Yes|Yes||Yes|Yes|Yes|Yes|Yes|||Yes||||||
|Analytics|||||||||||Yes||Yes||||||||Yes|
|||||||||||||||||||||||
|**Reporting and analytics**|||||||||||||||||No|No||No||
|Does tool provide Monitoring Dashboard|Yes|Yes|Yes||Yes|Yes|Yes||Yes||Yes|Yes|Yes|Yes|Yes|Yes|||||No|
|Does tool provide Logging of request.|Yes|Yes|Yes||Yes|Yes|Yes||Yes||Yes|Yes|Yes|Yes|Yes|Yes||||||
|Does tool provide statistics for SLA.|Yes|Yes|Yes||Yes||Yes||||Yes|||||||||||
|Does tool provide logging to ELK / 3rd party logging|Yes|Yes|Yes||Yes|Yes|||Yes||Yes|Yes|||Yes|Yes|||Yes||Yes|

## Decision Outcome

Based on the option to run the API Management tool on premise, the following options have been pinpointed for further analysis.

If open source options are not a requirement, it is suggested to evaluate the following tools.

* [Mulesoft Anypoint](https://www.mulesoft.com/platform/api-management)
* [Software AG API Management](https://softwareaggov.com/products/integration/webmethods-api-management/)
* [IBM API Connect](https://www.ibm.com/cloud/api-connect)
* [Axway Ampify](https://www.axway.com/en/products/api-management) 
* [Tibco Mashery](https://www.tibco.com/products/api-management)
* [Nginx Plus](https://www.nginx.com/)

These are the tools that are most mature, and do not provide lock in for runtime platform. 
They need to be evaluated based on pricing and technical ability.

If true open source is required, it is suggested to evaluate the following tools.

* [Kong](https://konghq.com/)
* [Red Hat 3Scale](https://www.3scale.net/)
* [Tyk](https://tyk.io/)
* [WSO2](https://wso2.com/api-management/)

These tools provide open source offering, but in most cases the features for Api Developer Portal and Publishing tools are only part of enterprise offering with subscription.
Evaluation is needed for validating if the open source offering of the tool contains what is needed for implementation. 
We need to evaluate pricing of enterprise offering against the price of creating/implementing required pieces, like custom Api Developer Portal. 

For all considered tools we need to check what underlying software components are required. For example, data storage, queuing and logging capacity.
We need to take into consideration effort and ability to build Developer portal, compared to customizing the tool offering.

Downside for 

* [Google Apigee Edge](https://apigee.com/about/cp/open-source-api-management)
* [AWS](https://aws.amazon.com/api-gateway/api-management/) 
* [Microsoft Azure API Management](https://azure.microsoft.com/en-us/services/api-management/)

is that they are all platform dependent, to the owners proposed platform with more limited on-premise options. These are all top of the line tools according to capabilities, so
if vendor lock was not one of the decision drivers, they would be on evaluation list.

Other tools that we looked at did in our opinion lack functionality or other ability for further considered, even though many of them could be considered.
Note that the list provided is not all existing Api Management tools, so other options might apply.

### Positive Consequences

* Api Management tools are listed and grouped based on if they have open source option or not.
* This is first phase of decision on what tool could help implementation on Api Management Platform, and narrow down options to consider.

### Negative Consequences

* Follow up is required on tool that will make the shortlist.

## Pros and Cons of the Options 

### [Google Apigee Edge](https://apigee.com/about/cp/open-source-api-management)

Full blown API Management Platform from Google.

* Good, considered leader by both Gartner and Forrester
* Good, number 1 product in Gartner.
* Good, number 2 product in Forrester.
* Good, offers lot of functionality, and easy to use. `Gartner`
* Good, big market presence. `Forrester`
* Bad, complex to install on site. `Gartner`
* Bad, prices are higher. `Gartner`
* Bad, cloud offerings are only available on Google Cloud.

### [Mulesoft Anypoint](https://www.mulesoft.com/platform/api-management)

Full blown API Management Platform from Mulesoft. Mulesoft products combine Application Integration and API management in product suite.
Mulesoft is based on open source core product Mule. [GitHub](https://github.com/mulesoft/mule), but API management components are not open source.
Mulesoft was acquainted by SalesForce 2018. 

* Good, considered leader by Gartner and strong performer by Forrester
* Good, number 2 product in Gartner.
* Good, because chosen option for Australia gov.au platform.
* Good, because Mulesoft offers stand-alone offering for API Management.
* Consideration, consideration what happens with ownership of SalesForce.

### [Software AG API Management](https://softwareaggov.com/products/integration/webmethods-api-management/)

Full blown API Management Platform from Software AG. Software AG products combine Application Integration and API management in product suite.
Software AG products are not open source. 

* Good, considered leader by both Gartner and Forrester
* Good, number 3 product in Gartner.
* Good, number 3 product in Forrester.
* Good, offers stand-alone offering for API Management.

### [IBM API Connect](https://www.ibm.com/cloud/api-connect)

Full blown API Management Platform from IBM. 
API Connect from IBM is not open source. 

* Good, considered leader by both Gartner and Forrester
* Good, number 1 product in Forrester.
* Good, number 4 product in Gartner.

### [Axway Ampify](https://www.axway.com/en/products/api-management) 

Full blown API Management Platform from Axway. Axway products combine Application Integration and API management in product suite.
Axway products are not open source.

* Good, considered leader by both Gartner and strong performer by Forrester
* Good, offers stand-alone offering for API Management.

### [Tibco Mashery](https://www.tibco.com/products/api-management) 

Full blown API Management Platform from Tibco. Tibco products combine Application Integration and API management in product suite.
Tibco products are not open source.

* Average, considered visionary by Gartner and strong performer by Forrester.
* Good, offers stand-alone offering for API Management.

### [AWS](https://aws.amazon.com/api-gateway/api-management/) 

Full blown API Management Platform from AWS. 

* Good, in 2018, AWS’s revenue from Amazon API Gateway grew by a market-leading 160% year over year, far above the market average of 31%. `Gartner`
* Average, considered challenger by Gartner
* Consideration, AWS indicates that their product can be installed on premise, but most reviews point out that it is Cloud only offering.
* Bad, AWS doesn’t offer a customer-managed gateway, which is critical technology for many
organizations operating in highly secured and restricted on-premises environments. However,
its AWS Outposts offering, which provides AWS services on-premises (managed, maintained
and supported by AWS), is in preview at the time of writing. `Gartner`

### [Sensedia](https://sensedia.com/)

To get further information about Sensedia product we need to register email and read whitepapers. Review is based on Gartner / Forrester report.

* Average, considered visionary by Gartner and strong performer Forrester
* Good, Sensedia is one of the few vendors in this market to support the growing demand for the creation and management of GraphQL endpoints. `Gartner`
* Bad, Although Sensedia has been hiring local staff and has begun to expand into Europe, it still has limited reach beyond its home country of Brazil. `Gartner`
* Bad, Small market presence `Forrester`

### [Kong](https://konghq.com/)

Kong is open source API gateway. [GitHub](https://github.com/Kong).
The open source part is Kong Gateway. Kong provides Enterprise Edition of the Product, that includes API Developer Portal, and Developement Tools.
Kong is built on NginX.

* Average, considered visionary by Gartner.
* Good, large open source community, over 180 contributors and 25000 GitHub stars.
* Good, large range of installation modules.
* Good, provides maintainance and support for large enterprise.
* Good, API Interface for managing the gateway.
* Bad, little SOAP support.

### [Red Hat 3Scale](https://www.3scale.net/)

Red Hat 3Scale is open source API gateway [GitHub](https://github.com/3scale/APIcast). It needs license for usage.

* Average-, considered visionary by Gartner and contender by Forrester
* Good, fully open source product. All offerings are open source.
* Good, company has good market presence `Forrester`
* Consideration, small community, 28 contributors 196 GitHub stars

### [WSO2](https://wso2.com/api-management/)

WSO2 is open source API management tool. It can be obtained from GitHub without support, but Paid option includes support and fixes.

* Average+, considered visionary by Gartner and leader by Forrester
* Good, number 4 product in Forrester.
* Good, decent open source community, 144 contributors and 410 GitHub stars.
* Good, fully open source product. All offerings are open source.
* Consideration, recent change in license model, directing customers to paid support.

### [Tyk](https://tyk.io/)

Full blown API Management Platform from Tyk. Tyk provides open source API Gateway, and paid version of the program that includes Tyk API Dashboard, Designer, Analytics and Developer Portal.

* Average, considered strong performer by both Gartner and Forrester
* Good, API Gateway is free to use for all forever according to homepage.
* Good, good open source community, 62 contributors and 5500 GitHub stars.
* Bad, Small market presence `Forrester`

### [Dell Boomi](https://boomi.com/)

Boomi is full blown API Management Platform from Dell. This is enterprise solution, and not open source.

* Average-, considered nice player by Gartner.
* Bad, score lowest of all vendors in Gartner report.

### [Microsoft Azure API Management](https://azure.microsoft.com/en-us/services/api-management/)

Api management platform from Microsoft.

* Good, considered leader by both Gartner and Forrester
* Consideration, Microsoft indicates that theyr product can be installed on premise via VLAN, but most reviews point out that it is Cloud only offering.
* Bad, Azure API Management is an Azure cloud service and will remain focused on developers’ and
IT professionals’ priorities to build, deploy and manage applications through Microsoft’s global
cloud. It’s unlikely to evolve in response to the main business drivers of digital transformations,
in contrast to most other offerings in this market. `Gartner`

### [Nginx Plus](https://www.nginx.com/)

NginX offers API management in Nginx Plus and Nginx Controller product.
NginX Plus and NginX Contoller are not open source products.

* Good, NginX open source reverse proxy is videly used as component in other API Managemen solutions.
* Bad, Did not find many information about distribution and usage.

### [Broadcom Layer7](https://www.broadcom.com/products/software/api-management)

Layer7 is full blown API Management Platform from Broadcom.
Layer7 is not open source product.

* Average-, considered nice player by Gartner
* Bad, drops from leader in Gartner report. `Gartner`

### [KrakenD](https://www.krakend.io/)

Krakend offers open source API Gateway. Tool is intended to create REST interface to combine many calls to backend system.

* Consideration, small community, 17 contributors but 2700 GitHub stars
* Bad, no developer portal.
* Bad, tool not intended as API Management tool, only gateway to combine microservice in single platform.

### [Netflix Zool](https://github.com/Netflix/zuul)

Zool is open source API Management Tool by Netflix, [GitHub](https://github.com/Netflix/zuul)
Zool is purpose was to serve as backend of the NetFlix streaming application.

* Good, 66 contributors and 9400 GitHub stars.
* Consideration, 66 contributors but very small activity on GitHub.
* Consideration, designed for use with Netflix.
* Bad, no Api Developement Portal.
* Bad, Last release nearly one year ago.

### [Api Umbrella](https://apiumbrella.io/)

Open source API management tool by National Renewable Energy Laboratory.
Open source [GitHub](https://github.com/NREL/api-umbrella)

* Consideration, 66 contributors but very small activity on github.
* Bad, latest release over one year ago.

### [Express Gateway](https://www.express-gateway.io/)

According to homepage, initial purpose as microservices API Gateway.
Open Source [GitHub](https://github.com/ExpressGateway/express-gateway)

* Bad, No support for OpenAPI, requested in GitHub 2018 without implementation.
* Bad, 26 contributors, and very small activity on GitHub.

### [Gravitee.io](https://gravitee.io/)

According to homepage, initial purpose as microservices API Gateway.
Open Source [GitHub](https://github.com/gravitee-io).

* Good, 995 Github stars.
* Bad, only 16 contributors, and very small activity on GitHub.
* Consideration, Currently creating Enterprise edition in order to have money to address all change requests.

## Links

* [`Gartner`](https://www.gartner.com/) Magic Quadrant for Full Life Cycle API Management, Published 9 October 2019
* [`Forrester`](https://www.forrester.com/) The Forrester Wave™: API Management Solutions, Q4 2018
