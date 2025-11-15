# AWS & Database Fundamentals Notes

## 1. Compute and Infrastructure

### 1.1. EC2 (Elastic Compute Cloud)
> EC2 is a web service that provides secure and resizable virtual servers on the cloud.
- Allow the user to rent virtual machines called instances
- Able to control the amount of CPU, Memory, GPU, storage, and network capacity as needed

#### EC2 instances option
- General purpose: CPU, memory, and network balances. Ex: Web server
- Compute optimized: CPU utilization. Ex: Game
- Memory optimized: used to keep large memory data sets. Ex: big data
- Storage optimized: sequential read & write access. Ex: Data warehouse
- Accelerated computing: Hardware accelerators where the GPU is prioritized. Ex: Machine/Deep learning
- HPC optimized: uses High-performance processors to fit different use cases. Ex: Complex simulation

#### EC2 (Elastic Compute Cloud) Overview
- Enables scale up, handle changes or spikes
- Hosted in multiple region, SLA 99/99% availability for each Amazon EC2 region
- Can access Amazon EFS across AZs, VPC, and regions


### 1.2. AWS Global Infrastructure
- AWS Regions: a geographical cluster of data centers. Has at least 2 AZ; can have up to 6.
- Availability Zones (AZ): Separated by a couple of kilometers for redundancy, each AZ has 1-3 data centers
  - Housed in separate facilities with redundant power and redundant parallel fiber network
  - Provide Amazon CloudFront that uses the Global Content Delivery Network (CDN)
  - Helps with partitioning to protect from natural disasters

#### AWS Global Infrastructure Benefit
- Better performance, availability, and reliability
- Security that satisfies the requirements for military and global banks
- Scalability based on actual business need
- Lower cost of ownership and overall price of IT Infrastructure


## 2. Storage and Content Delivery

### 2.1. S3 (Simple Storage Service)
- An object storage service that keeps data as objects
- An object consists of data and metadata (name-value pairs) itself, uniquely identified using a key
- Scalable, pay-only-for-used-services, with eleven 9's of data durability
- AUsed for website, mobile/enterprise app, backup, IoT devices, big data analytics

#### S3 Features and Management
- Storage classes: range from data that is often accessed (standard) to archives that are accessed every couple of days or weeks (Glacier)
- S3 Storage Class Analysis: Sort data based on data access pattern
- S3 Lifecycle Policy: transfer data to a different bucket based on how often it is accessed, and also adjust when data expires
- S3 Cross-Region Replication (CPR) or S3 Same Region Replication: data can be replicated to AWS in a different region or in the same region
- S3 Object Lock: lock data based on retention period, enforce write-once-read-many (WORM) policies
- Ability to integrate with AWS Lambda to create alerts, log activities, and automate workflow
- Can run big-data analytics on the S3 objects themselves
- Data can be queried with,
  - Amazon Athena: with SQL, query regular data
  - Amazon Redshift Spectrum (mostly for complex queries): with SQL for data at rest
- Items stored can be versioned or unversioned to easily retrieve the previous version, useful against accidental deletion or overwrite

#### Amazon S3 - Access Management
- By default, access is private and only accessible to the resource owner. Access can be granted by a different option.
  - Resource-based policies: policies are added to resources through ACL or bucket policies as a JSON file. Temporary access also allowed using a time-limited URL
  - User policies: Given to the user, using AWS IAM
  - Combination of both.

### 2.2. Amazon EBS (Elastic Block Store)
- Block-level storage volumes for EC2 instances.
- One EBS can only mount to one instance at a time; multiple EBS can attach to one instance
- Low latency between the EBS volume and EC2 instance up to milliseconds.
- Used for high throughput and intensive workloads.
- Data persists in the EBS volume even when the EC2 instance is deleted.
- Two types of storage used are: 
  - SSD (Solid-State Drive) backed storage - for frequent R/W with small I/O
  - HDD (Hard Disk Drive) backed storage - throughput intensive workload (mapReduce, Data warehouse, log processing)

### 2.3. Amazon EFS (Elastic File System)
- Manages file storage infrastructure for Linux (NFS 4.0 and 4.1)
- Help deploy, patch, and maintain the file system
- Scale on demand to petabytes
- Encrypt data in rest and on transit, security compliance
- Support massive parallel shared access to EC2 instances
- Regional services that keep data across multiple AZs
- Can be accessed by ECs across different AZs, VPCs, and regions
- Can be accessed by an on-premise server using AWS Direct Connection or AWS VPN
- Different option,
  - Amazon EFS - for Linux
  - Amazon FSX - for Windows app and Windows file server

 
## 3. Database

### 3.1. Amazon Relational Database Service (RDS) Overview
- A managed relational database service (resizable, handles monitoring and patching).
- Easy to administer: no need for infrastructure provisioning, installing, or maintaining.
- Available and Durable: Multi-AZ DB instances provide synchronous replication to different AZs.
- Secure: Able to be isolated in a VPC.
- Engine Choices: Amazon Aurora, PostgreSQL, MySQL, MongoDB, Oracle, SQL Server.
- Migration: Simple using AWS Database Migration Service.

#### RDS Features
- Lower Administrative Burden
- Choose between 3 different instance classes: general purpose, memory-intensive, and burstable
- Provide automatic software patching
- Different storage types
  - Gp2 (General purpose) storage that is based on SSD
  - Magnetic storage - std storage, backward compatibility
  - Provisioned IOPS (SSD) Storage -  consistent, up to 40,000 IOPS per DB instance, optimised for I/O intensive
- Automatic backup of up to 35 days, also provides manual database snapshots

### 3.2. Non-Relational Databases (NoSQL)

#### NoSQL Database Overview
- Non-relational databases that are purpose-built
- Don't have a fixed, pre-defined schema
- Scale horizontally instead of vertically

#### NoSQL Database Models for AWS
- Amazon DynamoDB - Key value
- Amazon DocumentDB (with MongoDB compatibility) - for catalogs, JSON, and user profiles
- Amazon Neptune, Neo4j - graph, relationships, node, fraud detection
- Amazon ElastiCache, Amazon DynamoDB Accelerator (DAX) - microseconds responses
- Amazon Elasticsearch Service - for searching data content, indexing, categorizing, and analyzing

#### SQL vs NoSQL Database
| SQL (Relational Database) | NoSQL (NonRelational Databases) |
| --- | --- |
| Optimal for transactional data (OLTP) and Online Analytical Processing (OLAP) | Can be any type, as key-value, graph, document, semi-structured data, etc |
| ACID properties - Atomicity, consistency, Isolation, durability | High throughput and low latency |
| Vertical scaling | Horizontal Scaling, partitionable and distributed architecture |
| Fixed, Row and column-based schema | Can provide ACID by using DynamoDB |

## 4. Networking and Security

### 4.1. Amazon VPC (Virtual Private Cloud)
- Logically isolated private cloud within an AWS account with a default VPC based on the AWS region
- Allows manual configuration of a virtual network environment with IP address range, subnets, and gateway
- Support IPv4 (default) and IPv6
- All different subnets have to stay in one region, but a couple of VPN can be created throughout different regions
- Allow multiple layers of advanced security features using NACLs (Network Access Control Lists - firewall) 

#### Amazon VPC concept
- When creating a VPC, a private IP address has to be assigned using a CIDR block
- Private IP will not be reachable through the public, used only for private communication of your instances inside the VPC
- Each subnet has to have a route table
- NACL (Network Access Control List): Stateless firewall applied to subnets.
  - Default denies all inbound; allows all outbound.
  - One NACL per subnet.
  - Rules are checked from top to bottom.

#### Enabling VPC Internet Connection
1. Attach an Internet Gateway to the VPC.
2. Add a route to the Internet Gateway in the subnet's route table.
3. Assign a public IPv4, IPv6, or Elastic IP address.
  - NAT Gateway: Enables instances in a private subnet to reach the internet without being publicly reachable (doesn't support IPv6).
  - Egress-only Internet Gateway: For IPv6; allows outbound traffic but prevents inbound traffic.

#### VPC Peering Connections
- Route traffic between two VPCs using private IPv4 or IPv6 addresses
- Can connect VPCs in the same or different accounts/regions.
- Not a gateway or VPN; uses existing VPC infrastructure.
- Requires the Requester VPC to send a request and the Accepter VPC to accept it (requires non-overlapping CIDR blocks).

### 4.2. Security and compliance services
- AWS Security Hub - provides a central view of security posture and compliance status across the AWS environment.
- AWS Artifact - a self-service portal to access compliance reports.
- Amazon Inspector - continuously scanning for vulnerabilities and checking AWS resources configuration.
- Amazon GuardDuty - a managed threat detection service, uses threat intelligence and Machine learning.
- AWS Shield - always-on detection to detect, remediate, and prevent DoS and DDoS.

### 4.3. AWS IAM (Identity & Access Management)
- Enables access to AWS resources securely, and manages who can interact with AWS
- Each IAM (user, group, or role) will inherit the permissions of the group
- Deny by default unless said otherwise
- Offered as a feature of the AWS account, with no additional charges
- Allows control over allowed login time, source IP address, and MFA

#### IAM Policies
- Attach IAM policy to IAM entities, which consist of statements,
  | Field | Description |
  | --- | --- |
  | version | specify the version of the policy language |
  | SID (optional) | specify statement ID |
  | Effect | to allow or to deny, but the default is to deny |
  | Principal | the IAM entities that will be affected |
  | Action | list of actions to allow or deny |
  | Resources | mention the specific resource the action will affect |
  | Conditions | the requirements can be either by time, login MFA, etc |
- IAM Access Analyzer
  - Analyze the resources that will be available outside an AWS account based on the resource policy
  - Utilizer Amazon S3 buckets, AWS KMS keys, Amazon SQS queues, IAM roles, AWS Lambda functions


## 5. Monitoring and Management

### 5.1. Amazon CloudWatch Overview
- Used to monitor logs, metrics, and events for developers and engineers
- Optimize resources, data & insights, respond to performance changes, operational health
- Provides a unified view of AWS Resources, applications, AWS Services, and on-premises servers (via the CloudWatch agent).
- Detects anomalous behavior and allows setting alarms for troubleshooting.
- Benefit: Can monitor hybrid cloud environments using the CloudWatch agent.
- Example Use: Can trigger EC2 autoscaling or stop/run instances.

### 5.2. AWS System Manager 
- Operations Management - central location for issue resolving and investigation
- Change Management - automates common tasks using System Manager Documents
- Application Management - manages application and service metadata
- Node Management - AWS Systems Manager Fleet Management to streamline management

#### AWS System Manager use cases:
- Centralized operations by aggregating data to a viewable console
- Implement the best proactive and reactive processes
- Remediate Security Issues - enhance security and Compliance
- Auto-resolve Issues - manage applications and issues easily

### 5.3. AWS Auto Scaling and Healing
- Monitor apps and set up application scaling
- Build scaling plans using Spot Fleets, ECS Tasks, or DynamoDB Index
- Automatically monitor health using ELB Check Trigger to automatically shift the instances when an issue occurs.
- When termination, Life Cycle Hooks (via CloudWatch Events and Lambda) trigger EC2 Systems Manager


## 6. Strategy and Cost

### 6.1. AWS Pricing
- Pay only for the service you need, cost optimization
- No long-term contracts or complex licensing, services are priced independently and transparently based on demand.
- Has management tools to monitor costs for better planning
- Pricing Models: By hour/second, capacity reservation, spot instances, and savings plans.

### 6.2. AWS CAF (Cloud Adoption Framework)
- Used to check cloud readiness for businesses
- A set of best practices, guidance, and tools that help organizations digitally transform and accelerate their cloud adoption
- Organize activities into six perspectives—business, people, governance, platform, security, and operations—to align cloud strategy with business goals
- The framework is built around a four-phase cycle: Envision, Align, Launch, and Scale

### 6.3. AWS Support Overview
- Basic - free and automatic, for personal and developer use.
- Paid option - all the resources, including unlimited tech support.
