# 1. Introduction to Cloud

### Cloud computing 
Cloud Computing is the delivery of IT resources (servers, storage, databases, AI/ML tools, networking) over the internet with pay-as-you-go pricing.
- Removes the need to buy hardware
- Lets users rent resources only when needed (computing power, storage, server, databases, AI, ML tools, etc)
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
- Accelerated Computing – GPU/FPGA based; used for ML training, graphics, heavy math.
- Storage Optimized – high disk throughput; used for large databases, warehousing, I/O-heavy workloads.

AMIs (Amazon Machine Images) is blueprint of an EC2 instance including OS, storage config, architecture, permissions, and preinstalled apps.
- Three ways to use AMIs: create your own, use available AWS AMIs, purchase form AWS Marketplace.
- User Data allows you to run scripts automatically when the instance launches (e.g., install software).

### Interacting with AWS
AWS APIs – all AWS services communicate through APIs.
AWS CLI – lets you call these APIs in the terminal (create instances, manage S3, etc.).
AWS SDKs – lets developers integrate AWS into applications using languages like Python, Java, C++, .NET.

### Differnet AWS pricing options:
- On-demand instances - pay only for the capacity you consume
- Reserved instances - get savings when committin to a 1-year or 3-year term for predictable workloads on specific instances family or AWS Regions.
- Spot instances - bid on spare compute capacity at up to 90% of the on-demand price, flexibility to be interrupted.
- Savings instances - save upt o 72% by commiting to consistent usage level.
- Dedicated hosts - reserve entire physical server exclusively
- Dedicated Instances - pay the instances running on hardware dedicated solely to your account

### Scaling & Load Balancing
Auto Scaling automatically adjusts the number of EC2 instances based on demand.
- Scalability = ability to handle increasing workloads
- Elasticity = automatically adding/removing resources as needed

Elastic Load Balancer (ELB) distributes traffic to multiple EC2 instances to prevent overload.
Routing methods include:
- Round Robin – evenly distributes
- Least Connections – sends traffic to the instance with fewest active sessions
- IP Hash – same user goes to same instance
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
2. Set code to trigger form an event source.
3. Run code when triggered (reliable, secure, and efficient).
4. Pay only for the compute time used.

Example of use
- Real-time image processing for a social media applciation.
- Personalized content delivery for a news aggregator.
- Real-time even handling for an online game.

### Containers and Orchestration

Containers package code + dependencies into a portable, consistent environment that runs anywhere (like lightweight VMs).

Orchestration platforms handle:
- Starting/stopping containers.
- Scaling across multiple servers.
- Updating, monitoring, and maintaining container clusters.

AWS Container Options
- Amazon ECS (Elastic Container Service) - simpler, AWS-native orchestration; easier setup.
- Amazon EKS (Elastic Kubernetes Service) - uses Kubernetes (industry standard, open-source). Good for teams already using Kubernetes.

Orchestration get the containers from Amazon ECR (Elastic Container Registry) to stores the container images.

Fargate - serverless, AWS manages the servers, no need to manage servers or EC2 instances.

### Additional computer services

#### Elastic Beanstalk 
Fully managed service that streamlines deployment, management, and scaling of web apps. Good for RESTful APIs, mobile backend services, microservices architectures with automated scaling and simplified infrastructure management.

#### AWS Batch
Fully managed service to run batch computing workloads. Automate schedules, process large-scale, parallel workloads in areas like scientific computing, financial task analysis, media transcoding, big data processing, ML training, and genomics research.

#### Lightsail
Offer VPS (Virtual Private Serves) at a predictable monthly pricing. Ideal for small businesses, basic workloads. 

#### Outposts
Fully managed hybrid cloud solution. Good for low-latency apps, data pricessing in remote locations, migrating and modernizing legacy apps, and meeting regulatory compliance or data residency requirements.