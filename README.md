# aws-solutions-architect-associate-notes
## Contents
### Compute services
- [EC2](#ec2)
- [Lambda](#lambda)
- [Elastic Beanstalk](#elastic-beanstalk)
- [Elastic Container Service](#elastic-container-service)
- [Elastic Container Registry](#elastic-container-registry)
- [Elastic Kubernates Service](#elastic-kubernates-service)

### High availability and scalability 
 - [Eastic Load Balancer](#elastic-load-balancer)
 - [Auto Scaling Group](#auto-scaling-group)

### Storage
- [S3](#s3)
- [EBS](#ebs)
- [EFS](#efs)
- [Instance Store](#instance-store)
- [FSx](#fsx)
- [Storage Gateway](#storage-gateway)
- [Aws backup](#aws-backup)

### Database
- [RDS](#rds)
- [Amazon Aurora](#amazon-aurora)
- [DynamoDB](#dynamodb)
- [DocumentDB](#documentdb)
- [ElastiCache](#elasticache)
- [Amazon Neptune](#amazon-neptune)
- [Amazon QLDB](#amazon-qldb)
- [Amazon Timestream](#amazon-timestream)

### Decoupling applications 
- [SQS](#sqs)
- [SNS](#sns)
- [Kinesis](#kinesis)
- [Amazon MQ](#amazon-mq)
- [Event Brigde](#event-bridge)

### Data & Analytics
- [Athena](#athena)
- [Redshift](#redshift)
- [OpenSearch](#opensearch)
- [EMR](#emr)
- [QuickSight](#quicksight)
- [Glue](#glue)
- [Lake formation](#lake-formation)
- [Kinesis Data analytics](#kinesis-data-analytics)
- [MSK Managed Streaming for Apache Kafka](#msk-managed-streaming-for-apache-kafka)
- [Big Data Ingestion Pipeline](#big-data-ingestion-pipeline)

###  Migration & Transfer
- [Snow Family](#snow-family)
- [DataSync](#datasync)
- [Transfer Family](#transfer-family)
- [Database Migration Service](#database-migration-service)
- [Application migration service](#application-migration-service)
- [RDS and Aurora MySQL Migrations](#rds-and-aurora-mysql-migrations)

### Disaster Recovery 
- [Disaster Recovery](#disaster-recovery)

### Machine Learning
- [Rekognition](#rekognition)
- [Transcribe](#transcribe)
- [Polly](#polly)
- [Translate](#translate)
- [Lex](#lex)
- [Comprehend](#comprehend)
- [Comprehend Medical](#comprehend-medical)
- [SageMaker](#sagemaker)
- [Forecast](#forecast)
- [Kendra](#kendra)
- [Personalize](#personalize)
- [Textract](#textract)

### Networking
- [Route 53](#route-53)
- [API Gateway](#api-gateway)
- [VPC](#vpc)
- [PrivateLink](#privatelink)
- [Site-to-Site VPN](#site-to-site-vpn)
- [Direct connect](#direct-connect)
- [Transit Gateway](#transit-gateway)
- [Networking Costs](#networking-costs)

### Content delivery
- [CloudFront](#cloudfront)
- [Global Accelerator](#global-accelerator)

### Monitoring & Audit
- [CloudWatch](#cloudwatch)
- [CloudTrail](#cloudtrail)
- [Config](#config)
- [Trusted Advisor](#trusted-advisor)
- [Cost explorer](#cost-explorer)

### Access Management 
- [Identity Access Management](#identity-access-management)
- [AWS Organizations](#aws-organizations)
- [SSO](#sso)
- [Cognito](#cognito)
- [AWS Directory Services](#aws-directory-services)
- [AWS Control Tower](#aws-control-tower)


### Parameters & Encryption
- [Key Management Service](#key-management-service)
- [SSM Parameter Store](#ssm-parameter-store)
- [Secrets Manager](#secrets-manager)
- [Certificate Manager](#certificate-manager)

### Cloud Security
- [Web Application Firewall](#web-application-firewall)
- [AWS Shield](#aws-shield)
- [Firewall Manager](#firewall-manager)
- [GuardDuty](#guardduty)
- [Inspector](#inspector)
- [Macie](#macie)
- [Network Firewall](#network-firewall)

### HPC
- [High Performance Computing](#high-performance-computing)

### Docs

[AWS Well Architected](https://aws.amazon.com/fr/architecture/well-architected)

[AWS reference architectures](https://aws.amazon.com/fr/architecture/)

[AWS architecture solution](https://aws.amazon.com/fr/solutions/)

[AWS Disaster Recovery](https://aws.amazon.com/fr/disaster-recovery/)

[other ressources](https://drive.google.com/file/d/1Qo4DJFxyYwuhjLfJ24oXvA3bmG9Cvfnw/view)
[Tips](https://www.toptal.com/aws-cloud-engineers/aws-certified-solutions-architect-exam-tips)

# Compute services

## EC2 

- EC2 (Elastic Compute Cloud) is an  __Infrastructure as a Service (IaaS)__
- Storage space:
   - Network attached __(EBS & EFS)__
   - Direct attached(Hardware) __(EC2 Instance Store)__
- Firewall rules: __security group__
- Static IPv4 addresses known as Elastic IP addresses
- Bootstrap script (Execute only at first launch): EC2 User Data
- MetaData is data about your EC2 instance 
- This can include information such as private IP address, public IP address, hostname, security groups, etc.
- __Url to fetch metadata about the instance (http://169.254.169.254/latest/meta-data)__

__IAM Roles for EC2 instances__

- Never enter AWS credentials into the EC2 instance, instead attach IAM Roles to the instances

__EC2 Instance Types__

You can use different types of EC2 instances that are optimised for different use cases\

__General Purpose__
 - Great for a diversity of workloads such as __web servers or code repositories__
 - Balance between __Compute, Memory, Networking__
__Compute Optimize__
 - Great for compute-intensive tasks that require high performance processors:
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing (HPC)
  - Scientific modeling & machine learning
  - Dedicated gaming servers

__Memory Optimized__
 - Fast performance for workloads that process large data sets in memory 
 - Distributed web scale cache stores

__Storage Optimized__
 - Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage 
 - High frequency online transaction processing (OLTP) systems
 - Cache for in-memory databases (for example, Redis)
 - Data warehousing applications

__Security group__
- Security groups are acting as a “firewall” on EC2 instances
- They regulate: 
- Access to Ports
- Authorised IP ranges – IPv4 and IPv6
- Control of inbound network (from other to the instance)
- Control of outbound network (from the instance to other)
- All inbound traffic is __blocked__ by default
- All outbound traffic is __allowed__.
- __It’s good to maintain one separate security group for SSH access__
- If your application is not accessible (time out), then it’s a security group issue
- If your application gives a “connection refused“ error, then it’s an application error or it’s not launched

__EC2 Instances Purchasing Options__

__On Demand__
- Pay per use (no upfront payment)
- Has the highest cost but no upfront payment
- No long-term commitment
- Recommended for __short-term__ and __un-interrupted workloads__, where you can't __predict__ how the application will behave

__Reserved Instances__

- __Predictable Usage__, Applications with steady state or predictable usage
- __Specific Capacity Requirements__, Applications that require reserved capacity.
- __Pay up Front__ You can make upfront payments to reduce the total computing costs even further
- __Standard RIs__ Up to 72% off the on-demand price.
- __Convertible RIs__ Up to 54% off the on-demand price. Can change the instance type
- __Scheduled RIs__ Launch within the time window you define. Match your capacity reservation to a predictable recurring schedule that \
only requires a fraction of a day, week, or month.

__EC2 Savings Plans__
- Get a discount based on long-term usage (up to 72% - same as RIs)
- Commit to a certain type of usage ($10/hour for 1 or 3 years)
- Usage beyond EC2 Savings Plans is billed at the On-Demand price
- Flexible across: Instance size. 
- Commit to a certain type of usage ($10/hour for 1 or 3 years, OS, Tenancy(Host, Dedicated, Default)

__EC2 Spot Instances__
- Can get a discount of up to 90% compared to On-demand
- Instances that you can “lose” at any point of time if your max price is less than the current spot price
- The MOST cost-efficient instances in AWS
- Useful for workloads that are resilient to failure
- Not suitable for critical jobs or databases
- __Spot Block__“block” spot instance during a specified time frame (1 to 6 hours) without interruptions
- You can only cancel Spot Instance requests that are __open, active, or disabled__. 
- To terminate spot instance You must first cancel a Spot Request, and then terminate the associated Spot Instances.

__EC2 Dedicated Hosts__
- A physical server with EC2 instance capacity fully dedicated to your use
- Allows you address compliance requirements and use your existing server- bound software licenses 
- The most expensive option
- Useful for software that have complicated licensing mode 
- Or for companies that have strong regulatory or compliance needs

__EC2 Capacity Reservations__
- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- You’re charged at On-Demand rate whether you run instances or not

__Elastic IP__
- If you need to have a fixed public IP for your instance, you need an Elastic IP
- An Elastic IP is a public IPv4 IP you own as long as you don’t delete it
- You can attach it to one instance at a time 
- With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
- You can only have 5 Elastic IP in your account

__Placement Groups__
3 types of placements groups : Cluster, Spread, Partition

__Cluster__
- Grouping of instances within a single Availability Zone, same hardware
- Recommended for applications that need low network latency, high network throughput, or both.

__Spread__

- A spread placement group is a group of instances that are __each placed on distinct underlying hardware__.
- Recommended for applications that have a small number of critical instances that should be kept separate from each other
- Multi AZ, same region
- max 7 instances per group per AZ
- __Reduce risk of simulataneous failure__

__Partition__
- Each partition placement group has its own set of racks. Each rack has its own network and power source. 
- Multiple AZs in the same region
- Up to 7 partitions per AZ
- Up to 100s of EC2 instances
- __Isolate from failure__

__Networking with EC2__

You can attach 3 different types of __virtual networking cards__ to your EC2.

__ENI(Elastic Network Interface)__
- An ENI is simply a virtual network card that allows:
- Private IPv4 addresses 
- Public Ipv4 Address
- Many IPV6
- One Elastic IP (IPv4) per private IPv4
- Mac Address
- 1 or More SG
- You can create ENI independently and attach them on the fly (move them) on EC2 instances for failover
- Bound to a specific availability zone (AZ)

__EN(Enhanced Networking)__
_ For High Performance Networking between __10 Gbps to 100 Gbps__
- Single Root I/O Virtualization (SR-IOV) provides higher I/O performance and lower CPU utilization
- Depending on your instance type, enhanced networking(EN) can be enable using :

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1. __ENA (Elastic Network Adapter)__ Supports network speeds of up to __100 Gbps__ for supported instances types\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2. __VF (Virtual Function) interface__ Supports network speeds of up to __10 Gbps__ for supported instance types Typically used on older instances

__EFA(Elastic fabric Adapter)__
- For when you need to accelerate High Performance Computing (HPC) and machine learning applications 
- Or if you need to do an __OS-bypass__
- OS-bypass enables HPC and machine learning applications to bypass the operating system kernel and communicate directly with the EFA device
- Not currently supported with Windows — only Linux.

__Hibernation__

- The in-memory (RAM) state is preserved
- The instance boot is much faster! (the OS is not stopped / restarted)
- Under the hood: the RAM state is written to a file in the root EBS volume
- The root EBS volume must be encrypted
- __Instance RAM Size – must be less than 150 GB.__

## Lambda

- Virtual functions – no servers to manage!
- Limited by time - __short executions__
- Run __on-demand__
- Scaling is __automated__
- __Not good for running containerized applications__

__Lambda Limits__
- __Execution__
  - Memory allocation: __128 MB – 10GB__
  - Maximum execution time: __900 seconds (15 minutes)__
  - Environment variables: __4KB__
  - Disk capacity in function container (/tmp): 512 MB to 10GB 
  - Concurrency executions: 1000 (can be increased)
- __Deployment__
  - Lambda function deployment size (compressed .zip): 50 MB  
  - Size of uncompressed deployment (code + dependencies): 250 MB
  - Size of environment variables: 4 KB

__Lambda@Edge__
- Deploy Lambda functions alongside your CloudFront CDN for computing at edge locations
- Customize the CDN content using Lambda at the edge location (responsive)
- No server management (Lambda is deployed globally)
- Can be used to modify CloudFront requests & responses

![image](https://user-images.githubusercontent.com/35028407/226636397-3fdc7d54-56ab-4082-b163-c0facba57cf3.png)

__Networking__
- By default, your Lambda function is launched outside your own VPC (in an AWS owned VPC)
- __Therefore, it cannot access resources in your VPC (RDS, ElastiCache, internal ELB…)__
- To enable your Lambda function to access resources inside your private VPC, 
- You must define the VPC ID, the Subnets and the Security Groups
- Lambda will create an ENI (Elastic Network Interface) in your subnets

<img width="527" alt="Capture d’écran 2023-03-21 à 15 37 02" src="https://user-images.githubusercontent.com/35028407/226640425-234beb72-ef9b-479a-8667-e3b1f0f47bae.png">


## Elastic Beanstalk

- Used to deploy applications on AWS infrastructure
- __Platform as a Service (PaaS)__
- Automatically handles capacity provisioning, load balancing, scaling, application health monitoring, instance configuration, etc. but we have full control over the configuration
- Free (pay for the underlying resources)
- Supports versioning of application code
- Can create multiple environment (dev, test, prod)
- __Web & Worker Environments__
  - __Web Environment (Web Server Tier)__: clients requests are directly handled by EC2 instances through a load balancer.
  - __Worker Environment (Worker Tier)__: clients’s requests are put in a SQS queue and the EC2 instances will pull the messages to process them. Scaling depends on the number of SQS messages in the queue.
  
  ![image](https://user-images.githubusercontent.com/35028407/226097784-f6f083bf-cdc1-4f85-b9e6-bc38c76b45d3.png)


## Elastic Container Service

- AWS managed container orchestration platform
- Launch Docker containers on AWS = Launch __ECS Tasks__ on __ECS Clusters__
- __EFS__ is used as persistent multi-AZ shared storage for ECS tasks

__Launch Types__

__EC2 Launch Type__
- __Not Serverless__
- __you must provision & maintain the infrastructure (the EC2 instances)__
- EC2 instances have __ECS agent__ running on them as a __docker container__
- AWS takes care of starting / stopping containers

__Fargate Launch Type__
- __Serverless__
- You do not provision the infrastructure (no EC2 instances to manage)
- You just create task definitions
- AWS just runs ECS Tasks for you based on the CPU / RAM you need
- To scale, just increase the number of tasks

__IAM Roles for ECS__
- __EC2 Instance Profile (EC2 Launch Type only):__
  - Used by the ECS agent
  - Makes API calls to ECS servic
  - Pull Docker image from ECR
  - Reference sensitive data in Secrets Manager or SSM Parameter Store
- __ECS Task Role:__
  - Allows ECS tasks to access AWS resources
  - Each task can have a separate role
  - Use different roles for the different ECS Services
  - Task Role is defined in the task definition

__Data Volumes (EFS)__
- Mount EFS file systems onto ECS tasks
- Works for both __EC2__ and __Fargate launch types__
- Tasks running in any AZ will share the same data in the EFS file system
- __Fargate + EFS = Serverless__


__ECS Service Auto Scaling__
- Automatically increase/decrease the desired number of ECS tasks
- Amazon ECS Auto Scaling type:
- Amazon ECS Auto Scaling uses __AWS Application Auto Scaling__
  - Metric :
    - ECS Service Average CPU Utilization
    - ECS Service Average Memory Utilization - Scale on RAM
    - ALB Request Count Per Target – metric coming from the ALB  
- __Scaling type:__
  - __Target Tracking__ – scale based on target value for a specific CloudWatch metric 
  - __Step Scaling__ – scale based on a specified CloudWatch Alarm
  - __Scheduled Scaling__ – scale based on a specified date/time (predictable changes)

- ECS Service Auto Scaling (task level) ≠ EC2 Auto Scaling (EC2 instance level)
- __Fargate Auto Scaling__ is much easier to setup (__because Serverless__)

__EC2 Launch Type – Auto Scaling EC2 Instances__

- Accommodate ECS Service Scaling by adding underlying EC2 Instances
- 2 type:
  -  __Auto Scaling Group__ Scaling 
    - Scale your ASG based on CPU Utilization
    - Add EC2 instances over time
  - __ECS Cluster Capacity Provider__
    - Used to automatically provision and scale the infrastructure for your ECS Tasks
    - Capacity Provider paired with an Auto Scaling Group
    - Add EC2 Instances when you’re missing capacity (CPU, RAM…)  


<img width="1171" alt="Capture d’écran 2023-03-21 à 10 37 51" src="https://user-images.githubusercontent.com/35028407/226567639-87fab409-5068-4460-89d3-b277b4fa924d.png">


## Elastic Container Registry

- Store and manage Docker images on AWS
- Private and Public repository (Amazon ECR Public Gallery)
- Fully integrated with ECS, backed by Amazon S3
- Access is controlled through IAM policy

## Elastic Kubernates Service

- Used to launch __Kubernetes (open-source) clusters__ on AWS
- __Supports both EC2 and Fargate launch types__
- Inside the __EKS cluster__, we have __EKS nodes (EC2 instances)__ and __EKS pods (tasks)__ within them. We can use a private or public load balancer to access these EKS pods.
- EKS is an alternative to ECS
- Node Types
  - __Managed Node Groups__ 
    - Creates and manages Nodes (EC2 instances) for you
    - Nodes are part of an ASG managed by EKS
  - __Self-Managed Nodes__ 
    - Nodes created by you and registered to the EKS cluster and managed by an ASG
    - You can use prebuilt AMI - Amazon EKS Optimized AMI
  - __AWS Fargate__
    - No maintenance required; no nodes managed 


![image](https://user-images.githubusercontent.com/35028407/226579427-81fcabdc-0dcd-4bdf-a982-e2b9bc33464b.png)



# High availability and scalability 

- __Vertical Scaling__: Increase instance size (= scale up / down)
    - From: t2.nano - 0.5G of RAM, 1 vCPU
    - To: u-12tb1.metal – 12.3 TB of RAM, 448 vCPUs
    - Hardware limit
    - Use case : Non distribuate system like database
    
- __Horizontal Scaling__: Increase number of instances (= scale out / in)   
   - Auto Scaling Group
   - Load Balancer

- __High Availability__
  - Run instances for the same application across multi AZ
  - Auto Scaling Group multi AZ
  - Load Balancer multi AZ

## Elastic Load Balancer

- Spread load across multiple EC2 instances
- Supports Multi AZ
- Expose a single point of access (DNS) to your application
- Do regular health checks to your instances
- Enforce stickiness with cookies
- High availability across zones
- Separate public traffic from private traffic

__Types__
- __Classic Load Balancer (CLB) - deprecated__
  - __Load Balancing to a single application__
  - Supports HTTP, HTTPS (layer 7) & TCP (layer 4), SSL
  - Health checks are HTTP or TCP based
  - Provides a fixed hostname (xxx.region.elb.amazonaws.com)

- __Application Load Balancer (ALB)__
  - Load balancing to multiple applications (target groups) based on the request parameters
  - Operates at Layer 7 (HTTP, HTTPS and WebSocket)
  - Provides a fixed hostname (xxx.region.elb.amazonaws.com)
  - __Security Groups can be attached to ALBs__ to filters requests 
  - Great for micro services & container-based applications (Docker & ECS)
  - Client info is passed in the request headers
    - Client IP => X-Forwarded-For
    - Client Port => X-Forwarded-Port
    - Protocol => X-Forwarded-Proto
  - __Target Groups__
    - Health checks are done at the target group level
    - Target Groups could be
      - EC2 instances - HTTP
      - ECS tasks - HTTP
      - Lambda functions - HTTP request is translated into a JSON event
      - Private IP Addresses
  - __Listener Rules__ can be configured to route traffic to different target groups based on
    - Path (example.com/users & example.com/posts)
    - Hostname (one.example.com & other.example.com)
    - Query String (example.com/users?id=123&order=false)
    - Request Headers
    - Source IP address

- __Network Load Balancer (NLB)__
  - Operates at Layer 4 (TCP, UDP, TLS over TCP)
  - Can handle millions of request per seconds (extreme performance)
  - Lower latency ~ 100 ms (vs 400 ms for ALB
  - __1 static public IP per AZ__
  - Health Checks support the __TCP, HTTP and HTTPS Protocols__
  - __No security groups can be attached to NLBs__. Since they operate on layer 4, they cannot see the data available at layer 7. They just forward the   incoming traffic to the right target group as if those requests were directly coming from client. So, the attached instances must __allow TCP traffic     on port 80 from anywhere__.
  - Within a __target group, NLB can send traffic to__
    - EC2 instances
    - IP addresses( must be private IPs)
    - Application Load Balancer (ALB)

- __Gateway Load Balancer (GWLB)__
  - Operates at layer 3 (Network layer) - IP packets
  - Used when you want to inspect, analyze the traffic at network level before coming to your ELB or EC2 etc
  - Used to route requests to a __fleet of 3rd party virtual appliances__ like Firewalls, Intrusion Detection and Prevention Systems (IDPS), etc.
  - Then after inspection by the 3rd Party route back the traffic to your instances or ELB
  - target :
    - EC2 instances
    - IP adresses(must be private) 

- __Sticky Sessions (Session Affinity)__
  - Requests coming from a client is always redirected to the same instance based on a cookie After the cookie expires, the requests coming from the same user might be redirected to __another instance__


  - __Only supported by CLB & ALB__ because the cookie can be seen at layer 7 
  - Used to ensure the user doesn’t lose his session data, like login or cart info, while navigating between web pages.
  - Stickiness may cause load imbalance
  - Cookies could be:
    - __Application-based (TTL defined by the application)__ 
    - __Load Balancer generated (TTL defined by the load balancer)__
  - ELB reserved cookie names (should not be used):
    - AWSALB
    - AWSALBAPP
    - AWSALBTG

- __Cross-zone Load Balancing__
- Allows ELBs in different AZ containing unbalanced number of instances to distribute the traffic evenly across all instances in all the AZ registered under a load balancer.
- Supported Load Balancers
  - Classic Load Balancer : Disabled by default
  - Application Load Balancer : Always on (can be disabled at the target group level)
  - Network Load Balancer : Disabled by default

- __Security__
 - The load balancer uses an X.509 certificate (SSL/TLS server certificate)
 - You can manage certificates using ACM (AWS Certificate Manager)
 - You can create upload your own certificates alternatively 
 - __Server Name Indication (SNI)__
   - SNI solves the problem of loading multiple SSL certificates onto one web server (to serve multiple websites)
   - It’s a “newer” protocol, and requires the client to indicate the hostname of the target server in the initial SSL handshake 
   - The server will then find the correct certificate, or return the default one
   - __Does not work for CLB__ work with ALB and NLB

- __Connection Draining__
 - Connection Draining – for CLB
 - Deregistration Delay – for ALB & NLB
 - Time to complete __in-flight requests__ while the instance is de-registering or unhealthy
 - Stops sending new requests to the EC2 instance which is de-registering
 - Between 1 to 3600 seconds (default: 300 seconds)

## Auto Scaling Group

The goal of an Auto Scaling Group (ASG) is to:
 - Scale out (add EC2 instances) to match an increased load
 - Scale in (remove EC2 instances) to match a decreased load
 - Ensure we have a minimum and a maximum number of EC2 instances running
 - Automatically register new instances to a load balancer
 - Re-create an EC2 instance in case a previous one is terminated (ex: if unhealthy)
 - ASG can terminate instances marked as unhealthy by an ELB 
 
 __Scaling Policies__
 
 - __Scheduled Scaling__
    - Scale based on a schedule
    - Used when the load pattern is predictable
    - Anticipate a scaling based on known usage patterns
    
 - __Simple Scaling/Step Scaling__
    - Scale to certain size on a CloudWatch alarm (ex average CPU utilization in all ASG instances)
    - When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
    - When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1
  
 - __Target Tracking Scaling__
    - ASG maintains a CloudWatch metric and scale accordingly to maintain the target defined
    - Ex. maintain CPU usage at 40%
   
 - __Predictive Scaling__
    - Historical data is used to predict the load pattern using ML and scale automatically

__Cooldown__ 
 - After a scaling activity happens, the ASG goes into cooldown period (default 300 seconds) during which it does not launch or terminate additional instances (ignores scaling requests) to allow the metrics to stabilize.
 - Use a ready-to-use AMI to launch instances faster to be able to reduce the cooldown period

__Warm-Up__
- Warm-up value for Instances allows you to control the time until a newly launched instance can contribute to the CloudWatch metrics, so when warm-up time has expired, an instance is considered to be a part Auto Scaling group and will receive traffic

__Relational Database scaling (RDS)__

There are 4 types of scaling we can use to adjust our relational database performance:
- __Aurora Serverless__
  - We can offload scaling to AWS. Excels with unpredictable workloads.
- __Read Replicas__
  - Creating read-only copies of our data can help spread out the workload 
- __Scaling Storage__
  - Storage can be resized(disk size), but it’s only able to go up, not down(except for Aurora). 
- __Vertical Scaling__
  - Resizing the database from one size(ex EC2 t2micro) to another(ex EC2 t3 large) can create greater performance. 

__No Relational Database scaling__

- __DynamoDB__ DynamoDB scaling is used to scale dynamoDB

# Storage

## S3
- Remember that S3 is Object-based: i.e allows you to upload files.
- Files can be 0 Bytes to 5 TB.
- There is unlimited storage
- Files are stored in Buckets. Bucket is tied to region, while S3 is global level 
- Not suitable to install operating systems on S3 due to it being object based
- You can turn on MFA delete to avoid accidental delete. 
- __Tiered Storage__ S3 offers a range of storage classes designed for different use cases.
- __Lifecycle Management__ Define rules to automatically transition objects to a cheaper storage tier or delete objects that are no longer required after a set period of time.

__Versioning__
- You can version your files in Amazon S3
- Protect against unintended deletes (ability to restore a version)
- Easy roll back to previous version 
- With versioning, all versions of an object are stored and can be retrieved, including deleted objects. 
- When you DELETE an object, all versions remain in the bucket and Amazon S3 inserts a __delete marker__.
- You can permanently delete an object by specifying the version you want to delete. Only the owner of an Amazon S3 bucket can permanently delete a version. 
- Versioning can only be suspended once it has been enabled.

__Amazon S3 – Replication__
- __Must enable Versioning__ in source and destination buckets
- __Cross-Region Replication (CRR)__
- __Same-Region Replication (SRR)__
- Buckets can be in different AWS accounts
- After you enable Replication, only new objects are replicated
- You can replicate existing objects using S3 __Batch Replication__
- For DELETE operations:
  - Replicate delete markers from source to target (optional)
  - Permanent deletes are not replicated


__Security__

- __User based security__

  - IAM policies define which API calls should be allowed for a specific user
  - Preferred over bucket policy for fine-grained access control

- __Resource Based Policies__

   - __Bucket Policies__
     - Grant public access to the bucket
     - Can either add or deny permissions across all (or a subset) of objects within a bucket.
     - Force objects to be encrypted at upload
     - Cross-account access
   - __Access Control Lists__
     - A list of grants identifying grantee and permission granted  
     - ACLs use an __S3–specific XML__ schema. 
     - __You can grant permissions only to other AWS accounts, not to users in your account__
     - You cannot grant conditional permissions, nor explicitly deny permissions.
     - __Object ACLs are limited to 100 granted permissions per ACL__
     - __The only recommended use case for the bucket ACL is to grant write permissions to the S3 Log Delivery group__
  
- __Note__: An IAM principal can access an S3 object if the IAM permission allows it or the bucket policy allows it and there is no explicit deny.


__You can encrypt objects in S3 buckets using one of 4 methods__
- __Encryption in Transit__
  - SSL/TLS
  - HTTPS
  - HTTPS is mandatory for SSE-C
- __Server-Side Encryption (SSE)__
  - __Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3) – Enabled by Default__
    - Encrypts S3 objects using keys handled, managed, and owned by AWS
    - Object is encrypted server-side using AES-256
    - Must set header: "x-amz-server-side-encryption": "AES256"

  - __Server-Side Encryption with KMS Keys stored in AWS KMS (SSE-KMS)__
    - Leverage AWS Key Management Service (AWS KMS) to manage encryption keys
    - If you use SSE-KMS, you may be impacted by the KMS limits quotas
    - Must set header: "x-amz-server-side-encryption": "aws:kms"

  - __Server-Side Encryption with Customer-Provided Keys (SSE-C)__
    - When you want to manage your own encryption keys
    - Amazon S3 does NOT store the encryption key you provide
    - HTTPS must be used
    - Encryption key must provided in HTTP headers, for every HTTP request made


  - __Client-Side Encryption__ 
    - Use client libraries such as __Amazon S3 Client-Side Encryption Library__
    - Clients must encrypt data themselves before sending to Amazon S3
    - Clients must decrypt data themselves when retrieving from Amazon S3

__Enforcing Encryption with a Bucket Policy__
- A bucket policy can deny all PUT requests that don’t include the x-amz-server-side encryption parameter in the request header


__CORS__
- If a client makes a cross-origin request on our S3 bucket, we need to enable the correct CORS headers
- You can allow for a specific origin or for *

__MFA Delete__
- MFA will be required to:
  - Permanently delete an object version
  - Suspend Versioning on the bucket
- Bucket Versioning must be enabled
- Can only be enabled or disabled by the root user

__S3 Access Logs__

- For audit purpose, you may want to log all access to S3 buckets
- Any request made to S3, from any account, authorized or denied, will be logged into another __S3 bucket__
- That data can be analyzed using data analysis tools
- __The target logging bucket must be in the same AWS region__

__Pre-signed URL__
- Pre-signed URLs for S3 have temporary access token as query string parameters which allow anyone with the URL to temporarily access the resource before the URL expires (default 1h)
- Pre-signed URLs inherit the permission of the user who generated it
- Uses:
  - Allow only logged-in users to download a premium video
  - Allow users to upload files to a precise location in the bucket 

__S3 Object Lock and Glacier Vault Lock__
- Use S3 Object Lock to store objects using a __write once, read many (WORM)model__.
- Object Lock comes in two modes: __governance mode and compliance mode.__
  - __Governance mode__: users can’t overwrite or delete an object version or alter\
     its lock settings unless they have special permissions
  - __Compliance mode__: a protected object version can’t be overwritten or deleted\
     by any user, including the root user in your AWS account

__S3 Storage Classes__

__S3 Standard – General Purpose__
  - Used for frequently accessed data
  - Low latency and high throughput
  - The default storage class
  - Use cases include websites, content distribution, mobile and gaming applications, and big data analytics

__S3 Standard-Infrequent Access (S3 Standard-IA)__
  - __Infrequently accessed data(once a month)__
  - __Rapid Access__: Used for data that is accessed less frequently but requires rapid access when needed.
  - There is a low per-GB storage price and a per-GB retrieval fee
  - Use cases: __Disaster Recovery, backups__

__S3 Intelligent-Tiering__
  - Data with changing or unknown access patterns
  - Automatically moves your data to the most cost-effective tier based on how frequently you access each object.

__S3 Glacier__
- Low-cost object storage meant for archiving / backup
- Pricing: price for storage + object retrieval cost
- __Amazon S3 Glacier Instant Retrieval__
  - Millisecond retrieval, great for data accessed once a quarter  
  - Minimum storage duration of __90 days__
- __Amazon S3 Glacier Flexible Retrieval__
  - __Data accessed once a year__
  - 3 retrieval flexibility:
    - Expedited (1 to 5 minutes)  
    - Standard (3 to 5 hours)
    - Bulk (5 to 12 hours)
  - Minimum storage duration of 90 days

- __Amazon S3 Glacier Deep Archive – for long term storage__
  - __Data accessed once a year__
  - 2 flexible retrieval: 
    - Standard (12 hours)  
    - Bulk (48 hours)
  - Minimum storage duration of 180 days

__S3 Lifecycle Management__
- Lifecycle management automates moving your objects between thedifferent storage tiers, thereby maximizing cost effectiveness.

__S3 Notification Events__

- Optional
- Generates events for operations performed on the bucket or objects
- Targets:
  - SNS topics
  - SQS Standard queues (not FIFO queues)
  - Lambda functions 

__S3 performance__

__3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second, per prefix__ General Perf

- You can get better performance by spreading your reads across different prefixes, you can achieve 11,000 requests per second with 2 prefixes.
- If we used all 4 prefixes in the last example, you would achieve 22,000 requests per second
- There are no limits to the number of prefixes in a bucket. 

__Multipart Uploads__ Upload Perf
- __Recommended__ for files over 100 MB
- __Required__ for files over 5 GB
- __Parallelize uploads__ (increases efficiency)

__S3 Transfer Acceleration__
- Increase transfer speed by transferring file to an __AWS edge location__ which will forward the data to the __S3 bucket in the target region__
- Compatible with multi-part upload
- Data is ingested at the nearest edge location and is transferred over AWS private network (uses CloudFront internally)

__S3 Byte-Range Fetches__  Downloads Perf
-  Parallelize downloads by specifying byte ranges.
-  Better resilience in case of failures, since we only need to refetch the failed byte range and not the whole file

__S3 Select & Glacier Select__
- Retrieve less data using SQL by performing __server-side filtering__
- Can filter by rows & columns (simple SQL statements)
- Less network transfer cost
- Less CPU cost client-side

# EBS
- An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run
- Can only be mounted to 1 instance at a time (except EBS multi-attach)
- It allows your instances to persist data, even after their termination
- They are bound to a specific availability zone
- An EBS Volume in us-east-1a cannot be attached to us-east-1b
- To move a volume across, you first need to snapshot 
- __EBS Multi-attach__ allows the same EBS volume to attach to multiple EC2 instances in the same AZ

__EBS Snapshots__
- Make a backup (snapshot) of your EBS volume at a point in time
- Not necessary to detach volume to do snapshot, but recommended
- Can copy snapshots across AZ or Region

__EBS Snapshot Archive__
 - Move a Snapshot to an ”archive tier” that is 75% cheaper
 - Takes within 24 to 72 hours for restoring the archive
 
__Recycle Bin for EBS Snapshots__
- Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
- Specify retention (from 1 day to 1 year)

__Fast Snapshot Restore (FSR)__
 - Force full initialization of snapshot to have no latency on the first use ($$$)

__Volume Types__
__Only gp2/gp3 and io1/io2 can be used as boot volumes__

__EBS SSD__
- __gp2/gp3 (SSD)__ __General purpose SSD__ volume that balances price and performance for a wide variety of workloads
- __io1/io2 (SSD)__ __Provisioned IOPS__ Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads\
Attach the same EBS volume to multiple EC2 instances in the same AZ

__EBS HDD__

- __st1 (HDD)__ Low cost HDD volume designed for frequently accessed, throughput- intensive workloads
- __sc1 (HDD)__ Lowest cost HDD volume designed for less frequently accessed workloads

__EBS Encryption__

- For Encrypted EBS volumes:
  - Data at rest is encrypted
  - EBS Encryption leverages keys from KMS (AES-256)
  - Data in-flight between the instance and the volume is encrypted
  - All snapshots are encrypted
  - All volumes created from the snapshot are encrypted
- Encrypt an un-encrypted EBS volume 
  - Create an EBS snapshot of the volume
  - Copy the EBS snapshot and encrypt the new copy
  - Create a new EBS volume from the encrypted snapshot (the volume will be automatically encrypted)  

# EFS
- Managed NFS (network file system) that can be mounted on many EC2
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive 
- File system scales automatically, pay-per-use, no capacity planning
- Compatible with Linux-based AMI (Windows not supported at this time)
- Encryption at rest using KMS

__EFS – Performance__
- EFS can support thousands of concurrent connections (EC2 instances).
- EFS can handle up to 10 Gbps in throughput.
- Scale your storage to petabytes.

__Controlling Performance__

 When creating an EFS file system, you can set what performance characteristics you want
  - __General Purpose__ (default): latency-sensitive use cases (web server, CMS, etc.) 
  - __Max I/O__ : higher latency & throughput (big data, media processing)
  
__Storage Tiers__

- EFS comes with storage tiers and lifecycle management, allowing you to move your data from one tier to another after X number of days.
   - __Standard__ For frequently accessed files  
   - __Infrequently Accessed__ For files not frequently accessed
   
# Instance Store
- EBS volumes are network drives with good but “limited” performance
- If you need a high-performance hardware disk, use EC2 Instance Store
- Better I/O performance
- EC2 Instance Store lose their storage if they’re stopped (ephemeral)
- Good for buffer / cache / scratch data / temporary content 


# FSX

- Allows us to launch 3rd party high-performance file systems on AWS
- Useful when we don’t want to use an AWS managed file system like S3
- __Can be accessed from your on-premise infrastructure__


__FSx for Windows__

- A managed Windows Server that runs __Windows Server Message Block (SMB)__ -based file services.
- __Designed for Windows__ and Windows applications.
- Supports Multi-AZ (high availability)
- __Supports__ AD users, access control lists, groups, and security policies, along with Distributed File System (DFS) namespaces and replication.

__Amazon FSx for Lustre__

- A fully managed file system that is optimized for compute-intensive workloads
- High Performance Computing(HPC)
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies
- __Only works with Linux__
- Machine Learning
- Media Data Processing Workflows


__FSx Deployment Options__

- __Scratch File System__
  - Temporary storage (cheaper)
  - Data is not replicated (data lost if the file server fails)
  - High burst (6x faster than persistent file system)
  - Usage: short-term processing

- __Persistent File System__
  - Long-term storage (expensive)
  - Data is replicated within same AZ
  - Failed files are replaced within minutes
  - Usage: long-term processing, sensitive data

__How differ  EFS, FSx for Windows, or FSx for Lustre__
- __EFS__: When you need distributed, highly resilient storage for Linux instances and Linux-based applications.
- __Amazon FSx__ for Windows: When you need centralized storage for Windows-based applications, such as SharePoint\ Microsoft SQL Server, Workspaces, IIS Web Server, or any other native Microsoft application.
- __Amazon FSx for Lustre__ When you need high-speed, high-capacity distributed storage.\
  This will be for applications that do high performance computing (HPC), financial modeling, etc.\
  Remember that FSx for Lustre can store data directly on S3
 
# Storage Gateway
 
- Bridge between __on-premises data__ and __cloud data__
- Not suitable for __one-time sync__ of large amounts of data (use __DataSync__ instead)
- Optimizes data transfer by sending only changed data
- __Use cases__:
  - disaster recovery
  - backup & restore
  - on-premises cache & low-latency files access
  
__Types of Storage Gateway__
 
 __S3 File Gateway__
 
 - Configured S3 buckets are accessible using the __NFS__ and __SMB__ protocol
 - Most recently used data is __cached__ in the file gateway__
 - Supports S3 Standard, S3 Standard IA, S3 One Zone A, S3 Intelligent Tiering
 - __Transition to S3 Glacier using a Lifecycle Policy__
 - Bucket access using __IAM roles__ for each File Gateway
 - SMB Protocol has integration with Active Directory (AD) for user authentication
 
 ![image](https://user-images.githubusercontent.com/35028407/226275837-ab8f87ea-0c8e-4752-b606-b6fc0ffb03c7.png)

__FSx File Gateway__
- Native access to Amazon FSx for Windows File Server
- __Local cache for frequently accessed data__
- Windows native compatibility (SMB, NTFS, Active Directory...)
- Useful for group file shares and home directories

![image](https://user-images.githubusercontent.com/35028407/226276631-75b1606a-70de-4b97-826c-5e2e343122f7.png)

__Volume Gateway__

- Block storage using iSCSI protocol backed by S3
- Backed by __EBS snapshots__ which can help restore on-premises volumes
- Two kinds of volumes:
  - __Cached volumes__: low latency access to most recent data
  - __Stored volumes__: entire dataset is on premise, scheduled backups to S3
  
  ![image](https://user-images.githubusercontent.com/35028407/226277537-507618d3-46af-4567-933a-aaa1981cba97.png)

__Tape Gateway__
- Used to backup on-premises data using tape-based process to S3 as Virtual Tapes
- Uses iSCSI protocol

![image](https://user-images.githubusercontent.com/35028407/226277866-1936282f-11f0-4551-8faa-58bc48abc9e8.png)

__Storage Gateway - Hardware Appliance__

- Storage Gateway requires on-premises virtualization. If you don’t have virtualization available, you can use a Storage Gateway - Hardware Appliance. It is a mini server that you need to install on-premises.
- __Does not work with FSx File Gatway__

 
# Aws Backup
 
Backup allows you to consolidate your backups across multiple AWS services, such as :
 - EC2
 - EBS
 - EFS 
 - S3
 - Amazon FSx for Lustre
 - Amazon FSx for Windows File Server  
 - AWS Storage Gateway
 - RDS
 - DynamoDB

__It gives you centralized control across all AWS services, in multiple AWS accounts across the entire AWS organization.__

__Aws backup benefit__
- __Central Management__
- __Automation__ : create automated backup schedules and retention policies,create lifecycle policies\
allowing you to expire  unnecessary backups after a period of time
- __Improved Compliance__: Backup policies can be enforced while backups can be encrypted both at rest and in transit\
 allowing alignment to regulatory compliance
 
 __Backup Vault__
 - WORM (Write Once Read Many) model for backups
 - Even the root user cannot delete backups
 - Even the root user cannot delete backups
   - Inadvertent or malicious delete operations
   - Updates that shorten or alter retention periods 
 
 # Database

## RDS

- RDS stands for Relational Database Service
- It’s a managed DB service for DB use SQL as a query language
- RDS is generally used for __online transaction processing (OLTP)__ workloads
- Databases supported :
  - Postgres
  - MySql
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Aurora  
- Continuous backups and restore to specific timestamp __(Point in Time Restore)!__
- You can’t SSH into your instances
 
__RDS Auto Scaling__

- When RDS detects you are running out of free database storage, it scales automatically. 
- You have to set __Maximum Storage Threshold__ (maximum limit for DB storage)
- Condition for automatic storage scaling:
   - Free storage is less than 10% of allocated storage
   - Low-storage lasts at least 5 minutes
   - 6 hours have passed since last modification
  
__RDS Read Replicas for read scalability AKA Performance__

- A read-only copy of your primary database in the same AZ, cross-AZ, or cross-region
- Used to increase or scale read performance.
- __Up to 5 Read Replicas__
- Replication is __ASYNC__ so reads are eventually consistent
- Replicas can be __promoted__ to their own DB
- Applications must update the connection string to leverage read replicas

__RDS Multi AZ for Disaster Recovery__

- With __Multi-AZ__, RDS creates an exact copy of your production database in another __Availability Zone__
- __Synchronous replication__
- One DNS name, so __connection string does not require to be updated__(both the databases can be accessed by one DNS name\
 which allows for automatic DNS failover to standby database)
- When failing over, __RDS flips the CNAME(map hostname to another hostname, so map dns name to to standby dns name) record__ for the DB instance to point at the standby, which is in turn promoted to become the new primary.
- Cannot be used for scaling as the standby database cannot take read/write operation
- The __Read Replicas__ can be setup as Multi AZ for __Disaster Recovery(DR)__

![image](https://user-images.githubusercontent.com/35028407/225748464-585f0ab9-6eac-4657-b2ef-db2bdb816bfc.png)


__RDS From Single-AZ to Multi-AZ__

- Zero downtime operation (no need to stop the DB)
- Just click on “modify” for the database
- The following happens internally
  - A snapshot is taken
  - A new DB is restored from the snapshot in a new AZ
  - Synchronization is established between the two databases

![image](https://user-images.githubusercontent.com/35028407/225748554-bd1454f8-d663-44e2-b4f2-c5fdcd255587.png)


__RDS Backup__

- __Automated Backups (enabled by default)__
  - Daily full backup of the database (during the defined maintenance window)
  - Backup retention: 7 days (max 35 days)
  - Transaction logs are backed-up by RDS every 5 minutes (point in time recovery) 
- __DB Snapshots__
  - Manually triggered
  - Backup retention: unlimited
  -  in a stopped RDS database, you will still pay for storage. If you plan on
stopping it for a long time, you should snapshot & restore instead

__RDS Proxy__
  - Fully managed database proxy for RDS
  - Allows apps to pool and share DB connections established with the database
  - mproving database efficiency by reducing the stress on database resources (e.g., CPU, RAM) and minimize open connections (and timeouts)
  - Serverless, autoscaling, highly available (multi-AZ)
  - __Reduced RDS & Aurora failover time by up 66%__
  - __Enforce IAM Authentication for DB, and securely store credentials in AWS Secrets Manager__
  - __RDS Proxy is never publicly accessible (must be accessed from VPC)__

## Amazon Aurora
- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB
- Aurora is “AWS cloud optimized” and claims __5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS__
- Aurora storage automatically grows in increments of 10GB, up to 128 TB.
- __Up to 15 read replicas__
- __Supports only MySQL & PostgreSQL__
- Failover in Aurora is instantaneous.
- Backtrack: restore data at any point of time without using backups

__Aurora High Availability__

- 2 copies of your data are contained in each Availability Zone
- with a minimum of 3 Availability Zones
- 6 copies of your data
- Aurora is designed to __transparently handle the loss of up to 2 copies of data__ without affecting
- database write availability and up to 3 copies without affecting read availability
- Aurora storage is also __self-healing__. 
- Data blocks and disks are continuously scanned for errors and repaired automatically
- Support for Cross Region Replication
- __Automated failover__ A read replica is promoted as the new master in less than 30 seconds
- In case no replica is available, Aurora will attempt to create a new DB Instance in the same AZ as the original instance

__Aurora Read Scaling__

- One Aurora Instance takes writes __(master)__
- Master + up to 15 Aurora Read Replicas serve reads
- Aurora DB Cluster :
  - __Writer Endpoint__ :
    - Always points to the master (can be used for read/write)
    - Each Aurora DB cluster has one writer cluster endpoint
  - __Reader Endpoint__
    - Provides load-balancing for read replicas only (used to read only)
    - If the cluster has no read replica, it points to master (can be used to read/write) 
    - Each Aurora DB cluster has one reader endpoint
    - When the client want to read the readerEndpoint will load balacing to a Read Replica 
  - __Custom Endpoint__
    - Used to point to a subset of replicas
    - Provides load-balanced based on criteria other than the read-only or read-write capability of the DB instances like instance class (ex, direct   internal users to low-capacity instances and direct production traffic to high-capacity instances)
    - When a custom endpoint is set a Reader Endpoint will not be used 


__Aurora Serverless__

- Optional
- Automated database instantiation and auto scaling based on actual usage
- __Good for infrequent,intermittent or unpredictable workloads__
- No capacity planning needed
- Pay per second, can be more cost effective

__Aurora Multi-Master__

- Optional
- In case you want immediate __failover__ for write node (High availability)
- Every node does R/W - vs promoting a Read Replica as the new master

__Aurora Global Database__

- __Aurora Cross Region Read Replicas:__
  - Useful for disaster recovery
 - Designed for __globally distributed applications__ with __low latency local reads__ in each region
 - 1 Primary Region (read / write)
 - Up to 5 secondary (read-only) regions (replication lag < 1 second)
 - Up to 16 Read Replicas per secondary region
 - Helps for decreasing latency for clients in other geographical locations
 - __RTO of less than 1 minute__ (to promote another region as primary)

__Aurora Backup__

  - __Automated backups__
    - 1 to 35 days (cannot be disabled) 
    - point-in-time recovery in that timeframe
  - __Manual DB Snapshots__
    - Manually triggered by the user
    - Retention of backup for as long as you want    
    - Aurora clone is faster to create a new DB than form Snapshot

# ElastiCache

- The same way RDS is to get managed Relational Databases…
- ElastiCache is to get managed Redis or Memcached
- Caches are in-memory databases with really high performance, low latency
- Helps make your application stateless, because it doesn’t have to cache locally

## DynamoDB

- Fully managed, highly available with replication across multiple AZs
- NoSQL database - not a relational database - __with transaction support__
- Scales to massive workloads, distributed database
- __Single digit millisecond__ response time at any scale
- Maximum size of an item is 400KB
- __Supports TTL__ (automatically delete an item after an expiry timestamp)
- Supports __Transactions__ (either write to multiple tables or write to none)- __DynamoDB transactions.__
- DynamoDB transactions provide developers atomicity, consistency, isolation, and durability\
(__ACID__ across 1 or more tables within a single AWS account and region.
- All-or-nothing transactions.

__Capacity__

- __Provisioned Mode (default)__
  - You specify the number of reads/writes per second
  - You need to plan capacity beforehand
  - Pay for provisioned Read Capacity Units (RCU) & Write Capacity Units (WCU)
  - Auto-scaling option (eg. set RCU and WCU to 80% and the capacities will be scaled automatically based on the workload)
- __On-demand Mode__
  - Read/writes automatically scale up/down based on workloads 
  - No capacity planning needed
  - Pay for what you use, more expensive ($$$)
  - Great for unpredictable workloads, steep sudden spikes

 __DynamoDB Accelerator (DAX)__

- Fully managed, highly available, in-memory cache
- 10x performance improvement
- Reduces request time from milliseconds to __microseconds__ even under load
- Help solve read congestion by caching
- 5 minutes TTL for cache (default)
- Doesn’t require application code changes

__DynamoDB Streams__

- Ordered stream of notifications of item-level modifications (create/update/delete) in a table
- Destination can be:
  - Kinesis Data Streams
  - AWS Lambda
  - Kinesis Client Library applications
- Data Retention for up to 24 hours   
- Allow Implement cross-region replication
- React to changes in real-time (welcome email to users)

__DynamoDB Global Tables__

- Globally distributed applications
- Based on DynamoDB streams
- Multi-region redundancy for disaster recovery or high availability
- Replication latency under 1 second
- __Must enable DynamoDB Streams as a pre-requisite__

## DocumentDB
- Aurora is an “AWS-implementation” of PostgreSQL / MySQL …
- __DocumentDB is the same for MongoDB (which is a NoSQL database)__
- Fully Managed, highly available with replication across 3 AZ
- DocumentDB storage automatically grows in increments of 10GB, up to 64 TB.
- Automatically scales to workloads with millions of requests per seconds

## Amazon Neptune
- Fully managed __graph database__
- A popular graph dataset would be a __social network__
- Highly available across 3 AZ, with up to 15 read replicas
- Highly available with replications across multiple AZs

## Amazon QLDB

- QLDB stands for ”Quantum Ledger Database”
- A ledger is a book __recording financial transactions__
- Fully Managed, Serverless, High available, Replication across 3 AZ
- Used to review history of all the changes made to your application data over time
- __Immutable system: no entry can be removed or modified, cryptographically verifiable__
- You cannot update a record (i.e.,replace old content) in a ledger database. Instead, an update adds a new record to the databas
- __Use case__ : __financial transactions__, supply chain, cryptocurrencies, such as Bitcoin, blockchain

## Amazon Timestream

- Fully managed, fast, scalable, serverless __time series database__
- Automatically scales up/down to adjust capacity
- Encryption in transit and at rest
- __Use cases__: IoT apps, operational applications, real time analytics, …


# Networking

## VPC

- VPC = Virtual Private Cloud
- You can have multiple VPCs in an AWS region (__max. 5 per region – soft limit__)
- Because VPC is private, only the Private IPv4 ranges are allowed:
  - 10.0.0.0 – 10.255.255.255 (10.0.0.0/8) 
  - 172.16.0.0 – 172.31.255.255 (172.16.0.0/12)
  - 192.168.0.0 – 192.168.255.255 (192.168.0.0/16)
- Max. CIDR per VPC is 5, for each CIDR
  - __Min. size is /28 (16 IP addresses)__
  - __Max. size is /16 (65536 IP addresses)__

  
__VPC – Subnet__
-  AWS reserves __5 IP addresses (first 4 & last 1)__ in each subnet

__Internet Gateway (IGW)__
- Allows resources (e.g., EC2 instances) in a VPC connect to the Internet
- It scales horizontally and is highly available and redundant
- One VPC can only be attached to one IGW and vice versa
- Internet Gateways on their own do not allow Internet access
- Route tables must also be edited!

__Bastion Hosts__
- A EC2 instance running in the public subnet (accessible from public internet), to allow users to SSH into the instances in the private subnet.
- __Bastion Host security group__ must allow inbound from the __internet on port 22 from restricted CIDR__, for example the public
CIDR of your corporation
- __Security Group of the EC2 Instance__ must allow the Security Group of the Bastion Host, or the private IP of the Bastion host

<img src="https://user-images.githubusercontent.com/35028407/227360848-ca36d049-0dd5-4586-936a-8eec9cb083f5.png" width="400" />


__NAT Instance__

- __NAT for Network Address Translation__
- Allows EC2 instances in private subnets to connect to the Internet
- Must be launched in a public subnet
- Must disable EC2 setting: __Source /destination Check__ because NAT instance forward traffic that does not belong to him
- Must have Elastic IP attached to it
- Route Tables must be configured to route traffic from private subnets to the NAT Instance
- Can be used as a Bastion Host
- Disadvantages:
  - Not highly available or resilient out of the box. Need to create an ASG in multi-AZ + resilient user-data script
  - Internet traffic bandwidth depends on EC2 instance type 

![Capture d’écran 2023-03-12 à 21 21 53](https://user-images.githubusercontent.com/35028407/224571333-fedbdbe0-6fc4-483d-a3ce-586caa62c7b5.png)


__NAT Gateway__

- AWS-managed NAT, higher bandwidth, high availability, no administration
- Pay per hour for usage and bandwidth
- Preferred over NAT instances
- NATGW is created in a specific Availability Zone, __uses an Elastic IP__
- __Can’t be used by EC2 instance in the same subnet (only from other subnets)__
- Requires an IGW (Private Subnet => NATGW => IGW)
- __Created in a public subnet__
- 5 Gbps of bandwidth with automatic scaling up to 45 Gbps
- No Security Groups to manage / required
- Route Tables for private subnets must be configured to route internet-destined traffic to the NAT gateway

![image](https://user-images.githubusercontent.com/35028407/224571995-c755c35d-87e3-49da-b223-021da7d53d53.png)

__Architecture__

![image](https://user-images.githubusercontent.com/35028407/224572054-495518a9-d85e-404a-9b66-2ade283a5c77.png)

__NAT Gateway with High Availability__

- __NAT Gateway is resilient within a single Availability Zone__
- Must create __multiple NAT Gateways__ in __multiple AZs__ for fault-tolerance
- No cross-AZ failover needed because if an AZ goes down, all of the instances in that AZ also go down.

<img src="https://user-images.githubusercontent.com/35028407/224572232-0dc02ac3-1e4d-4bad-86e6-3c138c2d2393.png" width="400" />


__Network Access Control List (NACL)__

- NACL are like a firewall which control traffic from and to __subnets__
- One NACL per subnet but a NACL can be attached to multiple subnets
- __New subnets are assigned the Default NACL__
- __Default NACL allows all inbound & outbound requests__
- New NACL rule By default deny all inbound and outbound traffic until you add rules
- __NACL Rules__:
  - Based only on IP addresses
  - Rules number: 1-32766 (lower number has higher precedence)
  - First rule match will drive the decision
  - The last rule denies the request (only when no previous rule matches)


__NACL vs Security Group__

 - __NACL__
   - Firewall for subnets
   - Supports both Allow and Deny rules
   - __Stateless__ (both request and response will be evaluated against the NACL rules)
 - __Security Group__
   - Firewall for EC2 instances
   - Supports only Allow rules
   - __Stateful__ return traffic is automatically allowed,regardless of any rules

![image](https://user-images.githubusercontent.com/35028407/227431682-2fa029ab-e6c1-4211-a512-ddadf3f9d095.png)


__NACL with Ephemeral Ports__

- For any two endpoints to __establish a connection__, they must use ports
- Clients connect to a __defined port__, and expect a response on an __ephemeral port__
- In the example below, the client EC2 instance needs to connect to DB instance. Since the ephemeral port can be randomly assigned from a range of ports, the Web Subnets’s NACL must allow inbound traffic from that range of ports and similarly DB Subnet’s NACL must allow outbound traffic on the same range of ports.

![image](https://user-images.githubusercontent.com/35028407/227432695-6bf1d7db-a70e-4d07-9e27-598735e4b8a6.png)



__VPC Peering__
- Privately connect two VPCs using AWS network
- Must not have overlapping CIDRs
- VPC Peering connection is NOT transitive
- Must update route tables in each VPC’s subnets to ensure requests destined to the peered VPC can be routed through the __peering connection__
- You can create VPC Peering connection between VPCs in different __AWS
accounts/regions__(cross account or cross region)
- You can reference a __security group__ in a peered VPC (works cross accounts – same region)

![image](https://user-images.githubusercontent.com/35028407/224573874-c62c0540-a409-4208-8b00-e740a65fbd98.png)

![image](https://user-images.githubusercontent.com/35028407/224573884-adf59c75-6bb8-48bd-a973-073738009655.png)

![image](https://user-images.githubusercontent.com/35028407/224573970-04a0a16b-3774-42d3-90b5-a96f503b8e31.png)




__VPC Endpoints__

- Every AWS service is publicly exposed (public URL)
- VPC Endpoints (powered by __AWS PrivateLink__) allows you to connect to __AWS services__ using a __private network__ instead of using the public Internet
- They’re redundant and scale horizontally
- They remove the need of IGW, NATGW, … to access AWS Services
- Types of Endpoints :
  - __Interface Endpoints (powered by PrivateLink)__
    - Provisions an __ENI__ (private IP address) as an entry point
    - Need to __attach a security group to the interface endpoint__ to control access
    - Supports most AWS services
    - No need to update the route table
    - $ per hour + $ per GB of data processed
  - __Gateway Endpoint__
    - Provisions a gateway
    - Must be used as a target in a route table 
    - Supports only __S3__ and __DynamoDB__
    - Free

![image](https://user-images.githubusercontent.com/35028407/224574183-409f676e-b68c-4024-8539-5d94595ae278.png)

__VPC Flow Logs__

- Captures information about __IP__ traffic going into your __interfaces__
- Three levels:
  - __VPC__ Flow Logs
  - __Subnet__ Flow Logs
  - __ENI__ Flow Logs 
- Can be configured to show accepted, rejected or all traffic
- Flow logs data can be sent to __S3__ (bulk analytics) or __CloudWatch Logs__ (near real-time via metric filter)
- Query VPC flow logs using __Athena__ in __S3__ or __CloudWatch Logs Insights__


__IPv6 Support__
- IPv4 cannot be disabled for your VPC
- Enable IPv6 to operate in __dual-stack mode__ in which your EC2 instances will get at least a private IPv4 and a public IPv6. They can communicate using either __IPv4__ or __IPv6__ to the internet through an __Internet Gateway__.
- If you cannot launch an EC2 instance in your subnet, It’s not because it cannot acquire an IPv6 (the space is very large). It’s because there are no available IPv4 in your subnet.
- __Solution__: Create a new IPv4 CIDR in your subnet  

<img src="https://user-images.githubusercontent.com/35028407/227515123-40067ef6-9aab-4a73-8595-cc43ecccca1d.png" width="400" />

__Egress-only Internet Gateway__
- Allows instances in your VPC to initiate outbound connections over IPv6 while preventing inbound IPv6 connections to your private instances.
- Similar to NAT Gateway but for IPv6
- Must update Route Tables

![image](https://user-images.githubusercontent.com/35028407/227515543-8e4715e8-ff40-402d-86b6-d6d9c68088fb.png)


# PrivateLink
To open our applications up to other VPCs, we can either:
- Open the VPC up to the Internet
  - Security considerations; everything in the public subnet is public
  - A lot more to manage 
- Use VPC Peering
  - You will have to create and manage many different peering relationships

- __PrivateLink__ The best way to expose a service VPC __to tens, hundreds, or thousands of customer VPCs__
- Doesn’t require VPC peering; no route tables, NAT gateways, internet gateways, etc
- Requires a __Network Load Balancer__ on the service VPC and an __ENI__ on the customer VPC

![image](https://user-images.githubusercontent.com/35028407/224575961-2394ab07-61d8-4967-9c2d-7a151b71db09.png)


# Site-to-Site VPN

- Easiest and most cost-effective way to connect a VPC to an on-premise data center
- __IPSec Encrypted__ connection through the public internet
- __Virtual Private Gateway (VGW)__: VPN concentrator on the VPC side of the VPN connection
- __Customer Gateway (CGW)__: Software application or physical device on customer side of the VPN connection
- __Enable Route Propagation__ for the Virtual Private Gateway in the route table that is associated with your subnets
- If you need to ping EC2 instances from on-premises, make sure you add the __ICMP protocol__ on the inbound rules of your security groups

![image](https://user-images.githubusercontent.com/35028407/224577737-2f0cdd52-7952-4c9f-aceb-07873b70d668.png)

__AWS VPN CloudHub__
- __Low-cost hub-and-spoke model for network connectivity between a VPC and multiple on-premise data centers(VPN only)__
- Every participating network can communicate with one another through the VPN connection
- It operates over the public internet, but all traffic between the customer gateway and the AWS VPN CloudHub is encrypted.
- To set it up, connect __multiple VPN connections__ on the __same VGW__, setup dynamic routing and configure __route tables__

![image](https://user-images.githubusercontent.com/35028407/224577899-f80ab184-fc0f-4c72-9afe-da6e4ad724ac.png)

# Direct connect

- Dedicated __private connection__ from an on-premise data center to a VPC
- Dedicated connection must be setup between your __Data Center__ and AWS __Direct Connect locations__
- You need to setup a __Virtual Private Gateway__ on your VPC
- __Data in transit is not-encrypted__ but the connection is private (secure)
- More stable and secure than Site-to-Site VPN
- Access public & private resources on the same connection using Public & __Private Virtual Interface (VIF)__ respectively
- DIRECT CONNECT IS:
   - Fast
   - Secure
   - Reliable
   - Able to take massive throughput
   - Lower cost
   
![image](https://user-images.githubusercontent.com/35028407/224578908-3c1ca9ca-9760-42bb-a995-2cf8f49809e8.png)

  
__Direct Connect Gateway__

  - Used to setup a Direct Connect to multiple VPCs from your data center, possibly in different regions but same account
  - Using DX, we will create a Private VIF to the Direct Connect Gateway which will extend the VIF to Virtual Private Gateways in multiple VPCs (possibly across regions).

![image](https://user-images.githubusercontent.com/35028407/224579112-faf44a8e-5246-4f13-83bc-482425b5b3ba.png)
  
   
__Connection Types__

  - __Dedicated Connection__
    - A physical Ethernet connection associated with a single customer.  
    - 1Gbps,10 Gbps and 100 Gbps capacity
  - __Hosted Connection__
    - A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of acustomer
    - 50Mbps, 500 Mbps, to 10 Gbps


__Encryption__

- For encryption in flight, use AWS Direct Connect + __VPN__ which provides an __IPsec-encrypted private connection__
- Good for an extra level of security

![image](https://user-images.githubusercontent.com/35028407/227508639-d5c562b7-9dcf-4e1f-8315-b7a7da370bf7.png)


__Resiliency__

- __Best way__ (redundant direct connect connections)

![image](https://user-images.githubusercontent.com/35028407/227494776-b2b6eddb-ce79-44f7-a4f3-5b71cacb994d.png)

- __VPN connection as a backup__ 
  - In case Direct Connect fails, you can set up a __backup Direct Connect connection (expensive), or a Site-to-Site VPN connection__ 


# Transit Gateway

- __Transitive peering__ between thousands of VPCs and on-premise data centers using __hub-and-spoke (star) topology__
- Works with __Direct Connect Gateway__, __VPN Connection__
- Regional resource, can work __cross-region__ 
- You can peer Transit Gateways __across regions__
- __Route Tables__ to control communication within the transitive network
- Supports __IP Multicast__ (not supported by any other AWS service)

<img src="https://user-images.githubusercontent.com/35028407/224579481-a1e10b06-f6d8-4a64-8e30-66c78229f5d1.png" width= "400"/>


__Increasing BW of Site-to-Site VPN connection__
- ECMP = Equal-cost multi-path routing
- To increase the bandwidth of the connection between Transit Gateway and corporate data center, create multiple site-to-site VPN connections, each with 2 tunnels (2 x 1.25 = 2.5 Gbps per VPN connection).

![image](https://user-images.githubusercontent.com/35028407/227510952-38ade650-0e63-4bdd-9b83-9841ecfc88ad.png)

__Share Direct Connect between multiple accounts__
- Share Transit Gateway across accounts using Resource Access Manager (RAM) connection between VPCs in the __same region__ but different accounts

![image](https://user-images.githubusercontent.com/35028407/227511205-5a9417ad-a06e-4d35-9342-ff56cfa35f8a.png)


# Networking Costs

-  Use Private IP instead of Public IP for good savings and better network performance
-  Use same AZ for maximum savings (at the cost of high availability)
- Traffic entering the AWS is free
- Traffic leaving an AWS region is paid


<img width="879" alt="Capture d’écran 2023-03-24 à 18 00 11" src="https://user-images.githubusercontent.com/35028407/227594380-fe99e9e1-4791-4717-922d-44de9dede345.png">

__Minimizing egress traffic network cost__

- __Egress traffic__: outbound traffic (from AWS to outside)
- __Ingress traffic__: inbound traffic - from outside to AWS (typically free)
- Try to keep as much internet traffic within AWS to minimize costs
- __Direct Connect location that are co-located in the same AWS Region result in lower cost for egress network__

<img width="800" alt="Capture d’écran 2023-03-24 à 18 15 16" src="https://user-images.githubusercontent.com/35028407/227595283-64401898-7ad0-4648-9cc1-ba979eb34177.png">


# Route 53

- A highly available, scalable, fully managed and Authoritative DNS(cusutmer can update DNS records)
- Route 53 is also a Domain Registrar
- Ability to check the health of your resources
- The only AWS service which provides 100% availability SLA

__Hosted Zone__

- A container for records that define how to route traffic to a domain and
its subdomains
- Hosted zone is queried to get the IP address from the hostname

  __Two types__
    - __Public Hosted Zone__
       - resolves public domain names
       - can be queried by anyone on the internet
    - __Private Hosted Zone__
       - resolves private domain names
       - can only be queried from within the VPC

__Record Types__

Each record contains:
  - __Domain/subdomain Name__ – e.g., example.com
  - __Record Type__ – e.g., A or AAAA
  - __Value__ – e.g., 12.34.56.78
  - __Routing Policy__ – how Route 53 responds to queries
  - __TTL__ – amount of time the record cached at DNS Resolvers

- __A__ – maps a hostname to IPv4
- __AAAA__ – maps a hostname to IPv6
- __CNAME__ – maps a hostname to another hostname
  - The target is a domain name which must have an A or AAAA record
  - __Cannot point to root domains (Zone Apex)__ Ex: you can’t create a CNAME record for __example.com__, but you can create for __something.example.com__
 
- __NS (Name Servers)__ - controls how traffic is routed for a domain
- __Alias__ - maps a hostname to an AWS resource(app.mydomain.com => blabla.amazonaws.com)
  - Native health check 
  - AWS proprietary
  - Can point to root (zone apex) and non-root domains
  - __Alias Record is of type A or AAAA (IPv4 / IPv6)__
  - Automatically recognizes changes in the resource’s IP addresses
  - __You can’t set the TTL__
  - Targets can be:
    - Elastic Load Balancers
    - CloudFront Distributions
    - API Gateway
    - Elastic Beanstalk environments
    - S3 Websites
    - VPC Interface Endpoints
    - Global Accelerator accelerator
  - __Target cannot be an EC2 DNS name__
  
  
  __Routing Policies__
  
  Define how Route 53 responds to DNS queries
  
  __Simple__
   - Route to one or more resources
   - If multiple values are returned, client chooses one at random 
   - No health check (if returning multiple resources, some of them might be unhealthy)
   - When Alias enabled, you can only specify one Aws resource as a target

  <img src ="https://user-images.githubusercontent.com/35028407/224734496-073f89af-49e1-4c2e-9213-eef3ef3411f9.png" width="400"/>
  <img src ="https://user-images.githubusercontent.com/35028407/224734556-e325660a-ab50-46a4-80d8-9a53ffd8e110.png" width="400"/>


__Weighted__

- Control the % of the requests that go to each specific resource
- Can be associated with Health Checks
- __Use cases__: load balancing between regions, testing, new application versions…

__Failover(Active-Passive)__
- Primary & Secondary Records (if the primary application is down, route to secondary application)
- __Health check__ must be associated with the primary record, you can also associate health check to secondary
- Used for __Active-Passive__ failover strategy

__Latency-based__

- Redirect to the resource that has the lowest network latency
- Latency is based on traffic between users and AWS Regions
- Can be associated with Health Checks (has a failover capability)

__Geolocation__

- Routing based on the client's location
- Specify location by Continent, Country
- Should create a “Default” record (in case there’s no match on location)
- __Use cases__: restrict content distribution & language preference
- Can be associated with Health Checks

__Geoproximity__

- Route traffic to your resources based on the geographic location of users and
resources 
- Ability to __shift more or less traffic to resources__ based on the defined __bias__
- To change the size of the geographic region, specify bias values:
  - To expand (1 to 99) – more traffic to the resource
  - To shrink (-1 to -99) – less traffic to the resource
- To use geoproximity routing you must use Route 53 __Traffic Flow__

__Multi-value__
- Route traffic to multiple resources (max 8)
- Health Checks (only healthy resources will be returned)
- __Multi-value is not subsitute for having an ELB, it the client side load balancing
- At difference of simple routing all response returned are healthy 
  
__Health Checks__
- HTTP Health Checks are only for public resources
- Automated for Automated DNS Failover
- Three types:
  - Monitor an endpoint (application or other AWS resource)
    - Multiple global health checkers check the endpoint health
    - Must configure the application firewall to allow incoming requests from the IPs of Route 53 Health Checkers
    - Supported protocols: HTTP, HTTPS and TCP
   - Monitor other health checks (__Calculated Health Checks__)
     - Combine the results of multiple Health Checks into one (AND, OR, NOT)
     - Specify how many of the health checks need to pass to make the parent pass
     - Usage: perform maintenance to your website without causing all health checks to fail
    - Monitor CloudWatch Alarms (to perform health check on private resources(Private Hosted Zone ))
      - Route 53 health checkers are outside the VPC. They can’t access private endpoints (private VPC or on-premises resources).
      - Create a CloudWatch Metric and associate a CloudWatch Alarm to it, then create a Health Check that checks the Cloud watch alarm.  

## API Gateway

- Serverless REST APIs
- Invoke Lambda functions using REST APIs (API gateway will proxy the request to lambda)
- Supports WebSocket (stateful)
- Cache API responses
- Can be integrated with any HTTP endpoint in the backend or any AWS API
-
__Endpoint Types__
 - __Edge-Optimized (default):__
   - For global clients
   - Requests are routed through the CloudFront edge locations (improves latency)
   - The API Gateway lives in only one region but it is accessible efficiently through edge locations 
 - __Regional__
   - For clients within the same region
   - Could manually combine with your own CloudFront distribution for global deployment (this way you will have more control over the caching strategies and the distribution)
 - __Private__
   - Can only be accessed within your VPC using an Interface VPC endpoint (ENI)
   - Use resource policy to define access
  
__Security__
- __User Authentication through__
  - IAM Roles (useful for internal applications)
  - Cognito (identity for external users – example mobile users) 
  - Custom Authorizer( Using lambda function to validate the token being passed in the header and return an lAM policy to determine if the user should be allowed to access the resource )
- __Custom Domain Name HTTPS security through__ integration with AWS Certificate Manager (ACM) 

# Content delivery

## CloudFront

- Content Delivery Network (CDN)
- __Improves read performance, content is cached at the edge__
- Improves users experience
- 216 Point of Presence globally __(edgelocations)__

__Origins__

 - __S3 bucket__
   - For distributing files and caching them at the edge 
   - Enhanced security with CloudFront Origin Access Control (OAC)
   - __Origin Access Identity (OAl old version) or Origin Access Control (OAC new version)__ allows the S3 bucket to only be accessed by __CloudFront__
   - CloudFront can be used as an ingress (to upload files to S3)
 
 - __Custom Origin (HTTP)__
   - Application Load Balancer
   - EC2 instance
   - S3 website (must first enable the bucket as a static S3 website) 
   - Any HTTP backend you want

__CloudFront Geo Restriction__
  - You can restrict who can access your distribution
    - __Allowlist :__
      - Allow your users to access your content only if they're in one of the countries on a list of approved countries.  
     - __Blocklist__
       - Prevent your users from accessing your content if they're in one of the countries on a list of banned countries. 
  - The “country” is determined using a 3rd party Geo-IP database
  - Use case: Copyright Laws to control access to content

__Pricing__

- Price Class All: all regions (best performance)
- Price Class 200: most regions (excludes the most expensive regions)
- Price Class 100: only the least expensive regions

# Global Accelerator

- Leverage the AWS internal network to route to your application
- __2 Anycast IP__ are created for your application
- The Anycast IP send traffic directly to Edge Locations
- The Edge locations send the traffic to your application
- Endpoint could be public or private (could span multiple region):
  - Elastic IP
  - EC2 instances
  - ALB
  - NLB

- __Disaster Recovery__
  - Global Accelerator performs health checks for the application
  - __Failover in less than 1 minute__ for unhealthy endpoints 

- __Good for:__
  - HTTP use cases that require static IP addresses or fast regional failover

# Decoupling applications

- Synchronous between applications can be problematic if there are sudden spikes of traffic
- What if you need to suddenly encode 1000 videos but usually it’s 10?
- In that case, it’s better to decouple your applications:
  - using SQS: queue model
  - using SNS: pub/sub model
  - using Kinesis: real-time streaming model 
- These services can scale independently from our application 

## SQS 
For Simple Notification Service
- Used to asynchronously decouple applications
- Supports multiple producers & consumers
- The message is persisted in SQS until a consumer deletes it
- The consumer polls the queue for messages. Once a consumer processes a message, it __deletes__ it from the queue using __DeleteMessage API__.
- __Max message size: 256KB__
- __Default message retention: 4 days (max: 14 days)__
- __Consumers could be EC2 instances or Lambda functions, Kinesis__

 ### Queue Types
 
 ### Standard Queue
 - Unlimited throughput (publish any number of message per second into the queue)
 - Low latency (<10 ms on publish and receive)
 - Can have duplicate messages (at least once delivery)
 - Can have out of order messages (best effort ordering)
 
 ### FIFO Queue
 
 - Limited throughput: 300 msg/s without batching, 3000 msg/s with
 - Messages are processed in order by the consumer
 - __Message De-duplication__:
   - __De-duplication interval__: 5 min (duplicate messages will be discarded only if they are sent less than 5 mins apart)
   - __De-duplication methods__:
     - __Content-based de-duplication__: computes the hash of the message body and compares
     - __Using a message de-duplication ID__: messages with the same __de-duplication ID__ are considered duplicates
 - __Message Grouping__
   - Group messages based on __MessageGroupID__ to send them to different consumers
   - Same value for __MessageGroupID__
     - All the messages are in order
     - Single consumer
   - Different values for MessageGroupID
     - Messages will be ordered for each group ID
     - Ordering across groups is not guaranteed(messages that belong to different message groups)
     - Each group ID can have a different consumer (parallel processing)
     
 ### Consumer Auto Scaling
 
 We can attach an ASG to the consumer instances which will scale based on the CW metric __Queue Length__(ApproximateNumberOfMessages)
 CW alarms can be triggered to step scale the consumer application.
 
 ### Security
 
 __Encryption__
 - In-flight encryption using HTTPS API
 - At-rest encryption using KMS keys
 - Client-side encryption if the client wants to perform encryption/decryption itself 
 
 __Access Controls__ : IAM policies to regulate access to the SQS API
 
 __SQS Access Policies(resource based policy)__
   - Useful for cross-account access to SQS queues
   - Useful for allowing other services (SNS, S3…) to write to an SQS queue
 
 ### Configurations
 __Message Visibility Timeout__
 - After a message is polled by a consumer, it becomes __invisible__ to other consumers
 - By default, the “message visibility timeout” is __30 seconds__
 - That means the message has __30 seconds__ to be processed
 - After the message visibility timeout is over, the message is “visible” in SQS
 - A consumer could call the __ChangeMessageVisibility__ API to get more time
 - If visibility timeout is high (hours), and consumer crashes, re-processing will take time
 - If visibility timeout is too low (seconds), we may get duplicates
 
 ![image](https://user-images.githubusercontent.com/35028407/225288979-b11b0e56-47cf-4017-9118-cad881cb83f8.png)


__Dead Letter Queue (DLQ)__
- An SQS queue used to store failing to be processed messages in another queue
- After the __MaximumReceives__(the number of times that a message can be received before being sent to a dead-letter queue) threshold is exceeded, the message goes into the DLQ
- __Redrive to Source__ - once the bug in the consumer has been resolved, messages in the DLQ can be sent back to the queue (original queue or a custom queue) for processing
- Prevents resource wastage
- Recommended to set a high retention period for DLQ (14 days)

__Queue Delay/Delivery Delay__
 - Delay message delivery
- Consumers see the message after some delay
- Default: 0 (Max: 15 min)
- Can be set at the queue level

__Long Polling__

- When a consumer requests messages from the queue, it can optionally “wait” for messages to arrive if there are none in the queue
- This is called Long Polling
- Decreases the number of API calls made to __SQS (cheaper)__
- Reduces latency (incoming messages during the polling will be read instantaneously)
- Polling time: 1 sec to 20 sec
- Long Polling is preferred over Short Polling
- Can be enabled at the queue level or at the consumer level by using __WaitTimeSeconds__ parameter in__ ReceiveMessage__ API.

__SQS + Lambda + DLQ__

Failed messages (after the set number of retries) are sent to the DLQ by the SQS queue
![image](https://user-images.githubusercontent.com/35028407/225288575-42fd9606-21e8-4012-a7d4-51d6b51ac450.png)


## SNS
For SNS for Simple Queue Service
- Pub-Sub model (publisher publishes messages to a topic, subscribers listen to the topic)
- Instant message delivery (does not queue messages)

__Security__

__Encryption__
 - In-flight encryption using HTTPS API
 - At-rest encryption using KMS keys
 - Client-side encryption if the client wants to perform encryption/decryption itself 
 
__Access Controls__ : IAM policies to regulate access to the SNS API
 
__SNS Access Policies(resource based policy)__
 - Useful for cross-account access to SNS queues
 - Useful for allowing other services (S3…) to write to an SNS queue
 
 __Standard Topics__
 - Highest throughput
 - At least once message delivery
 - Best effort ordering
 - Subscribers can be:
   - SQS queue
   - HTTP / HTTPS endpoints
   - Lambda functions
   - Emails (using SNS)
   - SMS & Mobile Notifications
   - Kinesis Data Firehose (KDF) to send the data into S3 or Redshift

__FIFO Topics__
  - Guaranteed ordering of messages in that topic
  - Publishing messages to a FIFO topic requires:
    - __Ordering__ by Message Group ID (all messages in the same group are ordered)
    - __Deduplication using__ a Deduplication ID or Content Based Deduplication
  - Can only have SQS FIFO queues as subscribers
  - __Limited throughput__ (same as SQS FIFO) because only SQS FIFO queues can read from FIFO topics
  
  __SNS + SQS Fanout Pattern__
  
  - Fully decoupled, no data loss
  - SQS allows for: data persistence, delayed processing and retries of work
  - Make sure your SQS queue access policy allows for SNS to write
  
  ![image](https://user-images.githubusercontent.com/35028407/225294978-dfb124e9-1b77-4355-bed4-b6569b7b68ba.png)

  
## Kinesis
- Makes it easy to collect, process, and analyze streaming data in real-time
- Ingest real-time data such as: Application logs, Metrics, Website clickstreams,
IoT telemetry data…

### Kinesis Data Streams 
- Real-time data streaming service
- __Used to ingest data in real time directly from source__
- Retention between 1 day to 365 days
- Ability to reprocess (replay) data
- Once data is inserted in Kinesis, it can’t be deleted (immutability)
- Data that shares the same partition goes to the same shard (ordering)
- Producers: AWS SDK, Kinesis Producer Library (KPL), Kinesis Agent
- Consumers:
    - Write your own: Kinesis Client Library (KCL), AWS SDK
    - Managed: AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics, 
  
- __Capacity Modes__
  - __Provisioned__
   - You choose the number of shards provisioned, scale manually or using API
   - Each shard gets 1MB/s in (or 1000 records per second)
   - Each shard gets 2MB/s out (classic or enhanced fan-out consumer)
   - You pay per shard provisioned per hour
  - __On-demand mode__
   - No need to provision or manage the capacity
   - Default capacity provisioned (4 MB/s in or 4000 records per second)
   - Scales automatically based on observed throughput peak during the last 30 days
   - Pay per stream per hour & data in/out per GB
  
  ![image](https://user-images.githubusercontent.com/35028407/225446271-ac6c3c50-515f-4fbe-afcd-5727bfdff773.png)

### Amazon MQ

- If you have some traditional applications running from on-premise, they may use open protocols such as __MQTT, AMQP, STOMP, Openwire, WSS, etc__. When migrating to the cloud, instead of re-engineering the application to use SQS and SNS (AWS proprietary), we can use Amazon MQ (managed Apache ActiveMQ) for communication. 
- Doesn’t “scale” as much as SQS or SNS because it is provisioned 
- Runs on a dedicated machine (can run in HA with failover)
- __Has both queue feature (SQS) and topic features (SNS)__
 
### Kinesis Data Firehose 

- Fully Managed Service, no administration, automatic scaling, serverless
- Used to load streaming data into a target location with optional transformation
- Can ingest data in real time directly from source
- Destinations:
  - __AWS: Redshift, S3, OpenSearch__
  - 3rd party: Splunk, MongoDB, DataDog, NewRelic, etc.
  - Custom HTTP endpoint
  - Supports custom data transformation using Lambda functions
  - No replay capability (does not store data like KDS)

![image](https://user-images.githubusercontent.com/35028407/225447015-a7b9e3ee-e23a-48eb-81ca-2f85b8eeba66.png)


### Event Bridge
- __Schedule or Cron__ to create events on a schedule
- __Event Pattern__: Event rules to react to a service doing something
- Trigger Lambda functions, send SQS/SNS messages

# Migration & Transfer

## Snow Family

- Highly-secure, portable devices to __collect and process data__ at the edge, and __migrate data into and out of AWS__
-  Offline devices to perform data migrations
- If it takes more than a week to transfer over the network, use Snowball devices!

__Device__

- __Snowcone__
  - 2 CPUs, 4GB RAM, wired or wireless access
  - __8 TB storage__
  - Good for space-constrained environment
  - __DataSync Agent__ is preinstalled
  - When to use: __Up to 24 TB, online and offline__

- __Snowball Edge__
  - __Compute Optimized__
    - 52 vCPUs, 208 GB of RAM
    - __42 TB storage__
    - Supports Storage Clustering
  - __Storage Optimized__
    - Up to 40 CPUs, 80 GB of RAM 
    - __80 TB storage__
    - Supports Storage Clustering (up to 15 nodes)
    - Transfer up to petabytes
  - __When to use: Up to petabytes(PB)__
   
- __Snowmobile__
  - __100 PB storage__
  - Used when __transferring > 10PB__
  - Transfer up to exabytes
  - Does not support Storage Clustering
  - __When to use: Up to exabytes(EB)__


__Edge Computing__

- Process data while it’s being created on an edge location (could be anything that doesn’t have internet or access to cloud)
- Devices for edge computing:
  - Snowcone
  - Snowball Edge 

__Data migration__

   - Physical data transport solution: __move TBs or PBs__ of data in or out of AWS 
   - Pay per data transfer job
   - Provide block storage and Amazon S3 compatible object storage
   - __Snowball cannot import to Glacier directly__ (transfer to S3, configure a lifecycle policy to transition the data into Glacier)
   - Need to install __OpsHub__ software on your computer to manage Snow Family devices
 
## DataSync

- Move large amount of data to and from 
  - On-premises / other cloud to AWS (NFS, SMB, HDFS, S3 API…) – needs agent
  - AWS to AWS (different storage services) – no agent needed
  - Can synchronize to:
    - Amazon S3 (any storage classes – including Glacier)
    - Amazon EFS
    - Amazon FSx (Windows, Lustre, NetApp, OpenZFS...)
  -  Replication tasks can be scheduled hourly, daily, weekly
  - __File permissions and metadata are preserved (NFS POSIX, SMB…)__
 
 ![image](https://user-images.githubusercontent.com/35028407/226283193-8d5cd915-7248-4a8d-ad47-3ca555db377b.png)

 
## Transfer Family

- AWS managed service to transfer files in and out of Simple Storage Service (S3) or EFS using FTP (instead of using proprietary methods)
- Supported Protocols
  - FTP (File Transfer Protocol) - unencrypted in flight
  - FTPS (File Transfer Protocol over SSL) - encrypted in flight
  - SFTP (Secure File Transfer Protocol) - encrypted in flight 
  
- Supports Multi AZ
- Pay per provisioned endpoint per hour + fee per GB data transfers
- Clients can either connect directly to the FTP endpoint or optionally through Route 53
- Transfer Family will need permission(IAM roleà)- to read or put data into S3 or EFS

## Database Migration Service
- Migrate entire __databases__ from on-premises to __AWS cloud__
- __The source database remains available during migration__
- Continuous Data Replication using __CDC (change data capture)__
- Requires __EC2 instance running the DMS software__ to perform the replication tasks. If the amount of data is large, use a large instance. If multi-AZ is enabled, need an instance in each AZ.

__Types of Migration__

__Homogeneous Migration__
 - When the source and target DB engines are the same (eg. Oracle to Oracle)
 - One step process:
   - Use the __Database Migration Service (DMS)__ to migrate data from the source database to the target database 
 
__Heterogeneous Migration__
  - When the source and target DB engines are different (eg. Microsoft SQL Server to Aurora)
  - Two step proces:
    - Use the __Schema Conversion Tool (SCT)__ to convert the source schema and code to match that of the target database 
    - Use the __Database Migration Service (DMS)__ to migrate data from the source database to the target database

__Migrating using Snow Family__

- Use the Schema Conversion Tool (SCT) to extract the data locally and move it to the Edge device
- Ship the Edge device or devices back to AWS
- After AWS receives your shipment, the Edge device automatically loads its data into an Amazon S3 bucket.
- AWS DMS takes the files and migrates the data to the target data store (eg. DynamoDB)

# Application migration service

__AWS Application Discovery Service__
- Plan migration projects by gathering information about on-premises data centers
- Server utilization data and dependency mapping are important for migrations
- Two types of migration:
  - __Agentless Discovery (AWS Agentless Discovery Connector)__
    - VM inventory, configuration, and performance history such as CPU, memory, and disk usage
  - __Agent-based Discovery (AWS Application Discovery Agent)__
    - System configuration, system performance, running processes, and details of the network connections between systems    
- Resulting data can be viewed within AWS Migration Hub 

__AWS Application Migration Service__
- Lift-and-shift (rehost) solution which simplify migrating applications to AWS
- Converts your physical, virtual, and cloud-based servers to run natively on AWS
- Supports wide range of platforms, Operating Systems, and databases
- Minimal downtime, reduced costs

<img width="1111" alt="Capture d’écran 2023-03-25 à 12 51 14" src="https://user-images.githubusercontent.com/35028407/227715832-b76e2fc2-1e1c-455e-b4f2-29a120628f97.png">



# RDS and Aurora MySQL Migrations

__RDS MySQL to Aurora MySQL__
 - __Option 1__: DB Snapshots from RDS MySQL restored as MySQL Aurora DB
 - __Option 2__: Create an Aurora Read Replica from your RDS MySQL, and when the replication lag is 0, promote it as its own DB cluster (can take time and cost $)

__External MySQL to Aurora MySQL__

- __Option 1__: 
  - Use Percona XtraBackup to create a file backup in Amazon S3
  - Create an Aurora MySQL DB from Amazon S3
- __Option 2__:
  - Create an Aurora MySQL DB
  - Use the mysqldump utility to migrate MySQL into Aurora (slower than S3 method)

__Use DMS if both databases are up and running__

__Same process with PostgreSQL__


# Disaster Recovery

## Disaster Recovery

- Any event that has a negative impact on a company’s business continuity or finances is a disaster
- __Recovery Point Objective (RPO)__: how often you backup your data (determines how much data are you willing to lose in case of a disaster)
- __Recovery Time Objective (RTO)__: how long it takes to recover from the disaster (down time)


![image](https://user-images.githubusercontent.com/35028407/227709642-9f16d5fc-c0aa-4994-9f8e-cc863ffe69af.png)


  __Strategies__
  
  - __Backup & Restore__
    - High RPO (hours)
    - Need to spin up instances and restore volumes from snapshots in case of disaster => High RTO 
    - Cheapest & easiest to manage
  - __Pilot Light__
    - __Critical parts of the app are always running__ in the cloud (eg. continuous replication of data to another region)
    - Low RPO (minutes)
    - Critical systems are already up => Low RTO
    - Ideal when RPO should be in minutes and the solution should be inexpensive
    - DB is critical so it is replicated continuously but EC2 instance is spin up only when a disaster strikes
  - __Warm Standby__
    - A complete backup system is up and running at the minimum capacity. This system is quickly scaled to production capacity in case of a disaster.
    - Very low RPO & RTO (minutes)
    - Expensive
  - __Multi-Site or Hot Site Approach__
    - A backup system is running at full production capacity and the request can be routed to either the main or the backup system. 
    - Multi-data center approach
    - Lowest RPO & RTO (minutes or seconds)
    - Very Expensive
   

# Machine Learning

## Rekognition

- Find __objects, people, text, scenes__ in __images and videos__ using ML
- __Facial analysis__ and __facial search__ to do user verification, people counting:
- Use cases
  - Content Moderation
  - Text Detection 
  - Face Detection and Analysis (gender, age range, emotions…)
  - Face Search and Verification
  - Celebrity Recognition
  - Detect content that is inappropriate, unwanted, or offensive (image and videos)
  - Used in social media, broadcast media, advertising, and e-commerce situations to create a safer user experience

# Transcribe

- Automatically __convert speech to text__
- Automatically remove __Personally Identifiable Information (PII)__ using Redaction
- Use cases: 
  - transcribe customer service calls
  - automate closed captioning and subtitling

# Polly

- Turn __text__ into __lifelike speech__ using deep learning
- Allowing you to create applications that talk

# Translate

- Natural and accurate __language translation__

# Lex
- __Amazon Lex__
  - same technology that powers Alexa
  - Automatic Speech Recognition (ASR) to convert speech to text
  - __Natural Language Understanding to recognize the intent of text, callers__
  - Helps build chatbots, call center bots
- __Amazon Connect__
  - Receive calls, create contact flows, cloud-based __virtual contact center__
  - Can integrate with other CRM systems or AWS  

# Comprehend
- For __Natural Language Processing – NLP__
- Fully managed and serverless service
- Uses machine learning to find insights and relationships in text


# Comprehend Medical

- Amazon Comprehend Medical detects and returns useful information in unstructured __clinical text__
- Uses __NLP__ to detect __Protected Health Information__ (PHI)


# SageMaker
- Fully managed service for __developers / data scientists__ to build __ML models__
- Typically, difficult to do all the processes in one place + provision servers
- Machine learning process (simplified): predicting your exam score

# Forecast

- Fully managed service that uses ML to deliver __highly accurate forecasts__
- Example: predict the future sales of a raincoat
- Use cases: Product Demand Planning, Financial Planning, Resource Planning

# Kendra
- Fully managed __document search__ service powered by Machine Learning
- Extract answers from within a __document (text, pdf, HTML, PowerPoint, MS Word, FAQs…)__

# Personalize

- Fully managed __ML-service__ to build apps with real-time personalized __recommendations__
- Same technology used by Amazon.com
- Integrates into existing websites, applications, SMS, email marketing systems, …

# Textract

- Automatically __extracts text__, handwriting, and data from any scanned documents using AI and ML
- Read and process any type of document (PDFs, images, …)


# Data & Analytics

## Athena

- Serverless query service to analyze data stored in Amazon S3
- Uses __SQL__ language to query the files
- Built on Presto engine
- Output stored in S3
- Supports CSV, JSON, ORC, Avro, and Parquet file format
- Commonly used with Amazon Quicksight for reporting/dashboards

__Performance__
 - Use __columnar data__ for cost-savings (less scan)
 - __Compress data__ for smaller retrievals (bzip2, gzip, lz4, snappy, zlip, zstd…)
 - Partition datasets in S3 for easy querying on virtual columns

__Amazon Athena – Federated Query__
- Allows you to run SQL queries across data stored in relational, non-relational, object, and custom data sources (AWS or on-premises)
- Store the results back in Amazon S3

# Redshift
- AWS managed __data warehouse__ (10x better performance than other data warehouses)
- Based on __PostgreSQL__
- Used for __Online Analytical Processing (OLAP)__ and high performance querying
- __Columnar storage__ of data with __massively parallel query execution__ in __SQL__
- Faster querying than __Athena__ due to indexes
- Need to provision instances as a part of the Redshift cluster (pay for the instances provisioned)
- Integrated with Business Intelligence (BI) tools such as __QuickSight or Tableau__
- Redshift Cluster can have __1 to 128 nodes (128TB per node)__
  - __Leader Node__: query planning & result aggregation 
  - __Compute Nodes__: execute queries & send the result to leader node

- No multi-AZ support (all the nodes will be in the same AZ)

__Loading data into Redshift__

- __S3__
  - Use __COPY command__ to load data from an S3 bucket into Redshift 
  - __Without Enhanced VPC Routing__
    - data goes through the public internet
  - __Enhanced VPC Routing__
    - data goes through the VPC without traversing the public internet
- __Kinesis Data Firehose__
  - Sends data to __S3__ and issues a __COPY command__ to load it into Redshift   
- __EC2 Instance__
  - Using __JDBC driver__
  - Used when an application needs to write data to Redshift
  - Optimal to write data in batches 

__Snapshots & DR__
- Snapshots are point-in-time backups of a cluster, stored internally in S3
- Snapshots are incremental (only what has changed is saved)
- You can restore a snapshot into a __new cluster__
- __Automated__
  - every 8 hours, every 5 GB, or on a schedule
  - Set retention between 1 to 35 days
- __Manual__
  - snapshot is retained until you delete it  

- __Feature to automatically copy snapshots into another region__

__Redshift Spectrum__
- Query data present in S3 without loading it into Redshift
- Need to have a Redshift cluster to use this feature
- Query is executed by 1000s of Redshift Spectrum nodes
- Consumes much less of your cluster's processing capacity than other queries

## OpenSearch

- Amazon OpenSearch is successor to __Amazon ElasticSearch__
- Used in combination with a database to perform __search operations on the database__
- Can search on any field, even supports __partial matches__
- Need to provision a cluster of instances (pay for provisioned instances)
- Supports Multi-AZ
- Used in Big Data
- Security through Cognito & IAM, KMS encryption, TLS
- Comes with __Kibana__ (visualization) & __Logstash__ (log ingestion)

## EMR

- EMR stands for “Elastic MapReduce”
- EMR helps creating __Hadoop clusters (Big Data)__ to analyze and process vast amount of data  
- The clusters can be made of __hundreds of EC2 instances__
- EMR comes bundled with __Apache Spark, HBase, Presto, Flink…__
- EMR takes care of all the __provisioning and configuration__
- __Auto-scaling__
- Integrated with __Spot Instances__

## QuickSight

- __Serverless machine learning-powered business intelligence service to create interactive dashboards__
- Fast, automatically scalable, embeddable
- Use cases:
  - Business analytics
  - Building visualizations
  - Get business insights using data
- Integrated with :
  - RDS
  - Aurora
  - Athena
  - Redshift
  - S3

# Glue

- Managed __extract, transform, and load (ETL)__ service
- Useful to prepare and transform data for __analytics__
- Fully __serverless__ service 

![image](https://user-images.githubusercontent.com/35028407/226724824-88501505-8756-4bc0-b00a-6fa512a75b61.png)

- Used to get data from a store, process and put it in another store (could be the same store)
- __Glue Job Bookmarks__: prevent re-processing old data
- __Glue Data Crawlers__ crawl databases and collect metadata which is populated in Glue Data Catalog
- Data lake is stored into S3

# Lake Formation 

- __Data lake = central place to have all your data for analytics purpose__
- Fully managed service that makes it easy to setup a __data lake__ in days
- Out-of-the-box source __blueprints__: S3, RDS, Relational & NoSQL DB…
- __Fine-grained Access Control for your applications (row and column-level)__


## Kinesis Data analytics

__Kinesis Data Analytics (SQL application)__
- Real-time analytics on __Kinesis Data Streams__ & __Firehose__ using SQL
- Add reference data from Amazon S3 to enrich streaming data
- Fully managed, no servers to provision
- Automatic scaling
- __Output__
  - Kinesis Data Streams: create streams out of the real-time analytics queries 
  - Kinesis Data Firehose: send analytics query results to destinations
- __Use cases:__
  - Time-series analytics
  - Real-time dashboards  
  - Real-time metrics

![image](https://user-images.githubusercontent.com/35028407/226729226-bad6dbde-3ed8-42b3-af2a-af867ffdd6f0.png)

__Kinesis Data Analytics for Apache Flink__
- Use Flink (Java, Scala or SQL) to process and analyze streaming data
- Use any Apache Flink programming features
- Flink does not read from Firehose (use Kinesis Analytics for SQL instead)
- SOurce :
  - Kinesis Data Streams 
  - Amazon MSK


# MSK Managed Streaming for Apache Kafka

- Alternative to Amazon Kinesis both allow to stream data
- Fully managed Apache Kafka on AWS
  - Allow you to create, update, delete clusters
  - MSK creates & manages Kafka brokers nodes & Zookeeper nodes for you
  - Deploy the MSK cluster in your VPC, multi-AZ (up to 3 for HA)
  - Data is stored on EBS volumes for as long as you want 

__MSK Serverless__

- Run Apache Kafka on MSK without managing the capacity
- MSK automatically provisions resources and scales compute & storage

# Big Data Ingestion Pipeline
- We want the ingestion pipeline to be fully serverless
- We want to collect data in real time
- We want to transform the data
- We want to query the transformed data using SQL
- The reports created using the queries should be in S3
- We want to load that data into a warehouse and create dashboards

# Monitoring & Audit

## CloudWatch

Serverless performance monitoring service

### Metrics

- CloudWatch provides metrics for every services in AWS
- __Metric__ is a variable to monitor (CPUUtilization, NetworkIn…)
- Metrics belong to __namespaces__
- __Dimension__ is an attribute of a metric (instance id, environment, etc…)
- Up to 10 dimensions per metric
- __2 Type__
  - Default metric
    - These metrics are provided out of the box and do not require any additional work on your part to configure   
  - Custom 
    - These metrics will need to be provided by using the CloudWatch agent installed on the host. 

 __EC2 Monitoring__
 - Must run a __CloudWatch agent__ on instance to push system metrics and logs to CloudWatch.
 - Instance role (IAM) must allow the instance to push logs to CloudWatch
 - EC2 instances have metrics every 5 minutes
 - With detailed monitoring (for a cost), you get metrics every 1 minute
 - Use detailed monitoring if you want to react faster to changes (eg. scale faster for your ASG)
 - __Available metrics in CloudWatch__:
    - CPU Utilization
    - Network Utilization
    - Disk Performance
    - Disk Reads/Writes
 - __Custom metrics__
    - Memory utilization (memory usage)
    - Disk swap utilization
    - Disk space utilization    
 
 __CloudWatch Logs Agent__
 - Old version of the agent
 - Can only send to CloudWatch Logs

__Can only send to CloudWatch Logs__
 - Collect additional system-level metrics such as RAM, processes, etc… 
 - Collect logs to send to CloudWatch Logs
 - Centralized configuration using SSM Parameter Store
 - Collected directly on your Linux server / EC2 instance
    - CPU (active, guest, idle, system, user, steal)
    - Disk metrics (free, used, total), Disk IO (writes, reads, bytes, iops)
    - RAM (free, inactive, used, total, cached)
    - Netstat (number of TCP and UDP connections, net packets, bytes)
    - Processes (total, dead, bloqued, idle, running, sleep)
    - Swap Space (free, used, used %)
    
 __Logs__
 
 - Used to store application logs
 - __Log Event__ This is the record of what happened. It contains a timestamp and the data. 
 - __Log Stream__ A collection of __log events__ from the same source create a __log stream__.Think of one
continuous set of logs from a single instance
 - __Log Group__ This is a collection of log streams. For example, you’d group all your Apache
web server logs across hosts together.
 
 - __Logs can be sent to__:
   - S3 buckets (exports)
   - Kinesis Data Streams
   - Kinesis Data Firehose
   - Lambda functions
   - ElasticSearch
 
 __Metric Filters__ can be used to filter expressions and use the count to trigger CloudWatch alarms. They apply only on the incoming metrics after the metric filter was created. Example filters:
   - find a specific IP in the logs
   - count occurrences of “ERROR” in the logs
   
 __Cloud Watch Logs Insights__ can be used to query(Sql) logs and add queries to CloudWatch Dashboards 
 
 __Subscription Filter__ 
  - To stream logs in real-time, apply a Subscription Filter on logs
  - Logs can take up to 12 hours to become available for exporting to S3 (not real-time)
  -  To store logs in real time in S3, use a subscription filter to publish logs to KDF in real time which will then write the logs to S3.
  - Logs from multiple accounts and regions can be aggregated using subscription filters
  
  ![image](https://user-images.githubusercontent.com/35028407/226958132-e901025b-f7bd-4b51-85a2-a5ee49cc1916.png)

 
 __Alarms__
 
- Alarms are used to trigger notifications for any metric
- Various options (sampling, %, max, min, etc…)
- Alarm States: OK, INSUFFICIENT_DATA, ALARM
- Alarm Targets:
  - Stop, Terminate, Reboot, or Recover an EC2 Instance
  - Trigger Auto Scaling Action 
  - Send notification to SNS
 

__CloudWatch Insights and Operational Visibility__

- __CloudWatch Container Insights__
  - Collect, aggregate, summarize metrics and logs from containers
  - __In Amazon EKS and Kubernetes, CloudWatch Insights is using a containerized version of the CloudWatch Agent to discover containers__
- __CloudWatch Lambda Insights__
  - Monitoring and troubleshooting solution for serverless applications running on AWS Lambda
  - Collects, aggregates, and summarizes system level metrics including CPU time, memory, disk, and network
- __CloudWatch Contributors Insights__
  - Find “Top-N” Contributors through CloudWatch Logs
- __CloudWatch Application Insights__
  - Automatic dashboard to troubleshoot your application and related AWS services

# CloudTrail

 - Provides governance, compliance and audit for your AWS Account
 - CloudTrail is enabled by default!
 - __Get an history of events / API__ calls made within your AWS Account
 - Can put logs from CloudTrail into __CloudWatch Logs__ or __S3__
 - __A trail can be applied to All Regions (default) or a single Region__
 - If a resource is deleted in AWS, investigate CloudTrail first
 - __Event retention: 90 days__
 - To keep events beyond this period, log them to S3 and use Athena
 
 __CloudTrail Events__
 
   - __Management Events__
  
     - Events of operations that modify AWS resources :
       - Creating a new IAM user
       - Deleting a subnet
     - Enabled by default
     - Can separate Read Events (that don’t modify resources) from Write Events (that may modify resources)
   
   - __Data Events__
     - By default, data events are not logged (because high volume operations)
     - Events of operations that modify data:
       - Amazon S3 object-level activity (ex: GetObject, DeleteObject, PutObject)
       - AWS Lambda function execution activity (the Invoke API)
       
   - __CloudTrail Insights Events__
     - Enable CloudTrail Insights to __detect unusual activity__ in your account
       - inaccurate resource provisioning 
       - hitting service limits
       - Bursts of AWS IAM actions
       
      - CloudTrail Insights analyzes normal management events to create a baseline and then continuously analyzes write events to detect unusual patterns. If that happens, CloudTrail generates insight events that
        - show anomalies in the Cloud Trail console
        - can can be logged to S3
        - can trigger an EventBridge event for automation

# Config
- Helps with auditing and recording __compliance__ of your AWS resources
- Record configurations changes over time
- __Evaluate compliance of resources using config rules__
- Does not prevent non-compliant actions from happening (no deny)
- Questions that can be solved by AWS Config:
   - Is there unrestricted SSH access to my security groups?
   - Do my buckets have any public access?
   - How has my ALB configuration changed over time? 
- You can receive alerts (SNS notifications) for any changes

- __Remediation__
  - automate remediation of non-compliant resources using __SSM Automation Documents__
    - AWS-Managed Automation Documents
    - Custom Automation Documents to invoke a Lambda function for automation 
  - You can set Remediation Retries if the resource is still non-compliant after auto remediation 

__CloudWatch vs CloudTrail vs Config__

- __CloudWatch__
  - Performance monitoring (metrics, CPU, network, etc…) & dashboards
  - Events & Alerting
  - Log Aggregation & Analysis
  
- __CloudTrail__
  - Record API calls made within your Account by everyone
  - Can define trails for specific resources 
  - Global Service
  
- __Config__
  - Record configuration changes
  - Evaluate resources against compliance rules
  - Get timeline of changes and compliance

# Trusted Advisor
- Analyze your AWS accounts and provides recommendation:
  - Cost Optimization
    - low utilization EC2 instances, EBS volumes, idle load balancers, etc.
    - Reserved instances & savings plans optimizations 
  - Performance
    - High utilization EC2 instances, CloudFront CDN optimizations 
    - EC2 to EBS throughput optimizations, Alias records recommendations
  - Security
    - MFA enabled on Root Account, IAM key rotation, exposed Access Keys
    - S3 Bucket Permissions for public access, security groups with unrestricted ports 
  - Fault Tolerence
    - EBS snapshots age, Availability Zone Balance
    - ASG Multi-AZ, RDS Multi-AZ, ELB configuration, etc 
  - Service limit
    - whether or not you are reaching the service limit for a service and suggest you to increase the limit beforehand 


# Cost Explorer
- Visualize, understand, and manage your AWS costs and usage over time
- Create custom reports that analyze cost and usage data. 
- Analyze your data at a high level: total costs and usage across all accounts
- __Forecast usage up to 12 months based on previous usage__


# Access Management

## Identity Access Management

- Groups are collections of users and have policies attached to them
- User can belong to multiple groups
- You should log in as an IAM user with admin access even if you have root access.
-
__Policies__

 - Policies are JSON documents that outline permissions for users, groups or roles
 - Two types:
   - __User based policies__
       - IAM policies define which API calls should be allowed for a specific user
   - __Resource based policies__
     - Control access to an AWS resource
     - Grant the specified principal permission to perform actions on the resource and define under what conditions this applies    
  
  - An IAM principal can access a resource if the user policy ALLOWS it OR the resource policy ALLOWS it AND there’s no explicit DENY.
  
__Roles__
 
 - Some AWS service will need to perform actions on your behalf
 - To do so, we will assign permissions to AWS services with IAM Roles

__Reporting Tools__

 - __Credentials Report__ : lists all the users and the status of their credentials (MFA, password rotation, etc.)
 - __Access Advisor__ : shows the service permissions granted to a user and when those services were last accessed

__Assume Role vs Resource-based Policy__
 - When you assume an IAM Role, you give up your original permissions and take the permissions assigned to the role
 - When using a resource based policy, the principal doesn’t have to give up their permissions
 - Kinesis data stream use IAM role 
 - SNS, SQS, Lambda, CloudWatch log, API Gateway ... are Ressource based policy

__Permission Boundaries__
- Set the maximum permissions an IAM entity can get
- __Can be applied to users and roles (not groups)__
- Used to ensure some users can’t escalate their privileges (make themselves admin)

## AWS Organizations

- __Global service__
- Manage multiple AWS accounts under an organization
  - The main account is the management account
  - Other accounts are member accounts  
- An AWS account can only be part of one organization
- __Consolidated Billing__ across all accounts (lower cost)
- Pricing benefits from aggregated usage of AWS resources
- API to automate AWS account creation (on demand account creation)
- Establish Cross Account Roles for Admin purposes where the master account can assume an admin role in any of the children accounts

__Organizational Units (OU)__
- Folders for grouping AWS accounts of an organization
- Can be nested

![image](https://user-images.githubusercontent.com/35028407/227026387-6dc7c349-2c0c-4410-876e-614b8c504a94.png)

__Service Control Policies (SCP)__
- IAM policies applied to OU or Accounts to restrict Users and Roles
- They do not apply to the management account (full admin power)
- Must have an explicit allow (does not allow anything by default – like IAM)
- __Explicit Deny__ has the highest precedence

## SSO 

- For __Single Sign-On__ called now __IAM Identity Center__
- One login (single sign-on) for all your
  - __AWS accounts in AWS Organizations__
  - Business cloud applications (e.g., Salesforce, Box, Microsoft 365, …)
  - SAML2.0-enabled applications 
  
- Identity providers
  - Built-in identity store in IAM Identity Center
  - 3rd party: Active Directory (AD), OneLogin, Okta

## Cognito

Amazon Cognito lets you add user sign-up, sign-in, and access control to your web and mobile apps quickly and easily. Amazon Cognito scales to millions of users and supports sign-in with social identity providers, such as Apple, Facebook, Google, and Amazon, and enterprise identity providers via SAML 2.0 and OpenID Connect.

__Cognito User Pools (CUP)__
- __Create a serverless database of user for your web & mobile apps__
- Integrate with API Gateway & Application Load Balancer
- Multi-factor authentication (MFA)
- __Federated Identities:__ users from Facebook, Google, SAML…

__Cognito Identity Pools (Federated Identity)__
- Provide AWS credentials to users so they can access __AWS resources directly__
- Provides temporary credentials (using STS) to users so they can access AWS resources
- Integrate with Cognito User Pools as an identity provider
- Example use case: provide temporary access to write to an S3 bucket after authenticating the user via FaceBook (using CUP identity federation)

__Cognito vs IAM: “hundreds of users”, ”mobile users”, “authenticate with SAML”__

# AWS Directory Services
- __AWS Managed Microsoft AD__
- Create your own AD in AWS, manage users locally, supports MFA
- Establish “trust” connections with your __on- premises AD__


__AD Connector__
- Directory Gateway (proxy) to redirect to on- premises AD, supports MFA
- Users are managed on the on-premises AD

__Simple AD__
- AD-compatible managed directory on AWS
- Cannot be joined with on-premises AD

## AWS Control Tower

- Easy way to __set up and govern a secure and compliant multi-account AWS environment__ based on best practices
- AWS Control Tower uses AWS Organizations to create accounts
- Benefits:
  - Automate the set up of your environment in a few clicks 
  - Automate ongoing policy management using guardrails
  - Detect policy violations and remediate them
  - Monitor compliance through an interactive dashboard
- __Guardrails__
  - Provides ongoing governance for your Control Tower environment (AWS Accounts)
  - __Preventive Guardrail__ – using SCPs (e.g., Restrict Regions across all your accounts)  
  - __Detective Guardrail__ – using AWS Config (e.g., identify untagged resources)

# Parameters & Encryption

## Key Management Service

- Anytime you hear “encryption” for an AWS service, it’s most likely KMS
- __Regional service (keys are bound to a region)__
- AWS manages encryption keys for us
- Provides encryption and decryption of data and manages keys required for it
- Encrypted secrets can be stored in the code or environment variables
- __Encrypt up to 4KB of data per call (if data > 4 KB, use envelope encryption)__
- Integrated with lAM for authorization
- Audit key usage with __CloudTrail__(to know who made call to KMS API)
- Need to set __IAM Policy & Key Policy__ to allow a user or role to access a KM

__KMS Keys__
- __KMS Keys is the new name of KMS Customer Master Key__
- __Symmetric (AES-256 keys)__
  - Single encryption key that is used to Encrypt and Decrypt
  - AWS services that are integrated with KMS use Symmetric CMKs 
  - You never get access to the KMS Key unencrypted (must call KMS API to use)
- __Asymmetric (RSA & ECC key pairs)__
  - Public (Encrypt) and Private Key (Decrypt) pair
  - Used for Encrypt/Decrypt, or Sign/Verify operations  
  - The public key is downloadable, but you can’t access the Private Key unencrypted
  - __Use case__: encryption outside of AWS by users who can’t call the KMS API

__Three types of KMS Keys__
- __AWS Owned Keys (free)__: SSE-S3, SSE-SQS, SSE-DDB (default key)
- __AWS Managed Key__: free (aws/service-name, example: aws/rds or aws/ebs)
- __Customer managed keys__ created in KMS: $1 / month
- __Customer managed keys imported__ (must be symmetric key): $1 / month + pay for API call to KMS ($0.03 / 10000 calls)

__Key Rotation__

- __Automatic__

  - __AWS-managed KMS Key__
    - automatic every 1 year 
  - __Customer-managed KMS Key__
    - must be enabled
    - automatic every 1 year  
- __Manual__
  - __Imported KMS Key__
    - only manual rotation possible using alias

__Key Policies__

- Control access to KMS keys, “similar” to S3 bucket policies
- Cannot access KMS keys without a key policy
- __Default Key Policy__
  - Created if you don’t provide a specific Key Policy
  - The default allow every one in your account to access the key
- __Custom KMS Key Policy__
  - Define users, roles that can access the KMS key
  - Define who can administer the key
  - Useful for cross-account access of your KMS key   


__Cross-region Encrypted Snapshot Migration__
- Copy the snapshot to another region with __re-encryption option__ using a new key in the new region (__keys are bound to a region__)

__Cross-account Encrypted Snapshot Migration__
- Create a Snapshot, encrypted with your own KMS Key (__Customer Managed Key__)
- __Attach a KMS Key Policy to authorize cross-account access__
- Share the encrypted snapshot
- (in target) Create a copy of the Snapshot, encrypt it with a new CMK in your account
- Create a volume from the snapshot

__KMS Multi-Region Keys__

- Identical KMS keys in different AWS Regions that can be used interchangeably
- Multi-Region keys have the __same key ID, key material, automatic rotation__
- Encrypt in one Region and decrypt in other Regions
- No need to re-encrypt or making cross-Region API calls
- KMS Multi-Region are NOT global (Primary + Replicas)
- Each Multi-Region key is managed independently
- __Use cases__: global client-side encryption, encryption on __Global DynamoDB, Global Aurora__

__AMI Sharing Process Encrypted via KMS__
- AMI in Source Account is encrypted with KMS Key from Source Account
- Must modify the image attribute to add a __Launch Permission__ which corresponds to the specified __target AWS account__
- Must share the __KMS Keys__ used to encrypted the snapshot the AMI references with the target account / IAM Role
- The IAM Role/User in the target account must have the permissions to DescribeKey, ReEncrypted, CreateGrant, Decrypt
- When launching an EC2 instance from the AMI, optionally the target account can specify a new KMS key in its own account to re-encrypt the volumes

## SSM Parameter Store
- Secure storage for configuration and secrets
- Optional Seamless Encryption using KMS
- Serverless, scalable, durable, easy SDK
- Security through IAM
- Notifications with Amazon EventBridge
- Integration with CloudFormation

__Parameter Tiers__

<img width="1137" alt="Capture d’écran 2023-03-23 à 07 38 54" src="https://user-images.githubusercontent.com/35028407/227123434-5dfbaf5c-9757-4fe4-8431-07a41d106b4c.png">

__Parameter Policies__
- Only supported in advanced tie
- Assign policies to a parameter for additional features
  - Expire the parameter after some time (TTL)
  - Parameter expiration notification
  - Parameter change notification


## Secrets Manager
- Newer service, meant for storing secrets
- Capability to force __rotation of secrets__ every X days(not available in __Parameter Store__)
- Automate generation of secrets on rotation (uses Lambda)
- Secrets are encrypted using KMS
- Mostly used for __RDS(MySQL, PostgreSQL, Aurora) authentication__
  - need to specify the username and password to access the database
  - link the secret to the database to allow for automatic rotation of database login info

__Secrets Manager – Multi-Region Secrets__
- Replicate Secrets across multiple AWS Regions
- Secrets Manager keeps read replicas in sync with the primary Secret
- Ability to promote a read replica Secret to a standalone Secret
- __Use cases__: multi-region apps, disaster recovery strategies, multi-region DB


## Certificate Manager
- Easily provision, manage, and deploy TLS Certificates
- Used to provide in-flight encryption for websites (HTTPS)
- Supports both public and private TLS certificates
- Free of charge for public TLS certificates
- __Automatic TLS certificate renewal__
- load TLS certificates on
  - Elastic Load Balancers (CLB, ALB, NLB)
  - CloudFront Distributions
  - APIs on API Gateway 
  - Cannot use ACM with EC2 


# Cloud Security

## Web Application Firewall

- Protects your application from common __layer 7 web exploits__ such as __SQL Injection__ and __Cross-Site Scripting (XSS)__
- __Layer 7 is HTTP__ (vs Layer 4 is TCP/UDP)
- Can only be deployed on
  - __Application Load Balancer__
  - __API Gateway__
  - __CloudFront__
  - __AppSync GraphQL API__ 
  - __Cognito User Pool__
 - WAF contains __Web ACL(Access Control List)__ containing rules to __filter requests__ based on: 
   - __IP addresses__
   - HTTP headers
   - HTTP body
   - URI strings
   - Size constraints (ex. max 5kb)
   - __Geo-match__ (block countries)
   - __Rate-based__ rules (to count occurrences of events per IP) for __DDoS protection__
 - __Web ACL are Regional except for CloudFront__

## AWS Shield

- __DDoS__: Distributed Denial of Service – many requests at the same time
- __AWS Shield Standard__
  - Free service that is activated for every AWS customer
  - Provides protection from attacks such a
    - __SYN/UDP Floods__
    - __Reflection attacks__
    - and other layer 3/layer 4 attacks  
 - __AWS Shield Advanced__
 - __DDoS mitigation service__ ($3,000 per month per organization)
  - Protect against more sophisticated attack on
    - EC2 instances
    - Elastic Load Balancing (ELB)
    - CloudFront
    - Global Accelerator
    - Route 53
   - 24/7 access to AWS __DDoS Response (DRP)__ team   


## Firewall Manager

- __Manage all the firewall rules in all accounts of an AWS Organization__
- Security policy: common set of __security rules__
  - WAF rules (Application Load Balancer, API Gateways, CloudFront)
  - AWS Shield Advanced (ALB, CLB, NLB, Elastic IP, CloudFront)
  - Security Groups for EC2, Application Load BAlancer and ENI resources in VPC
  - AWS Network Firewall (VPC Level)
  - Amazon Route 53 Resolver DNS Firewall
  - Policies are created at the region level

## GuardDuty

- Intelligent __Threat discovery__ to protect your AWS Account 
- Uses __Machine Learning algorithms__, anomaly detection, 3rd party data
- No management required (just enable)
- Input data includes:
  - CloudTrail Logs (unusual API calls, unauthorized deployments)
  - VPC Flow Logs (unusual internal traffic, unusual IP address)
  - DNS Logs (compromised EC2 instances sending encoded data within DNS queries)
  - EKS Audit Logs (suspicious activities and potential EKS cluster compromises)
- Can setup EventBridge rules to be notified in case of findings
- EventBridge rules can target AWS Lambda or SNS
- __Can protect against CryptoCurrency attacks (has a dedicated “finding” for it)__

![image](https://user-images.githubusercontent.com/35028407/227137981-b3bdb45b-3b18-441b-8b9d-9a8bd9731d47.png)


## Inspector

- Automated Security Assessments 
- For :
  - __EC2 instances__ using __System Manager (SSM) Agent__ running on EC2 instances 
  - __Amazon ECR__ - Assessment of containers as they are pushed to __ECR__
  - __Lambda Functions__ Identifies software vulnerabilities in function code and package dependencies

- Integration with __AWS Security Hub__
- Send findings to Amazon __Event Bridge__
- Gives a risk score associated with all vulnerabilities for prioritization


## Macie

- Amazon Macie is a fully managed __data security and data privacy service__
that uses __machine learning and pattern matching to discover and protect your sensitive data__ in AWS(ex in an S3 bucket).
- Macie helps identify and alert you to sensitive data, such as __personally identifiable information (PII)__
- Notifies through an __EventBridge event__

## Network Firewall
- Protect your entire Amazon VPC
- From Layer 3 to Layer 7 protection
- Any direction, you can inspect
  - VPC to VPC traffic
  - Outbound to internet
  - Inbound from internet
  - To / from Direct Connect & Site-to-Site VPN
- Internally, the AWS Network Firewall uses the AWS Gateway Load Balancer 
- Rules can be centrally managed cross- account by AWS Firewall Manager to apply to many VPCs

# HPC

## High Performance Computing

- Cloud is perfect for HPC
- __Cluster placement group__ for low latency inter-nodal communication
- __EC2 Enhanced Networking (SR-IOV)__
  - __Elastic Network Adapter (ENA)__
    - Supported in both Linux & __Windows__
  - __Elastic Fabric Adapter (EFA)__
    - Enhanced for HPC
    - Supported in __Linux only__
    - Leverages __Message Passing Interface (MPI)__ standard
    - __Bypasses__ the underlying Linux OS to provide low-latency networking

- __Automation and Orchestration__
  - __AWS Batch__
    - Used to run __single jobs that span multiple EC2 instances__ (multi-node) 
  - __AWS Parallel Cluster__
    - __Open-source cluster management__ tool to __deploy HPC on AWS__
    - Configure with text files
    - Automate creation of VPC, Subnet, cluster type and instance types
    - Ability to enable __EFA__ on the cluster
 

 

