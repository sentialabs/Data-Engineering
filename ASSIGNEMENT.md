# Sentia Recruitment
Welcome to Sentia Recruitment
The purpose of this repository is to provide an assignment that will highlight the strengths required by a cloud data engineer in our public cloud consultancy workforce.
## Table of content
- [General Information](#general-information)
- [Assignment](#assignment)
    - [Part 1 - Creation of an ETL process and deployment](#part-1---Creation-of-an-ETL-process-and-deployment)
    - [Part 2 - Create app to generate test data](#part-2---Create-app-to-generate-test-data)
    - [Part 3 - CI/CD](#part-3---cicd)
- [Deliverables](#deliverables)
- [Links](#links)
- [License](#license)
## General Information
This assignment is meant to challenge the potential applicant in the complete spectrum of designing a solution and delivering an environment in the public cloud using Infrastructure as Code (IaC).
Please be aware of the fact that we are not only looking at the actual deliverables but also the process followed to achieve these results. *The presentation of the results is of equal importance to the actual results.*
You will need to make a choice of delivering your solution in either **Amazon Web Services** or **Microsoft Azure**. We prefer the usage of native tools for IaC. Please use *CloudFormation (CFN)* or *Azure Resource Manager (ARM)* templates for this purpose and **not Terraform**. Of course, third party tools are always necessary in some cases. Please find suggested tools and guides in the [Links](#links) section that may help you in this journey.
## Assignment
### Part 1 - Creation of an ETL process and deployment
You have participated in a meeting with a client to assess their strategy to migrate to the public cloud. They are currently disclosing 10 data sources on multiple platforms. What they want the data sources to be extracted, transformed and Loaded to the public cloud. This is to have them available for their data scientists. The past few months, they have been having a lot of issues with small files. The current ETL processes where not created correctly.In the design there should be an approach how to prevent this from happening. Their current landscape consists of Informatica for ingress, Spark for transformation and SQL warehouse as a data warehouse. All of these need to be transformed to cloudnative solutions if possible. Please explain in the design why you decided on what. The customer asked to design the future state of this environment in the public cloud. The solution needs to:
* be scalable and flexible.
* be futureproof and expandable with new data pipelines.
* be cost effecient

### Part 2 - Create app to generate test data
To test your data pipelines we typically create test data. In part 1 you created a design for the platform. Below you can find an assignment to create a app to generate the test data for the platform you designed above.

The customer raises hundreds of different event types. This task involves a simplification of the following 3 event types which are part of the ordering process workflow:
* 'OrderPlaced' *is raised when a customer places an order.*
* 'OrderDelivered' *is raised when the customer receives their order.*
* 'OrderCancelled' *is raised when the customer manually cancels or the company hasn't got the inventory to complete the order.*

'OrderPlaced' represents the beginning of the workflow. Either one of 'OrderDelivered' or 'OrderCancelled' represents the terminus of the work flow.

The event Schema is as follows:
```json
{
    "Type": "OrderPlaced",
    "Data": {
        "OrderId": "3cb0f939-9398-4d29-a28f-2a1a3a6ce3b2",
        "TimestampUtc": "2017-05-14T19:12:32Z"
    }
}
```
* 'Type' *is the event type.*
* 'Data.OrderID' *is randomly generated uuid which uniquely identifies an order. A single order may have more than one event associated with it.*
* 'Data.TimestampUtc' *is the timestamp (iso format) at which the event occurred.*

*Implementation*

The technical test is to write an app that can generate events.
* Each order will produce two events namely ('OrderPlaced', 'OrderDelivered') or ('OrderPlaced', 'OrderCancelled')
* For every six orders, four order will consist of 'OrderPlaced' and 'OrderDelivered' events and two orders of 'OrderPlaced' and 'OrderCancelled' events.
* the batch of events within a given interval should be stored in a line-delimited JSON file named 'orders-<timestamp>.json' eg. Orders-2020-07-16-09-27-31-874511.json
* the app must take 4 arguments:
** number-of-orders - Number of orders to generate. (nb. Each order produces two events)
** batch-size - number of events per file.
** interval - Interval in seconds between each file being created.
* How to run the app:
```json
Generate-events \
	--number-of-orders=100000 \
	--batch-size=5000 \
	--interval=1 \
	--output-directory=<local-dir>
```
* Example shows a snippet of ten events from the content of a generated file. Each event is on its own line separated by a line-break.
```json
    { "Type": "OrderPlaced", "Data": { "OrderId": "3cb0f939-9398-4d29-a28f-2a1a3a6ce3b2", "TimestampUtc": "2020-07-14T19:12:32Z" } }
    { "Type": "OrderDelivered", "Data": { "OrderId": "3cb0f939-9398-4d29-a28f-2a1a3a6ce3b2", "TimestampUtc": "2020-07-14T19:12:32Z"} }
    { "Type": "OrderPlaced", "Data": { "OrderId": "a7d86ca5-7541-4c86-a7ad-1bec2b070b3c", "TimestampUtc": "2020-07-14T19:12:33Z" } }
    { "Type": "OrderDelivered", "Data": {"OrderId": "a7d86ca5-7541-4c86-a7ad-1bec2b070b3c", "TimestampUtc": "2020-07-14T19:12:33Z"} }
    { "Type": "OrderPlaced", "Data": { "OrderId": "757001d9-a454-40d3-a14b-9f0f9440be9f", "TimestampUtc": "2020-07-14T19:12:34Z" } }
    { "Type": "OrderDelivered", "Data": { "OrderId": "757001d9-a454-40d3-a14b-9f0f9440be9f", "TimestampUtc": "2020-07-14T19:12:34Z"} }
    { "Type": "OrderPlaced", "Data": { "OrderId": "4f3fd16c-4685-45e6-a6f9-823f5f73a7d0", "TimestampUtc": "2020-07-14T19:12:35Z" } }
    { "Type": "OrderDelivered", "Data": {"OrderId": "4f3fd16c-4685-45e6-a6f9-823f5f73a7d0", "TimestampUtc": "2020-07-14T19:12:35Z"} }
    { "Type": "OrderPlaced", "Data": { "OrderId": "812a8469-68d0-4c9b-8429-d46d51d63db3", "TimestampUtc": "2020-07-14T19:12:36Z" } }
    { "Type": "OrderDelivered", "Data": { "OrderId": "812a8469-68d0-4c9b-8429-d46d51d63db3", "TimestampUtc": "2020-07-14T19:12:36Z"} }
    { "Type": "OrderPlaced", "Data": { "OrderId": "8825cd95-f172-4132-9793-864b4dd725df", "TimestampUtc": "2020-07-14T19:12:37Z" } }
    { "Type": "OrderCancelled", "Data": {"OrderId": "8825cd95-f172-4132-9793-864b4dd725df", "TimestampUtc": "2020-07-14T19:12:37Z"} }
```
* Each 'OrderPlaced' event must have a 'OrderDelivered' or 'OrderCancelled' event with the same 'OrderId'.

### Part 3 - CI/CD
Please provide a design for the CI/CD pipeline that you will use to deliver the changes to the environment, every time the client updates requirements in GIT. For this purpose, please treat the target architecture from [Part 1](#part-1---transformation-and-migration-to-the-public-cloud) as a black box.
## Deliverables
Please provide the following:
* For Part 1, an architectural design and IaC templates for deploying the components.
* For Part 2, provide the GIT repo with the app in there.
* For Part 3, a complete architectural design of the CI/CD process.
* Please include a simple time log of the activities you have performed.
* Please document any assumptions and decisions you have made.
* Please include a presentation of the results within slides, ready to be presented to our client.
## Links
- [The Twelve Factors](https://12factor.net/)
- [GitHub For Beginners: Don’t Get Scared, Get Started](https://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1/)
- [Draw.io](https://www.draw.io/)
- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/index.html)
- [Resource Manager on Azure documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
- [AWS Cloud Development Kit (AWS CDK)](https://github.com/aws/aws-cdk)
- [Amazon EC2 Auto Scaling](https://aws.amazon.com/ec2/autoscaling/?sc_channel=ba&sc_campaign=autoscaling-ec2-button&sc_medium=button&sc_country=global&sc_geo=global&sc_outcome=aware)
- [Microsoft Azure Virtual Machine Scale Sets](https://docs.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview?toc=%2Fazure%2Fvirtual-machines%2Flinux%2Ftoc.json)
- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
- [Microsoft Azure Cloud Design Patterns](https://docs.microsoft.com/en-us/azure/architecture/patterns/)
- [Containers](https://www.docker.com/resources/what-container)
## License
Copyright © 2020, [Sentia](https://sentia.com). All rights reserved.
