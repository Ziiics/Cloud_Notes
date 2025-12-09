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
