##### Module 1 Introduction to amazon web services
Amazon EC2 (Amazon Elastic Compute Cloud) - the server 
Pay for what you need model
Cloud - all cloud compute
On Prem - all local compute (also called private cloud)
Hybrid Cloud - Usually where you need to have local resources and cloud resources availible when needed

##### Module 2 Compute in the cloud
###### EC2 **Instance Types** (Families): 

General purpose
Compute optimized
Memory Optimized
Accelerated computing (graphics)
Storage computing 

**Mulitancy**: sharing underlying hardware between virtual machines
**Vertically Scaling** an instance is giving 1 instance more CPU 
**Horizontal Scaling** would be purchasing more instances.

**EC2 Auto Scaling group** 

You can provision a group of EC2 Instances to be ready to provide extra support for no extra cost when they are offline. 


###### Elastic Load Balancing ELB: 
Amazon's easy to deploy Load Balancing framework runs on a region level meaning when you add or remove EC2 instances the load balancer will automatically deal with the change without further configuration needed. 

**Message and Queueing**: 
Tightly coupled arch if a single component fails it will cause issues for the entire system

Loosely coupled arch: if a single point fails the entire thing doesn't Amazon recommends to use Amazon Simple Queue Service SQS or Amazon Simple Notification Service SNS

**Amazon SQS**: Send receive store messages between software components at any volume SQS queues are where the messages wait to be received 

**Amazon SNS** : SNS topic a channel for messages to be delivered 


###### **Serverless compute**: You **cannot** see or access the underlying infrastructure, solely the application that you're running on the instance
Serverless compute options: 


**AWS Lambda**: service that lets you run code without provisioning or managing servers



Both run on AWS EC2 instances and use docker
ECS Elastic container service ( pretty much EC2 but a container )
EKS Elastic Kubernetes Service 
AWS Fargate can be used to not use EC2 and use a **Serverless** approach

**Summary:** 
Hosting traditional apps and have access to the OS use EC2

Host short functions or event driven apps with no provisioning or managing servers use Lambda

If you want to run containers Either ECS or EKS and then decide if you want to have it run on top of an EC2 Instance or a Fargate Instance (serverless)

##### Module 3 global infrastructure and reliability


###### **AWS Global Infrastructure**

Regions: groups of datacenters in one area they have multiple to support fault tolerance **(each region is isolated from another** unless explicitly specified). 

Some regions have certain features whereas others may not also meaning other regions may have a lower price

###### **AWS AZ's
**Availability Zone** is a single data center or a group of data centers within a Region. They are usually tens of miles apart 


[[#Elastic Load Balancing ELB]] will automatically load balance the different AZ's


###### Amazon CloudFront
Amazon AWS' CDN (Cloud delivery Network)

###### Amazon Route 53: 
amazons DNS server solution

###### Edge Locations: 

used to serve customers that are in remote areas where you don't want to dedicate a full HQ to so you just cache the data so they have easier access to it. 

These both use [[#Amazon CloudFront]] and [[#Amazon Route 53]]

###### AWS Outpost:



###### AWS Provisioning
You can use a GUI style console called the AWS Management console

Automatable:  
uses APIs to provision AWS instances so that users cannot make mistakes 
SDKs can be used aswell as a CLI straight to the API


###### AWS Elastic Beanstalk
Service that helps you 

###### AWS CloudFormation

An automatic configuration tool that parses YAML or JSON data to interact with AWS APIs 

##### Module 4 networking
###### Amazon VPC

Virtual Private Cloud
A private network in AWS

VPG Virtual Private Gateway: Used to limit access to a VPC by using a VPN tunnel

###### AWS DirectConnect: 
A service that lets you establish a dedicated private connection between your data center and a VPC. Think of it like a VPN except your the only one on the network
###### Networking / Security
Each instance comes with a security group (Instance level ACL)
the security group is Stateful meaning that it remembers the list of approved users
Stateless will check every packet 

By default Amazon NACLs are stateless and allow all inbound and outbound traffic
##### Module 5 storage and databases
###### Amazon EBS

Block level storage is good when you have a large file that is being edited or changed ie. a video file that you're editing using EBS would be better than using an S3 bucket here

Amazon Elastic Block Store Amazon EBS is a service that provides block-level storage volumes that you can use with Amazon EC2 instances. If you stop or terminate the instance all the data on the attached EBS volume remains available.

an instance store provides temp block-level storage for an EC2 Instance

You can take snapshots to backup data and only the data that has changed since the most recent snapshot is backed up 
###### Amazon S3
Amazon Simple Storage Service: it stores data as objects in a bucket the maximum file size in an object is 5 TB 

- **S3 Standard**: Ideal for frequently accessed data with low-latency and high-throughput.
- **S3 Intelligent-Tiering**: Automatically moves data between two access tiers (frequent and infrequent) to optimize costs.
- **S3 Standard-IA (Infrequent Access)**: For data that’s accessed less frequently, but still needs to be quickly available.
- **S3 One Zone-IA**: For infrequent access data that doesn’t need to be stored across multiple availability zones.
- **S3 Glacier**: Low-cost storage for data that is rarely accessed and can tolerate retrieval delays (hours).
- **S3 Glacier Deep Archive**: The lowest-cost storage for data that is rarely accessed and retrieval can take hours to days.
- **S3 Outposts**: Extends S3 storage to on-premises environments with AWS Outposts for hybrid workloads.

###### Amazon EFS

Amazon Elastic File System is a scalable file system used with AWS Cloud services and on-premises resources. As you add and remove files, Amazon EFS grows and shrinks automatically.

It's a regional service meaning that it works across multiple [[#AWS AZ's]]
on prem users can also access the EFS through Amazon [[#AWS DirectConnect]]
Compared to something like EBS where it stores it only in one AZ.
###### Amazon RDS

RDS is a relational database which means that data is stored in a way that relates it to other pieces of data.
i.e. someone buys the same thing multiple times we can tie that to a user. 

it uses 
- Amazon Aurora
- PostgreSQL
- MySQL
- MariaDB
- Oracle Database
- Microsoft SQL Server

###### Amazon Aurora 
This is an enterprise-level relational database that uses MySQL or PostgreSQL
Consider this if your workloads require high availability. Has 6 copies at any given time
###### Amazon DynamoDB
DynamoDB is a serverless, key-value, and nonrelational database service that runs single digit millisecond performance at any scale. It supports automatic scaling to scale your database to its needs.
###### Amazon Redshift
Amazon Redshift is a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and helps you to understand relationships and trends across your data.
###### Amazon Database Migration services

AWS DMS: enables you to migrate relational databases, nonrelational databases and other types of data stores.

this will migrate a source database to a target database when the migration is in progress the source database can still stay running the databases also don't have to be of the same type.

This can also be used to transfer a database to another base continuously 
##### Module 6 Security
###### AWS IAM
Identity and Access Management enables you to manage access to AWS services and resources securely. 

An **IAM** **policy** is a document that allows or denies permissions to AWS services and resources.
IAM policies enable you to customize users’ levels of access to resources. For example, you can allow users to access all of the Amazon S3 buckets within your AWS account, or only a specific bucket.

IAM groups are for a collection of IAM users and policies can be configured for both the user or the group 

IAM Roles are an identity that you can assume to gain temp access to permissions


Best practice is to use the IAM user with the thought of lowest privilege and give it an iam role for the tasks that you need temporarily and a policy for tasks that you will need long term. 
###### AWS Organizations

AWS Organizations create a root user for a specific group of users (organization) 

They are grouped into OUs (organizational units)

SCP (Service control policies) enable you to place restrictions on AWS services resources and individual API actions that users and roles in each account can access

###### AWS Artifact
AWS Artifact is a service that provides on-demand access to AWS security and compliance reports and select online agreements. AWS Artifact consists of two main sections: AWS Artifact Agreements and AWS Artifact Reports.

Customer compliance center contains resources to help you learn more about AWS compliance. 

###### AWS Shield 
AWS Shield is a service that protects applications against DDoS attacks. AWS Shield provides two levels of protection: Standard and Advanced.
###### AWS KMS 
**AWS Key Management Service** enables you to perform encryption operations through the use of **cryptographic keys**.
###### AWS WAF
AWS WAF is a web application firewall that lets you monitor network requests that come into your web applications.
###### Amazon Inspector
Amazon Inspector helps to improve the security and compliance of applications by running automated security assessments.
###### Amazon GuardDuty
Amazon GuardDuty is a service that provides intelligent threat detection for your AWS infrastructure and resources. It identifies threats by continuously monitoring the network activity and account behavior within your AWS environment.
##### Module 7 Monitoring and analytics
###### Amazon CloudWatch
A web service that enables you to monitor and manage various metrics and configure alarm actions based on data from those metrics.

Alarm if metric_cpu_utilization < 80% = alarm

You can make the alarms cause a notification 
###### AWS CloudTrail
AWS CloudTrail records API calls for your account. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller. Think of it like a log for APIs

CloudTrail insights will automatically detect unusual API activities in your AWS account
###### AWS Trusted Advisor
AWS Trusted Advisor is a web service that inspects your AWS environment and provides real-time recommendations in accordance with AWS best practices.

It checks these 5 categories based on AWS best practices: 
cost optimization, performance, security, fault tolerance, and service limits
##### Module 8 Pricing and support
###### AWS Cost Explorer
AWS Cost Explorer is a tool that lets you visualize, understand, and manage your AWS costs and usage over time.
###### AWS Marketplace
AWS Marketplace is a digital catalog that includes thousands of software listings from independent software vendors. You can use AWS Marketplace to find, test, and buy software that runs on AWS.
##### Module 9 Migration and innovation
###### AWS CAF
AWS Cloud Adoption Framework organizes guidance into six areas of focus, called **Perspectives**. Each Perspective addresses distinct responsibilities.

In general, the **Business**, **People**, and **Governance** Perspectives focus on business capabilities, whereas the **Platform**, **Security**, and **Operations** Perspectives focus on technical capabilities.
###### Migration Strategies
6 Rs of migration
- **Rehosting** also known as “lift-and-shift” involves moving applications without changes.
- **Replatforming**, also known as “lift, tinker, and shift,” involves making a few cloud optimizations to realize a tangible benefit.
- **Refactoring** (also known as **re-architecting**) involves reimagining how an application is architected and developed by using cloud-native features.
- **Repurchasing** involves moving from a traditional license to a software-as-a-service model.
- **Retaining** consists of keeping applications that are critical for the business in the source environment.
- **Retiring** is the process of removing applications that are no longer needed.
###### AWS Snow Family
AWS Snow Family is a collection of physical devices that help to physically transport up to exabytes of data into and out of AWS.

AWS Snow Family is composed of **AWS Snowcone**, **AWS Snowball**, and **AWS Snowmobile**.

###### AWS Snowcone
AWS Snowcone is a small, rugged, and secure edge computing and data transfer device. 
It features 2 CPUs, 4 GB of memory, and up to 14 TB of usable storage.
###### AWS Snowball
Comes in 2 types of devices 
**Snowball Edge Storage Optimized** devices are well suited for large-scale data migrations and recurring transfer workflows, in addition to local computing with higher capacity needs.

**Snowball Edge Compute Optimized** provides powerful computing resources for use cases such as machine learning, full motion video analysis, analytics, and local computing stacks.
###### AWS Snowmobile
AWS Snowmobile is an exabyte-scale data transfer service used to move large amounts of data to AWS.
##### Module 10 The cloud journey
###### AWS Well-Architected Framework
  
The AWS Well-Architected Framework helps you understand how to design and operate reliable, secure, efficient, and cost-effective systems in the AWS Cloud. It provides a way for you to consistently measure your architecture against best practices and design principles and identify areas for improvement.

###### 6 pillars: 
- **Operational excellence** is the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.
- The **Security** pillar is the ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies.
- **Reliability** is the ability of a system to do the following:
	  Recover from infrastructure or service disruptions
	  Dynamically acquire computing resources to meet demand
	  Mitigate disruptions such as misconfigurations or transient network issues
- **Performance efficiency** is the ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve.
- **Cost optimization** is the ability to run systems to deliver business value at the lowest price point.
- **Sustainability** is the ability to continually improve sustainability impacts by reducing energy consumption and increasing efficiency across all components of a workload by maximizing the benefits from the provisioned resources and minimizing the total resources required.
##### Module 11 AWS EXAM STUFF
The AWS Certified Cloud Practitioner exam consists of **65 questions** to be completed in **90 minutes**. The minimum passing score is **700** (the maximum score is 1,000).
![[AWS Cloud Practitioner Domains.png]]


