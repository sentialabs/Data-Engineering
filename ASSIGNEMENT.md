# Sentia Recruitment
Welcome to Sentia Recruitment
The purpose of this repository is to provide an assignment that will highlight the strengths required by a cloud data engineer in our public cloud consultancy workforce.
## Table of content
- [General Information](#general-information)
- [Assignment](#assignment)
    - [Part 1 - Creation of an ETL process and deployment](#part-1---Creation-of-an-ETL-process-and-deployment)
    - [Part 2 - CI/CD](#part-2---cicd)
- [Deliverables](#deliverables)
- [Links](#links)
- [License](#license)
## General Information
This assignment is meant to challenge the potential applicant in the complete spectrum of designing a solution and delivering an environment in the public cloud using Infrastructure as Code (IaC).
Please be aware of the fact that we are not only looking at the actual deliverables but also the process followed to achieve these results. *The presentation of the results is of equal importance to the actual results.*

## Assignment
### Part 1 - Creation of an ETL process and deployment
You have participated in a meeting with a client to assess their strategy to migrate to the public cloud. They are currently disclosing 10 data sources on multiple platforms. What they want the data sources to be extracted, transformed and Loaded to the public cloud. This is to have them available for their data scientists. The past few months, they have been having a lot of issues with small files. The current ETL processes where not created correctly.In the design there should be an approach how to prevent this from happening. Their current landscape consists of Informatica for ingress, Spark for transformation and SQL warehouse as a data warehouse. All of these need to be transformed to cloudnative solutions if possible. Please explain in the design why you decided on what. 
The solution needs to:
* be scalable and flexible.
* be futureproof and expandable with new data pipelines.
* be cost effecient

### Part 2 - CI/CD
Please provide a design for the CI/CD pipeline that you will use to deliver the changes to the environment, every time the client updates requirements in GIT. For this purpose, please treat the target architecture from [Part 1 - Creation of an ETL process and deployment](#part-1---Creation-of-an-ETL-process-and-deployment) as a black box.


## Deliverables
Please provide the following:
* For Part 1, an architectural design of the platform and the IaC templates for the components.
* For Part 1, functional design of the whole ETL process.
* For Part 2, a complete architectural design of the CI/CD process.
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
- [Microsoft Azure cloud Analytics solutions](https://docs.microsoft.com/en-us/azure/architecture/solution-ideas/articles/advanced-analytics-on-big-data)
- [AWS big data](https://aws.amazon.com/big-data/datalakes-and-analytics/)
## License
Copyright © 2020, [Sentia](https://sentia.com). All rights reserved.
