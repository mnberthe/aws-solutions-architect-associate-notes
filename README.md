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

# S3
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

- __S3 performance__
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

- __gp2/gp3 (SSD)__ General purpose SSD volume that balances price and performance for a wide variety of workloads
- __io1/io2 (SSD)__ Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads\ Attach the same EBS volume to multiple EC2 instances in the same AZ

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

__EFS__
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
- __Amazon FSx for Lustre__ When you need high-speed, high-capacity distributed storage. This will be for\ applications that do high performance computing (HPC), financial modeling, etc.\ Remember that FSx for Lustre can store data directly on S3
