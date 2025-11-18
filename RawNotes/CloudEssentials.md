### Cloud computing is the delivery of IT resources (servers, storage, databases, AI/ML tools, networking) over the internet with pay-as-you-go pricing.
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
