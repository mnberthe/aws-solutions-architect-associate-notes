# aws-solutions-architect-associate-notes
## Contents
### Compute services
- [EC2](#ec2)
- [Lambda](#lambda)
- [Elastic Beanstalk](#elasticbeanstalk)
- [Elastic Container Registry](#ecr)
- [Elastic Container Service](#ecs)
- [Elastic Kubernates Service](#EKS)
- [Fargate](#fargate)

### High availability and scalability 
 - [ELB](#elb)
 - [ASB](#asb)
 - [High Performance Computing (HPC)](#hpc)

### Storage
- [S3](#s3)
- [EBS](#ebs)
- [EFS](#efs)
- [FSx](#fsx)
- [Storage Gateway](#storagegateway)
- [Aws Backup](#awsbackup)
- [Snowball Edge](#snowballedge)
- [Snowmobile](#snowmobile)
- [Aws Transfer Family](#awstransferfamily)

### Database
- [RDS](#rds)
- [Aurora](#aurora)
- [DynamoDB](#dynamoDB)
- [DocumentDB](#documentDB)
- [ElastiCache](#elasticache)
- [Amazon Neptune](#netptune)
- [Redshift](#redshift)
- [QLDB](#qldb)
- [timestream](#timestream)

### Data & Analytics
- [Athena](#athena)
- [Redshift](#)
- [OpenSearch(ex ElasticSearch)](#openSearch)
- [EMR](#emr)
- [QuickSight](#quickSight)
- [Glue](#glue)
- [Lake formation](#lake-formation)
- [Kinesis Data analytics](#kinesis-data-analytics)
- [MSK Managed Streaming for Apache Kafka](#msk)
- [Big Data Ingestion Pipeline](#data-pipeline)

###  Migration
- [DMS(Database Migration Service)](#dms)
- [RDS & Aurora Migrations](#rds-aurora)
- [On premises strategies with aws](#on-premises)
- [MGN( Application migration service)](#mgn)
- [Transfering large datasets](#tranfer)
- [VMware cloud on aws](#vmWare)

### Disaster Recovery 
- [Disaster Recovery](#disaster)
- [Aws backup](#aws-backup)

### Decoupling applications 
- [SQS](#sqs)
- [SNS](#sns)
- [Kinesis](#kinesis)
- [Amazon MQ](#amazon-mq)
- [Event Brigde](#event-bridge)

### Machine Leanrning
- [Rekognito](#rekognito)
- [Transcribe](#transcribe)
- [Polly](#polly)
- [Translate](#emr)
- [Lex](#emr)
- [Comprehend](#emr)
- [Comprehend Medical](#emr)
- [SageMaker](#emr)
- [Forecast](#emr)
- [Kendra](#emr)
- [Personalize](#emr)
- [Textract](#emr)

### Networking
- [Route 53](#route53)
- [API Gateway](#api-gateway)
- [VPC](#vpc)
- [VPN](#vpn)
- [Direct connect](#direct-connect)
- [Transit Gateway](#transit-gateway)

### Content delivery
- [CloudFront](#cloudfront)
- [Global Accelerator](#global-accelerator)

### Parameters & Encryption
- [Key Management Service (KMS)](#kms)
- [SSM Parameter Store](#ssm)
- [Secrets Manager](#secret)
- [CloudHSM](#cloudHsm)
- [OpsWorks](#opsworks)


### Access Management 
- [Identity & Access Management (IAM)](#iam)
- [Cognito](#cognito)
- [Security Token Service (STS)](#sts)
- [Identity Federation in AWS](#identity-feration-in-aws)
- [AWS Organizations](#aws-organisation)
- [SSO]

### Cloud Security
- [AWS Shield](#aws-shield)
- [Web Application Firewall (WAF)](#waf)
- [Firewall Manager](#firewall-manager)
- [GuardDuty](#guard-duty)
- [Inspector](#inspector)
- [Macie](#macie)

### Monitoring & Audit
- [CloudWatch](#cloudWatch)
- [CloudTrail](#cloudTrail)
- [Config](#config)
- [X-Ray](#x-ray)
- [Trusted Advisor](#trusted-advisor)
- [Cost explorer](#cost-explorer)


# EC2 
EC2 (Elastic Compute Cloud) is an  __Infrastructure as a Service (IaaS)__\
Storage space:
 - Network attached __(EBS & EFS)__
 - Direct attached(Hardware) __(EC2 Instance Store)__\
Firewall rules: __security group__

Static IPv4 addresses known as Elastic IP addresses\
Bootstrap script (Execute only at first launch): EC2 User Data\
MetaData is data about your EC2 instance 
- This can include information such as private IP address, public IP address, hostname, security groups, etc.
- __Url to fetch metadata about the instance (http://169.254.169.254/latest/meta-data)__


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
__Cluster
- Grouping of instances within a single Availability Zone, same hardware
- Recommended for applications that need low network latency, high network throughput, or both.

__Spread__

- A spread placement group is a group of instances that are __each placed on distinct underlying hardware__.
- Recommended for applications that have a small number of critical instances that should be kept separate from each other
- Multi AZ, same region
- max 7 instances per group per AZ

__Partition__
- Each partition placement group has its own set of racks. Each rack has its own network and power source. 
- Multiple AZs in the same region
- Up to 100s of EC2 instances

__Networking with EC2__

You can attach 3 different types of __virtual networking cards__ to your EC2. \

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
