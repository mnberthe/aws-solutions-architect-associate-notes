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

### Storage
- [S3](#s3)
- [EBS](#ebs)
- [EFS](#efs)
- [FSx](#fsx)
- [Storage Gateway](#storagegateway)
- [Snowball Edge](#snowballedge)
- [Snowmobile](#snowmobile)
- [Aws Transfer Family](#awstransferfamily)

### Database
- [RDS](#rds)
- [Amazon Aurora](#amazon-aurora)
- [DynamoDB](#dynamodb)
- [DocumentDB](#documentdb)
- [ElastiCache](#elasticache)
- [Amazon Neptune](#amazon-neptune)
- [Amazon QLDB](#amazon-qldb)
- [Amazon Timestream](#amazon-timestream)

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
- [PrivateLink](#privatelink)
- [Site-to-Site VPN](#site-to-site-vpn)
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
- [SSO](#sso)

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

# Compute services

## EC2 
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

__Cluster__
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

__Amazon S3 – Replication__
- __Must enable Versioning__ in source and destination buckets
- __Cross-Region Replication (CRR)__
- __Same-Region Replication (SRR)__
- Buckets can be in different AWS accounts
- After you enable Replication, only new objects are replicated
- __Cross-Region Replication (CRR)__
- After you enable Replication, only new objects are replicated
- You can replicate existing objects using S3 __Batch Replication__
- For DELETE operations:
  - Replicate delete markers from source to target (optional)
  - Permanent deletes are not replicated


__Security__

- __User based security__

- IAM policies define which API calls should be allowed for a specific user
- Preferred over bucket policy for fine-grained access control

- __Resource-Based__

 - __Bucket Policies__
   - Grant public access to the bucket
   - Force objects to be encrypted at upload
   - Cross-account access
 - __Object Access Control List (ACL)__ - applies to the objects while uploading
 - __Bucket Access Control List (ACL)__ - access policy that applies to the bucket

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
- A bucket policy can deny all PUT requests that don’t include the x-amz-server-sideencryption parameter in the request header


__CORS__
- If a client makes a cross-origin request on our S3 bucket, we need to enable the correct CORS headers
- You can allow for a specific origin or for *

__MFA Delete__
- MFA will be required to:
  - Permanently delete an object version
  - Suspend Versioning on the bucket
  
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
  - __Rapid Access__: Used for data that is accessed less frequently but requires rapid access when needed.
  - There is a low per-GB storage price and a per-GB retrieval fee
  - Use cases: __Disaster Recovery, backups__

__S3 Intelligent-Tiering__
  - Automatically moves your data to the most cost-effective tier based on how frequently you access each object.

__S3 Glacier__
- Low-cost object storage meant for archiving / backup
- Pricing: price for storage + object retrieval cost
- __Amazon S3 Glacier Instant Retrieval__
  - Millisecond retrieval, great for data accessed once a quarter  
  - Minimum storage duration of __90 days__
- __Amazon S3 Glacier Flexible Retrieval__
  - Expedited (1 to 5 minutes)  
  - Standard (3 to 5 hours)
  - Bulk (5 to 12 hours)
  - Minimum storage duration of 90 days

- __Amazon S3 Glacier Deep Archive – for long term storage__
  - Standard (12 hours)  
  - Bulk (48 hours)
  - Minimum storage duration of 180 days

__S3 Lifecycle Management__
- Lifecycle management automates moving your objects between thedifferent storage tiers, thereby maximizing cost effectiveness.

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
   

# FSX
__FSx for Windows__

- A managed Windows Server that runs __Windows Server Message Block (SMB)__ -based file services.
- __Designed for Windows__ and Windows applications.
- __Supports__ AD users, access control lists, groups, and security policies, along with Distributed File System (DFS) namespaces and replication.

__Amazon FSx for Lustre__

- A fully managed file system that is optimized for compute-intensive workloads
- High Performance Computing
- Machine Learning
- Media Data Processing Workflows


__How differ  EFS, FSx for Windows, or FSx for Lustre__
- __EFS__: When you need distributed, highly resilient storage for Linux instances and Linux-based applications.
- __Amazon FSx__ for Windows: When you need centralized storage for Windows-based applications, such as SharePoint\ Microsoft SQL Server, Workspaces, IIS Web Server, or any other native Microsoft application.
- __Amazon FSx for Lustre__ When you need high-speed, high-capacity distributed storage.\
  This will be for applications that do high performance computing (HPC), financial modeling, etc.\
  Remember that FSx for Lustre can store data directly on S3
 
# Disaster Recovery 
 ## Aws Backup
 
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
- Up to 5 Read Replicas
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas

__RDS Multi AZ for Disaster Recovery__

- With __Multi-AZ__, RDS creates an exact copy of your production database in another __Availability Zone__
- __Synchronous replication__
- One DNS name, so __connection string does not require to be updated__(both the databases can be accessed by one DNS name\
 which allows for automatic DNS failover to standby database)
- When failing over, __RDS flips the CNAME record__ for the DB instance to point at the standby, which is in turn promoted to become the new primary.
- Cannot be used for scaling as the standby database cannot take read/write operation

# Amazon Aurora
- Aurora is a proprietary technology from AWS (not open sourced)
- Postgres and MySQL are both supported as Aurora DB
- Aurora is “AWS cloud optimized” and claims __5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS__
- Aurora storage automatically grows in increments of 10GB, up to 128 TB.
- Up to 15 read replicas
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
- 
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

__Aurora Serverless__

- Optional
- Automated database instantiation and auto scaling based on actual usage
- Good for infrequent,intermittent or unpredictable workloads
- No capacity planning needed
- Pay per second, can be more cost effective

__Aurora Multi-Master__

- Optional
- In case you want immediate failover for write node (High availability)
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

# ElastiCache

- The same way RDS is to get managed Relational Databases…
- ElastiCache is to get managed Redis or Memcached
- Caches are in-memory databases with really high performance, low latency
- Helps make your application stateless, because it doesn’t have to cache locally

# DynamoDB

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

# DocumentDB
- Aurora is an “AWS-implementation” of PostgreSQL / MySQL …
- __DocumentDB is the same for MongoDB (which is a NoSQL database)__
- Fully Managed, highly available with replication across 3 AZ
- DocumentDB storage automatically grows in increments of 10GB, up to 64 TB.
- Automatically scales to workloads with millions of requests per seconds

# Amazon Neptune
- Fully managed __graph database__
- A popular graph dataset would be a __social network__
- Highly available across 3 AZ, with up to 15 read replicas
- Highly available with replications across multiple AZs

# Amazon QLDB

- QLDB stands for ”Quantum Ledger Database”
- A ledger is a book __recording financial transactions__
- Fully Managed, Serverless, High available, Replication across 3 AZ
- Used to review history of all the changes made to your application data over time
- __Immutable system: no entry can be removed or modified, cryptographically verifiable__
- You cannot update a record (i.e.,replace old content) in a ledger database. Instead, an update adds a new record to the databas
- __Use case__ : __financial transactions__, supply chain, cryptocurrencies, such as Bitcoin, blockchain

# Amazon Timestream

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
  
__VPC – Subnet__
-  AWS reserves __5 IP addresses (first 4 & last 1)__ in each subnet

__Internet Gateway (IGW)__
- Allows resources (e.g., EC2 instances) in a VPC connect to the Internet
- It scales horizontally and is highly available and redundant
- One VPC can only be attached to one IGW and vice versa
- Internet Gateways on their own do not allow Internet access
- Route tables must also be edited!

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

_ __Architecture__

![image](https://user-images.githubusercontent.com/35028407/224572054-495518a9-d85e-404a-9b66-2ade283a5c77.png)

__NAT Gateway with High Availability__

__NAT Gateway is resilient within a single Availability Zone__
- Must create __multiple NAT Gateways__ in __multiple AZs__ for fault-tolerance
- No cross-AZ failover needed because if an AZ goes down, all of the instances in that AZ also go down.

![image](https://user-images.githubusercontent.com/35028407/224572232-0dc02ac3-1e4d-4bad-86e6-3c138c2d2393.png)


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

__NACL vs Security Group__
_ NACL:
  - Firewall for subnets
  - Supports both Allow and Deny rules
  - __Stateless__ (both request and response will be evaluated against the NACL rules)
  
- Security Group:
  - Firewall for EC2 instances
  - Supports only Allow rules
  - __Stateful__ return traffic is automatically allowed,regardless of any rules

__VPC Peering__
- Privately connect two VPCs using AWS network
- Must not have overlapping CIDRs
- VPC Peering connection is NOT transitive
- Must update route tables in each VPC’s subnets to ensure requests destined to the peered VPC can be routed through the __peering connection__

![image](https://user-images.githubusercontent.com/35028407/224573874-c62c0540-a409-4208-8b00-e740a65fbd98.png)

![image](https://user-images.githubusercontent.com/35028407/224573884-adf59c75-6bb8-48bd-a973-073738009655.png)

- You can create VPC Peering connection between VPCs in different AWS accounts/regions

![image](https://user-images.githubusercontent.com/35028407/224573970-04a0a16b-3774-42d3-90b5-a96f503b8e31.png)


__VPC Endpoints__

![image](https://user-images.githubusercontent.com/35028407/224574183-409f676e-b68c-4024-8539-5d94595ae278.png)

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
  - __Gateway Endpoint__
    - Provisions a gateway
    - Must be used as a target in a route table 
    - Supports only __S3__ and __DynamoDB__


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
- __Low-cost hub-and-spoke model for network connectivity between a VPC and multiple on-premise data centers__
- Every participating network can communicate with one another through the VPN connection
- It operates over the public internet, but all traffic between the customer gateway and the AWS VPN CloudHub is encrypted.

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

- __Connection Types__
  - __Dedicated Connection__
    - A physical Ethernet connection associated with a single customer.  
    - 1Gbps,10 Gbps and 100 Gbps capacity
  - __Hosted Connection__
    - A physical Ethernet connection that an AWS Direct Connect Partner provisions on behalf of acustomer
    - 50Mbps, 500 Mbps, to 10 Gbps

![image](https://user-images.githubusercontent.com/35028407/224578908-3c1ca9ca-9760-42bb-a995-2cf8f49809e8.png)

- __Direct Connect Gateway__

  - Used to setup a Direct Connect to multiple VPCs from your data center, possibly in different regions but same account

![image](https://user-images.githubusercontent.com/35028407/224579112-faf44a8e-5246-4f13-83bc-482425b5b3ba.png)


# Transit Gateway

- __Transitive peering__ between thousands of VPCs and on-premise data centers using __hub-and-spoke (star) topology__
- Works with __Direct Connect Gateway__, __VPN Connection
- Regional resource, can work cross-region 
- You can peer Transit Gateways across regions
- Route Tables to control communication within the transitive network
- Supports __IP Multicast__ (not supported by any other AWS service)

![image](https://user-images.githubusercontent.com/35028407/224579481-a1e10b06-f6d8-4a64-8e30-66c78229f5d1.png)




