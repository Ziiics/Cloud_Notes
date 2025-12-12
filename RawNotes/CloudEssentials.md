# 1. Introduction to Cloud

### Cloud computing 
Cloud Computing is the delivery of IT resources (servers, storage, databases, AI/ML tools, networking) over the internet with pay-as-you-go pricing.
- Removes the need to buy hardware
- Let users rent resources only when needed (computing power, storage, server, databases, AI, ML tools, etc)
- Allows quick access to resources within seconds

### Cloud Deployment Types
- On-Cloud – everything runs on cloud infrastructure; highest scalability and least local hardware.
- On-Premises – everything runs on local servers; minimal or no use of cloud services.
- Hybrid / Multi-Cloud – mix of cloud + on-prem, or mix of multiple cloud providers; gives flexibility and redundancy.

### AWS Global Infrastructure
- AWS resources exist across many Regions and Availability Zones worldwide.
- This design provides redundancy, so if one area has an outage, another automatically takes over.
- This supports fault tolerance, high availability, and disaster recovery.







# 2. Compute in the Cloud

### Amazon EC2 and AMI (Amazon Machine Image)

EC2 provides Virtual Machines (instances) that run on shared physical hardware (multi-tenancy).
Users choose the operating system (Linux or Windows), storage, networking, and instance type.

EC2 Instance Families:
- General Purpose – balanced CPU/memory/network; good for small apps, web servers, code repos.
- Compute Optimized – strong CPU performance; used for ML inference, gaming servers, scientific tasks.
- Memory Optimized – large RAM; used for in-memory DBs, big data, analytics.
- Accelerated Computing – GPU/FPGA-based; used for ML training, graphics, heavy math.
- Storage Optimized – high disk throughput; used for large databases, warehousing, and I/O-heavy workloads.

AMIs (Amazon Machine Images) are blueprints of an EC2 instance, including OS, storage config, architecture, permissions, and preinstalled apps.
- Three ways to use AMIs: create your own, use available AWS AMIs, or purchase from AWS Marketplace.
- User Data allows you to run scripts automatically when the instance launches (e.g., install software).

### Interacting with AWS
AWS APIs – all AWS services communicate through APIs.
AWS CLI – lets you call these APIs in the terminal (create instances, manage S3, etc.).
AWS SDKs – let developers integrate AWS into applications using languages like Python, Java, C++, .NET.

### Different AWS pricing options:
- On-demand instances - pay only for the capacity you consume
- Reserved instances - get savings when committing to a 1-year or 3-year term for predictable workloads on specific instance families or AWS Regions.
- Spot instances - bid on spare compute capacity at up to 90% of the on-demand price, flexibility to be interrupted.
- Savings instances - save up to 72% by committing to a consistent usage level.
- Dedicated hosts - reserve entire physical server exclusively
- Dedicated Instances - pay for the instances running on hardware dedicated solely to your account

### Scaling & Load Balancing
Auto Scaling automatically adjusts the number of EC2 instances based on demand.
- Scalability = ability to handle increasing workloads
- Elasticity = automatically adding/removing resources as needed

Elastic Load Balancer (ELB) distributes traffic to multiple EC2 instances to prevent overload.
Routing methods include:
- Round Robin – evenly distributes
- Least Connections – sends traffic to the instance with the fewest active sessions
- IP Hash – same user goes to the same instance
- Least Response Time – chåooses fastest responding server

### Messaging & Decoupling

Messaging creates a buffer between application components so one failure doesn't break the entire system.
AWS messaging services:
- EventBridge – connects services using event-based communication
- SQS – queues messages until the receiving system can process them
- SNS – publish/subscribe notifications (email, SMS, push)

Monolithic apps = tightly connected; one failure affects the whole app.

Microservices = loosely connected; each component runs independently and failures are isolated.







# 3. Exploring Compute Services

### AWS Lambda
AWS Lambda is a serverless compute services, where you only run code without managing servers. This model is called Function as a Service (FaaS).
- Great for quick, event-driven process.
- Supports any programming language, as Java, Python, and Node.js.
- Integrates with other AWS services quite easily (S3, DynamoDB, EventBridge).
- Handles execution, scaling, and resources allocation.

How Lambda Works
1. upload code to Lambda (called Lambda function).
2. Set code to trigger from an event source.
3. Run code when triggered (reliable, secure, and efficient).
4. Pay only for the compute time used.

Example of use
- Real-time image processing for a social media application.
- Personalized content delivery for a news aggregator.
- Real-time event handling for an online game.

### Containers and Orchestration

Containers package code + dependencies into a portable, consistent environment that runs anywhere (like lightweight VMs).

Orchestration platforms handle:
- Starting/stopping containers.
- Scaling across multiple servers.
- Updating, monitoring, and maintaining container clusters.

AWS Container Options
- Amazon ECS (Elastic Container Service) - simpler, AWS-native orchestration; easier setup.
- Amazon EKS (Elastic Kubernetes Service) - uses Kubernetes (industry standard, open-source). Good for teams already using Kubernetes.

Orchestration gets the containers from Amazon ECR (Elastic Container Registry) to store the container images.

Fargate - serverless, AWS manages the servers, no need to manage servers or EC2 instances.

### Additional computer services

- Elastic Beanstalk - 
    Fully managed service that streamlines deployment, management, and scaling of web apps. Good for RESTful APIs, mobile backend services, microservices architectures with automated scaling and simplified infrastructure management.
- AWS Batch - 
    Fully managed service to run batch computing workloads. Automate schedules, process large-scale, parallel workloads in areas like scientific computing, financial task analysis, media transcoding, big data processing, ML training, and genomics research.
- Lightsail - 
    Offer VPS (Virtual Private Servers) at a predictable monthly price. Ideal for small businesses, basic workloads. 
- Outposts - 
    Fully managed hybrid cloud solution. Good for low-latency apps, data processing in remote locations, migrating and modernizing legacy apps, and meeting regulatory compliance or data residency requirements.







# 4. Going Global

When expanding globally, the main considerations are Region selection, edge locations, and how AWS maintains consistency across locations.
- Choose a Region based on compliance, proximity to users, feature availability, and pricing.
- Each Region has multiple Availability Zones (AZs) for redundancy.
- AZs help maintain high availability, fault tolerance, and disaster recovery.

### CloudFront 
CloudFront is a part of the Amazon Global Edge Network (CDN). It uses Edge Locations to cache content close to users.

### CloudFromation
AWS CloudFormation is an IaC (Infrastructure as Code) that can be used to define AWS Resources with text-based documents called CloudFormation templates. You can specify details on how exactly you want it to be built, maintaining consistent deployment.
  






# 5. Networking

### Consist of 
- Amazon VPC (Virtual Prrivate Cloud) - logically isolated section to launch AWS resources.
- Subnet - used to organize resources, can be public or private, always belongs to a specific AWS Region.
- Internet Gateway - Needed for resources in a VPC to access the internet.

### Different ways to conntect to AWS Cloud
- AWS Client VPN - advanced authentication, remote access, elastic and fully managed.
- AWS Site-to-Site VPN - creates secure and private corrention between on-prem networks and AWS.
- AWS Private Link - access AWS services privately without NAT, IGW, or public internet. Traffic jam is possible.
- AWS Direct Connect - uses dedicated private connection between network and VPC. It bypass the internet and reliable for massive data transfer.

### Additional gateway,
- AWS Transit Gateway - connect to VPC and on-premises networks through a central hub.
- NAT Gateway - connect instance in private subnet to outside
- Amazon API Gateway - manages and scales API (Application Programming Interface).
- Virtual Privaete Gateway - to connectprivate subnet in VPC to data center.

### NACL and Security Group (all is user responsibility)
- Network ACL - control traffic at the subnet level. Stateless so it will check all traffic without remembering its state.
- Security groups - control traffic at resource level. Deny all traffic by default unless stated otherwise. Stateful and will remember previous decisions for incoming packets. Fine grained.

### Other Resources
- Amaon Route53 - DNS that translate website name to IP address
- Amazon CloudFront - CDN (Content Delivery Network)
- AWS Global Accelerator - uses intelligent traffic routing and fast failover. Example use cases include global gaming company and financial services applications.







# 6. Storage

### Different type of storage,

#### 1. Block Storage
    Persistent, low-latency attached to EC2 instances llike physical hard drives. Deivid data into block. Can be encrypted, backed up, and modified while in use. 

    Two primary block storage services:
    - Amazon EC2 instance store - unmanaged non-persistent, high-speed local disk, not persistent (data lost when instance stops).
    - Amazon Elastic Block Store (EBS) - Persistent block storage attached to EC2, automatically replicated within an AZ, supports snapshots (incremental backups).

#### 2. Object Storage
    Keep data (called metadata) as object with its unique ID. To change part of data, you have to change the whole image, good for data that don't constantly change. 

    Primary service include S3: have 11 9's percent durability, unlimited storage, everything is private by default Features versioning, lifecycle management, various storage classes.

    S3 Storage Classes
    - Standard - for general purpose, quick retrieval for data accessed regularly, like dynamic websites.
    - Intelligent-Tiering - useful when data has unknown or changing access patterns. Have frequent access tier, infrequent, and archive instanct access tier. Data will ne moved to the most cost-effective storage tier.
    - Standard Infrequent Access (Standard IA) - access less frequently but require rapid access. Ideal for long-term backups, disaster recovery files.
    - Express One Zone - store data in a single AZ to deliver consistent single-digit milisecond data. Cost 80% less than S3 Standard.
    - Glacier Instant Retrieval - for data rarelyl accessed and requires milisecond retrieval.
    - Glacier Flexible Retrieval - for adat accessed 1-2 tiems per yeat, can be minutes to hours
    - Glacier Deep Archive - lowest cost, for long-term retention and default retrieval is 12 hours, retain data for 7-10 years or longer.
    - Outposts - deliver object storage to on-premises using Amazon S3 APIs and features.

    S3 Lifecycle configurations:
    - Transition actions: define when objects should transition to another storage class
    - Expiration actions: define when objects expire and should be permanently deleted.

#### 3. File Storage
    Shared file systems accessible over the network, can be accessed simultaneously. 

    Two primary file storage services:
    - EFS (Elastic File System) - operates usign NFS (Linux Network File System) protocol, multi-AZ redundancy, can be shared and accessed simlutaneously, and is elastic. Have different types.
    - FSx - fully managed file system, supports Windows File Server, Lustre, ONTAP, OpenZFS

#### 4. Hybrid Storage
    AWS Storage Gateway - fully managed, hybrid, unlimited cloud storage. Integrate on-remises env with AWS Cloud Storage. Imporved data management, local caching, and cost optimization.

    Gateway types,
    - S3 File Gateway - bridges local environemnt with Amazon S3, the cloud environment will look like regular local data.
    - Volume Gateway - create virtual storage volumes while maintaining local access to data. Types,
      - Cached mode - stores primary data in clodu while frwuent one is cached
      - Stored mode - locally keeps complete dataset while asynchronously backing it up to the cloud as EBS snapshots.
    - Tape Gateway - repalce physical tape infrastructure with virtual tape capabilities while benefitting from durability and scalability of AWS Cloud.

### AWS Shared responsiblity
- Fully managed - customer responsible for customer data and client-side data encryption only.
- Managed services - additional of server-side encryptiona nd network traffic protection also becomes customer responsibility.
- Unmanaged services - The responsibility of managed service plus platform and apps management, OS, network, and firewall configuration.

### Amazon Data Lifecycle Manager - to define policies to help automate snapshot lifecucle amnagement. The steps are,
1. Create an EBS snapshots policy
2. Elect target resource types (can either be ENS volume or EC2 instance)
3. Exclude volume, narrow down the data to be included in the snapshots
4. Set custom schedules
5. Apply additional actions, as tags or corr-account sharing, etc.







# 7. Databases

### Amazon RDS (Relational Database)
- Relational Databases uses structured query language, SQL. 
  - Offer Multi-AZ deployment and automated backups, can also uses BD snapshots for manual.
  - Provide network isolation, encryption in transit, and encryption at rest.
  - Support engines as MySQL, PostgreSQL, MariaDB, Oracle, and SQL Server.
- Aurora 
  - AWS-managed relational database compatible with MySQL and PostgreSQL
  - Auto-scales to handle high workloads
  - Replicates data across multiple AZs for high availability
  - Delivers high performance with lower operational overhead

### NoSQL Databases
Non-relational database that uses Key-Value pairs, documents, or wide-column format.
- DynamoDB - fully managed NoSQL, incredibly fast, ideal for high performance and seamless scaling apps.

### In-memory Caches
ElastiCache is a fully managed in-memory caching service.
- Fully managed in-memory cache service (supports Redis and Memcached)
- Speeds up application performance by reducing load on databases
- Automatically detects and replaces failed nodes
- Ideal for session caching, leaderboards, real-time analytics

### Additional Databse services
- DocumentDB - handle semistructured data where information doesn't conform to rigid relational schemas. Compatible with MongoDB.
- AWS Backup - streamlines data protection across various AWS resources and on-premises deployment in single dashboard.
- Neptune - fully managed, urpose-built graph database to manage highly connected data sets.









# 8. AI ML and Data Analytics

### AI and Machine Learning
- AI (Artificial Intelligence) - focused on development of intelligetn computer systems capable of performing humanlike tasks.
- ML (Machine Learning) - type of AI for training machines to perform complex tasks without explicit instructions.

### AWS AI/ML tiers solution

#### 1. AI services - pre-built models trained for specifc functions. Some examples include:
    For language services:
    - Amazon Comprehend (interpret document text to a menaingful one)
    - Amazon Polly (convert text to lifelike speech)
    - Amazon Transcribe (convert speech into text)
    - Amazon Translate (text translation service)
    For computer vision and search services:
    - Amazon Kendra (search answer within large amount of neterprise content)
    - Amazon Rekognition (video analysis service)
    - Amazon Textract (extracts typed and handwritten text)
    Conversational AI and personalization services
    - Amazon Lex (add voice and text conversational to apps)
    - Amazon Personalize (use historical data to personalized recommendation)

#### 2. ML services - customized approach with Amazon SageMaker AI where you build, train, and deploy your own ML model.

- Amazon SageMaker AI: can be done wiht IDE or no-code interfacem fully managed infrastructure, and repeatable ML workflows

#### 3. ML frameworks and infrastructure - completely custom approach to building models using purpose-built chips
- ML framework is software librarry or tool that provides experienced ML practitioners with pre-built
- AWS ML infrastructure uses ML-optimized EC2, EMR, and ECS to support these solution.

### Deep Learning and Generative AI

- Deep Learning - a subset of ML where modelsa re trained using layers of artificial neurons that mimic the human brain. 
- Generative AI - deep learning powered by large ML known as foundation models (FMs). LLMs are a popular type of FM traied to use human language.
  - Amazon SageMaker JumpStart - ML hub with FMs and pre-built ML solutiotns deployable with a few clicks. Used for Rapid ML model deployment, custom fine-tuned solutions, ML experiments and prototypes.
  - Amazon Bedrock - fully managed service for adapting and deploying FMs. Used for Enterprise-grade generative AI, multimodel content generation, and advanced conversational AI.
  - Amazon Q - interactive AI assisstant that can be integrated with company's repositories. Hae for Business and Developer.

### Data Analytics
Tranformation of raw data to uncover valuable insights and trends.

#### Data apipelines for ETL (eExtract, Transform, Load) process:
1. Store the data. Some Data Storage services include,
    - Amazon S3 - popular choice for data lakes. Securely house virtually unlimited structured or unstructured data.
    - Amazon Redshift - fully managed data warehouse service that store petabytes of structured and semistructured data.
2. Extract from various sources or Data ingestion. Some Data ingestion services,
    - Amazon Kinesis Data Streams - for real-time ingestion of terabytes of data.
    - Amazon Data Firehouse - near real-time, fully managed service provide auto provisioning and scaling.
3. Transform into consistent, usable format for downstream tools. Data processing services,
    - AWS Glue - fully managed, simple, fast, and cost effective.
    - Amazon EMR - ideal for large-scale data processing and organizastions, auto infrastructure provisioning, cluster management, scaling. Supports Apache Spark, Apache Hadoop, and Apache Hive.
4. Load into destination system, like data warehouse or analytics platform. Data cataloging services,
    - AWS Glue Data Catalog - centralized, scalable, and managed metadata repository that enhances data discovery. 
5. Getting the analyzed data. Data analysis and visualization services,
    - Amazon Athena - run SQL queries to analyze data in relational, nonrelational, object, and custom data sources.
    - Amazon Redshift - fully managed data warehouse solution. have massively parallel processing architecture and columnar storage.
    - Amazon QuickSight - can be used for both technical and non-technical users.
    - Amazon OpenSearch Service - search for relevant content throguh precise keyword matching or natural language queries.








# 9. Security

### Authentication and Authorization
- Authentication - verifying the identity of user or entity through credentials
- Authorization - grants user certain access rights and permissions.

AWS Shared Responsibility Model 
- Customer is responsible to security in the AWS services and cloud.
  - AWS provided security mechanism: Prevent, Protect, and Detect and respond.
- AWS is responsible of the security of the cloud itself.

### AWS IAM, Secrets Manager, and Systems Manager
IAM (Identity and Access Management) 
  - By default, All actions are denied. Must explicitly grant permission.
  - Permission can be grant by groups, users, or roles. 
  - IAM Identity Center is specifically designed to help organizations implement single sign-on for AWS resources using their existing identity providers.
Secret Manager
  - Managed, rotate, and retrieve credentials, API keys, and other secrets.
Systems Manager
  - Provide centralized view across organizastion's accounts and Regions and multi-cloud and hybrid environment.

AWS protection through services
- AWS Shield Standard - auto protect AWS customers from most commmon DDoS attacks at no cost.
- AWS WAF - web apps firewall that monitors network requests that come into web apps.

To protect data, AWS uses
- AWS Key Management Service (AWS KMS) - create and manage cryptographic keys to encryp and decrypt data
- Amazon Macie - monitor sensitive daat at rest to make sure it's safe
- AWS Certificate Manager (ACM) - centralizes managermenmt of SSL/TLS certificates that provide data encryption in transit.

### Detection and response services
- Amazon Inspector - imporvde security and compliance of applications by running auto security assessmsent for EC2 instances, containers, and Lmabda functions.
- Amazon GuardDuty - provides intellident threat detection across all infrastructure and resources.
- Amazon Detective - to further investigae the root cause of threat that has been detected.
- AWS Security Hub - brings multiple secuirty services together to single place and format.









# 10. Monitoring, Compliance, and Governance in AWS Cloud

### The progression to effectively monitor AWS Cloud solutions are,
1. Securing systems - to protect data, sysgtems, and infrastructure from unauthorized access.
2. Monitoring activities - continuously observe and analyze system activity, network traffic, and security events.
   - Amazon CloudWatch can be used to monitors AWS reousrces and the applications you run on AWS in real time. The features include metrics, alarms, dashboards, and logs.
3. Conducting audits - periodically review and assess the effectiveness of seucriy controls and check requirements.
   - AWS CloudTrail - tracks user activity and API usage in AWS Cloud, on premises, and even with other cloud providers. Have three categories: events, logs, and insights.
4. Ensuring compliance - ensrue practices and controls emet requirements of relevant regulations and industry standard.
   - AWS Artifact - provides no-cost, on-demand access to AWS security and compliance reports and select online agreements.
   - AWS Compliance portal can also be used to see how other cusotomer solved various compliance, governance,a nd audit challenges.

### Following guidelines for different AWS resources
- AWS Config - assess, audit, and evaluate configurations of AWS resources, can create reports.
- AWS Audit Manager - continually audits AWS usage to simplify risk and compliance assessment.
- AWS Organizations - centrally manage and govern environemnt as AWS resources grow and scale. Can be used to automate AWS acount create, providing tools and accesss, and controlling user access. Can control based on OU and individual member account.
- AWS Cloud Tower - use preconfigured controls to enforce and manage governance rules for seucirty, operations, and compliance at scale. Used to quickly deplou apps and provision compliant AWS accounts.
- AWS Service Catalog - create, share, and organize from a curated caatlog of AWS resources. Used to provision resources across AWS accounts, apply access controls,and accelerate provisioning of CI/CD pipelines.
- AWS License Manager - helps manage software license and fine-tune licensing costs. Use it to streamlin license management and simplogy experience, automate the distributiona nd activation of software entitlements across AWS accounts.

### Operational Health & Best Practices
- AWS Health Dashboard - view account-specific health information and get AWS Health event updates. It gives you timely and actionable guidance to remedy issues. It also helps manage service health and is integrated and automated to use at scale.
- AWS Trusted Advisor helps you align with AWS best practices, prioritize recommendations, and optimize your AWS resources at scale. Can continuously evaluate your AWS environment by using best practice checks across several categories.
- AWS IAM Access Analyzer provides benefits like refining permissions, validating IAM policies, helping you meet your least privilege goals, and automating IAM policy reviews.









# 11. Pricing and Support

### Different pricing concept
- Pay as you go - adapt to changing business needs and reduce the risk of changes.
- Save when you commit - offer savings when commit to a 1-year ot 3-year plan.
- Pay less by using more - the more you use, the less you pay

Driving factors of cost include the computer power, storage, and data transfer amount.

### AWS pricing and billing services and tools

1. AWS Organizations 
   - centralized management of AWS environments,
   - Can create, group, and manage accounts, apply security policies,
   - Consolidate billing with multiple account using single payment method.
2. AWS Billing and Cost Management Dashboard
   - Centralizes cost management, show current charges, usage, forecastsm and detailed breakdown,
   - Help visualize spending
3. AWS Budgets
   - Custom budgets and sends alerts when Savings Plans and Reserved Instances (RIs) utilization exceed.
4. AWS Cost Explorer
   - Analyze historical spending trends wiht interactive graph
   - Forecast future AWS costs based on current usage
5. AWS Pricing Calculator
   - web-based planning tool for estimation on prices
   - useful to compare costs

### Different Support Plans
| Support Type | Details | Included checks | Technical Account Management (TAM) |
| --- | --- | --- | --- |
| Basic Support | Included already (access to documentation is a support too) | only Core AWS Trusted Advisor | not included |
| Developer Support | Response time is 12-24 hours | only Core AWS Trusted Advisor | not included |
| Business Support | For minimum production, 1-4 hours response time | Full set | not included |
| Enterprise On-Ramp Support | For minimum production and critical, 1-4 hours response time, 30-mins when business-critical system is down | Full set | A pool to provide proactive guidance |
| Enterprise Support | For minimum production and critical, 1-4 hours response time, 15-mins when business-critical system is down | Full set and prioritized | Designated TAM for consultative architectural and opreational guidance |

### AWS Marketplace and Partner Network 

Solutions and services offered in AWS Marketplace include,
- SaaS (Software as a service) - for business apps, marketing tools, and collaboration tools.
- ML and AI - prebuilt models for image recognition, ML algorithm.
- Data and Analytics - business intelligence platforms for visualization and reporting.

AWS Partner Nework (APN) - global community that uses AWS tech, programs, and tools to build solutions and services for customer. The benefit of becoming one are: funding, AWS Partner events, training and certifications.









# 12. Migrating to the AWS Cloud

### Phases of migration process
1. Assess - assess organization readiness to opreate in cloud. Tools: Migration Evaluator
2. Mobilize - create migration plan and address gaps. Tools: 
   - AWS Application Discovery Service - gathers config, performance, and connection details of both servers and database on-premises to create detailed migration plan.
   - AWS Migration Hub - centralized hub to assess, plan, implmeent, and track migration.
3. Migrate and modernize - get things moving. Tools:
   - For Migration: 
     - AWS Application Migration Service - migrate and improve on-premises and cloud-based applications.
     - AWS Database Migration Service - to migrate database.
   - For Data Transfer: AWS DataSync, AWS Transfer Family, AWS Snow Family.

AWS Rpofessional Services team created AWS CAF (Cloud Adoption Framework) to help migration. The six focused areas to consider when migration include: the business, people, governance, platform, security, and operations.

### Seven Migration  (also called 7 Rs)
1. Relocate - change hosting location to cloud
2. Rehost - moving application without changes
3. Replatform - make cloud optimization
4. Refactor - reimagining, add features, scale, and improve
5. Repurchase - moving from tranditional license to SaaS model
6. Retain - keeping apps in the source environment
7. Retire - remove uneeded applications

### Migrating Database

- Homogeneous migration - migrating data from and to the same database engine.
- Heterogeneous migration - transfering to different engine.

AWS Services that helps with migration:
- AWS DMS (Database Migration Service) - virtual machine that runs replication software. Supports both homogenous and heterogeneous migrations.
- AWS SCT (Schema Conversion Tool) - able to coonvert source database schema and code into oen that compatible with target database.

Transferring data can be done online or offline. 
1. Online Data Trasnfer
   - AWS DataSync - automate data transfer, useful when archiving cold data and managing hybrid data workflows.
   - AWS Transfer Family - fully managed support for secure file transfer over FTP, SFTP, and FTPS, etc
   - AWS Direct Connect - establish dedicated private connection between your network to VPC for data transfer.
2. Offline Data Transfer
   - AWS Snowball Edge Storage Optimized devices - deliver high performance NYMe storage.




# 13. Well-Architected Solutions