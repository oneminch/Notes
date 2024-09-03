## [[Cloud Computing]]
## Pricing

- AWS pricing fundamentals:
    - **Compute**
    - **Storage**
    - **Data transfer** - pay only for data transferred *out* of the cloud
## Shared Responsibility Model (SRM)

> [!quote] Shared Responsibility Model
> Security and Compliance is a shared responsibility between AWS and the customer.

![Shared Responsibility Model](shared-responsibility-model.jpg)
- **Source**: [AWS](https://aws.amazon.com/compliance/shared-responsibility-model/) 
## Concepts

### Regions

- Cluster of data centers
- Most AWS services are region-scoped.

**What determines where to launch a new service?**
- ==Compliance== - Data never leaves a region w/o explicit permission
- ==Customer Proximity== - Reduced latency
- ==Service Availability== - Not all services are available in every region 
- ==Pricing== - Varies from region to region
### Availability Zones (AZ)

- Within each region, there are several separate yet connected availability zones, usually anywhere from 3 to 6.
- Each AZ contains one or more data centers, each with redundant power, networking and connectivity.
- AWS Region: Sydney (ap-southeast-2)
    - ap-southeast-2a, ap-southeast-2b, ap-southeast-2c
### Points of Presence (Edge Locations)

- Deliver content to end users with low latency. 
- 400+ in 90+ cities across 40+ countries.
## Services

- **Global**: IAM, Route 53, CloudFront, WAF
- **Regional**: EC2, Elastic Beanstalk, Lambda, Rekognition
### Global
#### Identity and Access Management (IAM)

- Root account is created by default and associated with an organization.
- Users
    - People within an organization 
    - Can be grouped
    - Can belong to multiple groups
    - Don't necessarily have to be part of a group
- Groups
    - Only contain users, not other groups
- Policies
    - JSON documents that define permissions
    - Assigned to users (Inline) or groups 
    - **Policy Structure**
        - `Version` - Policy language version (2012-10-17)
        - `Id` - Optional Policy identifier
        - `Statement` - One or more (required)
            - `Sid` - Optional statment identifier
            - `Effect` - '`Allow`' or '`Deny`' access
            - `Principal` - account/user/role to which the policy is applied
            - `Action` - list of allowed or denied actions
            - `Resource` - list of resources the actions apply to
            - `Condition` - Optional conditions that determine when the policy is in effect

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:AttachVolume",
                "ec2:DetachVolume"
            ],
            "Resource": "arn:aws:ec2:*:*:instance/*",
            "Condition": {
                "StringEquals": {"aws:ResourceTag/Department": "Development"}
            }
        }
        ...
    ]
}
```
- Best Practices
    - ![IAM Best Practices](iam-best-practices.png)
    - Credit: [Ultimate AWS Certified Cloud Practitioner](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/)

**Password Policies**
- Min length
- Whether changing own password is allowed
- Character types required, 
- Expiration date
- Prevent re-use of passwords (that were used within a certain date range)

**MFA Options**
- Virtual MFA devices - Single device / multi-token
    - e.g. Authy
- U2F - Single key / multi-user (root or IAM)
    - e.g. YubiKey
- Hardware
    - Key fob devices
##### Ways to Access AWS

- **AWS Management Console (Web UI)** - Password + MFA
- **AWS CLI** - Secret Access Keys
    - Alternative to using the management console web UI.
- **AWS SDK** - Secret Access Keys
    - Language and platform-specific libraries
    - Embedded within applications to manage AWS services programmatically

> [!note]
> Users manage their own access keys.
##### IAM Roles for Services

- Permissions assigned to AWS services, so they can perform actions on user's behalf.
- Common roles include EC2 roles, Lambda Roles, etc
##### IAM Security Tools

- **IAM Credentials Report** - Account-level
    - Lists all users and their credential status under an account
- **IAM Access Advisor** - User-level
    - Lists service permissions granted to a user along with its last access time
    - Can be used to revise policies using the Least Priviledge approach
### Regional
#### Elastic Compute Cloud (EC2)

- IaaS
    - Rent VMs (via EC2)
    - Data storage on virtual drives (via EBS)
    - Load distribution across machines (via ELB)
    - Service auto-scaling (via ASG)
- Can be configured to meet demands
    - OS
    - CPU & RAM
    - Storage Type and Amount
        - Network-attached (EBS / EFS)
        - Hardware (EC2 instance store)
    - Network Card
    - Firewall Rules
    - Bootstrap Script
        - Automated launch commands that run once (with root user permissions) on machine boot
            - e.g. Install updates/software, download files
- Instance types can be created that are optimized for different use cases 
    - Storage optimized
    - Network optimized
    - Memory optimized
    - Compute optimized
- General purpose instances provide a balance of the different resources. These are great for various types of workloads such as setting up web servers.
- An example name for an instance type can be `t2.micro`:
    - ==t== - instance class
    - ==2== - generation
    - ==micro== - size within instance class
##### Security Groups

- Fundamental to AWS network security.
- 'Firewall' around EC2 instances to control inbound and outbound traffic.
    - Access to ports
    - Authorized IP ranges (IPv4 & IPv6)
- Only contain allow rules
- By default, 
    - all inbound traffic is blocked.
    - all outbound traffic is authorized (stateful).
- Rules can be referenced by IP or by security group
- Can be attached to multiple instances
- Scoped to a region/VPC combination
- If application
    - times out, the issue is because of a security group
    - refuses connection, the issue is because of an application or launch error

> It is considered best practice to maintain one separate security group for SSH access.

**Common Ports**
- 21
    - File Transfer Protocol (FTP)
    - Upload files
- 22 
    - Secure Shell (SSH)
    - Log into a Linux machine
    - Also for Secure File Transfer Protocol (SFTP) - upload files using SSH
- 80
    - HTTP
    - Access unsecure websites
- 443
    - HTTPS
    - Access secure websites
- 3389
    - Remote Desktop Protocol (RDP)
    - Log into a Windows machine

> [!important]
> Never enter access keys into EC2 instance.
##### Purchase Options

- **On-Demand**
    - short-term, uninterrupted and unpredictable workloads
    - pay by the second (Linux / Windows)
    - pay by the hour (Other OS)
    - Highest cost with no upfront payment
    - No long term commitment
- **Reserved**
    - Reserve specific instance attributes: type, region, OS, tenancy
    - Reservation period: 1 & 3 years
    - Payment can be made all upfront (cheapest), partially upfront or none upfront.
    - Reserved Instances (RI)
        - Long, steady workloads (e.g. databases)
        - Can be bought or sold in the RI Marketplace 
        - Scope: Regional or Zonal
    - Convertible Reserved Instances
        - Long workloads with flexible instances
        - Attributes can be changed
- **Savings Plans**
    - 1 & 3 years
    - Long workload
    - Get a discount based on long-term usage
    - Commit to amount of usage (e.g. $X/hour for 1 or 3 years)
    - Usage past commitment is billed at On-demand pricing
    - Locked to a specific instance family and region
    - Flexibility across instance size, OS and tenancy
- **Spot Instances**
    - Most cost-efficient
    - Short workloads resilient to failure
        - e.g. image processing, data analysis
    - Less reliable; Can be lost
- **Dedicated Hosts**
    - Most expensive
    - Entire physical server
        - Visibility into low-level hardware
        - Targeted instance placement
        - Address strong regulatory or compliance needs
        - Useful for software with complicated licensing (BYOL)
    - Either on-demand or reserved
    - Per host billing
- **Dedicated Instances**
    - Hardware not shared with others
        - May be shared with other instances on same account.
    - No control over instance placement
    - Per instance billing
- **Capacity Reservations**
    - Reserved on-demand capacity in specific AZ for any duration
    - No time commitment or billing discounts
    - Short-term, uninterrupted workloads in a specific AZ
    - On-demand charge rate regardless of running instances

> [!question]
> Which option is suitable for a certain type of workload?
##### SRM for EC2

- The customer is responsible for 
    - OS patches and updates
    - Software and utilities installed on an instance
    - Security group rules, IAM roles and IAM user access
#### Storage
##### Elastic Block Store (EBS)

- network drive that can be (optionally) attached to instances while running
- because they are network-attached
    - there might be latency
    - they can be attached/detached quickly
- data is persisted even after termination
    - can be configured using the "delete on termination" attribute
        - can be managed via the console or CLI
        - enabled by default for root EBS
        - disabled by default for other EBS
- can only be mounted to one instance at a time
- are bound to a specific AZ
    - can be moved (backed up and restored) to a different AZ 
- provisioned capacity
    - billing occurs for all capacity purchased
###### Snapshots

- backups made at a certain point in time, so they can be restored
- recommended (but not required) to detach volumes before a snapshot
- can be copied across AZs or regions

- **Snapshot Archive** - cheap, but take longer to restore (24-72 hrs)
- **Recycle Bin** - rules can be set up to retain/retrieve deleted snapshots. 
    - retention period can be specified (1d - 1yr).
##### EC2 Instance Store

- high-perf hardware disk
- better I/O perf and throughput
- ephemeral
    - if hardware fails, there is risk of data loss
    - use cases - buffer, cache, temporary data
    - backing up is the responsibility of the customer
##### Elastic File System (EFS)

- cross-AZ, cross-VPC and cross-Region, managed network FS (NFS)
- can be mounted (shared) across hundreds of instances
- works with a Linux instance
- highly available, scalable and expensive
- no capacity planning - pay per usage
###### EFS Infrequent Access (EFS-IA)

- lower cost than standard EFS (92% lower)
- cost optimized for infrequently accessed files
- files can be moved to EFS-IA based on last access time
- enabled with a Lifecycle Policy
    - e.g. move files not accessed before 90 days to EFS-IA
##### SRM for EC2 Storage

- AWS responsible for 
    - replication of EBS/EFS data
- Customer responsible for 
    - data encryption 
    - backup procedures for EC2 instance store 
##### Amazon FSx

- launch fully-managed, third-party FS on AWS
###### FSx for Windows File Server (WFS)

- Windows-native shared FS
- built on WFS
- support SMB protocol and Windows NTFS
- integrated with Microsoft Active Directory
- can be accessed from AWS or on-premises infra
###### FSx for Lustre

- for high-perf computing (HPC)
    - ML, analytics, video processing
##### Amazon Machine Image (AMI)

- a customization of an instance: software, config, OS, monitoring
    - basically like a scaffold or template for an instance setup
- built for specific region but can be copied across.
- instances can be launched from:
    - A public AMI - AWS-provided
    - Custom AMI - custom made and maintained
    - Marketplace AMI - made/sold by a third-party
###### EC2 Image Builder

- used to automate the creation, maintenance, validation and testing of VMs or container images (AMIs)
- can be run on a schedule
#### Load Balancing

- Vertical Scalability (VS)
    - Scale up/down
    - increase size of instances
        - e.g. t2.micro -> t2.large
    - common for non-distributed systems such as databases
    - there is a limit to VS because of hardware capabilities
- Horizontal Scalability (HS) - Elasticity
    - Scale in/out
    - ASG, ELB
    - increase # of instances / systems
    - common on web applications
    - implies distributed systems
- High Availability (HA)
    - usually goes hand in hand with HS
    - running instances/systems in multiple AZs (at least 2) 
    - ASGs + ELBs in multi-AZ mode
    - Goal - survive a disaster such as loss of a data center

> [!note]
> Scalability is linked to but different from high availability (HA)

- Elasticity
    - cloud-native term referring to load-based auto-scaling
    - cost-optimized - pay per usage
    - matches demand

- Load Balancers (LB)
    - are servers that forward internet traffic to multiple instances
    - spread across multiple instances
    - expose a single point of access to apps
    - handle failure of instances
    - do regular health checks on instances
    - provide HTTPS
    - HA across AZs
##### Elastic Load Balancers (ELB)

- fully-managed LBs
###### Application Load Balancers (ALB)

- HTTP/HTTPS/gRPC protocols
- Layer 7
- Static DNS / URL
- HTTP routing
###### Network Load Balancers (NLB)

- ultra high-perf (millions of requests per second)
- Static IP
- TCP/UDP protocols
- Layer 4
###### Gateway Load Balancers (GWLB)

- Layer 3
- GENEVE protocol
- route traffic to firewalls managed on instances
- for intrusion detection / deep packet inspection
###### Classic Load Balancers

-  Retired 2023
- Layer 4 & 7
##### Auto-Scaling Groups (ASG)

- allow scaling as load changes
    - scale in (remove instances) for low loads
    - scale out (add instances) for high loads
- ensure there is a min and max # of machines running
- auto-register/de-register instances to an LB
- replace unhealthy instances
- cost optimized
###### Scaling Strategies

- Manual
- Dynamic
    - *Simple*
        - e.g. CPU usage < 30%, remove instances
    - *Target Tracking*
        - e.g. Avg. ASG CPU should stay at 40%
    - *Scheduled*
        - anticipated based on known usage patterns
        - e.g. upcoming concert ticket release date/time, increase min capacity to 10 at 6pm on Aug 10
    - *Predictive*
        - use ML to predict future traffic
        - auto-provision # of instances in advance
        - useful for time-based load patterns
#### Simple Storage Service (S3)

- allows storing objects (files) in buckets (directories)
- buckets 
    - must have a globally unique name (lowercase and numbers)
    - are ==created at the region level==
    - no concept of directories within buckets
- objects have a key which represents the full path of the object.
    - keys - made up of prefix and object name
        - e.g. `s3://my-bucket/dir1/.../image.png`
- max file size allowed - 5TB
- when uploading if file size exceeds 5GB, must use 'multipart upload'
- Use cases
    - Backup and storage
    - disaster recovery
    - archive
    - hybrid cloud storage
    - application hosting
    - media hosting
    - data lakes and big data analytics
    - software update delivery
    - static websites (if public access is enabled)
##### S3 Security

- **User-based** - IAM policies
- **Resource-based**
    - **Bucket Policies**
        - most common
        - bucket-wide rules
        - used to grant 
            - cross-account access
            - public access to bucket
            - force object encryption on upload
        - JSON-based
            - resources - buckets/objects
            - effect - allow/deny
            - actions - APIs allowed or denied
            - principal - account/user to which the policy applies
            - Public access is blocked by default. For public access policies to work, it needs to enabled.
    - **Object Access Control List**
        - fine-grain control
        - can be disabled
    - **Bucket Access Control List** (less common)
        - can be disabled

> [!note]
> An IAM principal can access an S3 object if:
> - user IAM policy ALLOWs it or resource policy ALLOWs it, AND
> - there is no explicit DENY

##### Versioning

- considered best practice
    - unintended deletion protection
    - easy rollbacks
- can be enabled at the bucket level
- same key overwrite changes the version number

> [!note]
> Files unversioned prior to enabling versioning will have a version ID of null.
> 
> Suspending versioning doesn't delete previous versions.
> 
> Deleting a file version automatically rollback it back to its previous version.

##### Replication

- can be of two types:
    - Cross-Region Replication
        - useful for compliance, low latency access and cross-account replications
    - Same Region Replication
        - useful for log aggregation
- versioning must be enabled in source and destination buckets
- buckets can be in different accounts
- copying is asynchronous
- proper IAM permissions must be given to S3
- version IDs are also replicated
- replication rules apply to objects created/uploaded after the creation of the rule unless one-time replication is enabled during rule creation
##### Storage Classes

- **Durability**
    - Extremely high durability of objects across multiple AZs
    - Same across all storage classes
- **Availability**
    - depends on storage class
        - e.g. Standard is not available 53 minutes/year
###### Amazon S3 Standard

- Frequently accessed data
- low latency, high throughput
- able to sustain two concurrent facility failures
- **Use Cases**: big data analytics, mobile/gaming apps, content distribution
###### Amazon S3 Standard Infrequent Access (IA)

- lower cost
- infrequently but rapidly accessed data
- **Standard IA**
    - 99.99% availability
    - used for backups and disaster recovery
- **One Zone IA**
    - 99.5% availability
    - high durability in a single AZ
        - data is lost if AZ is destroyed
    - used for secondary backups and recreatable data
###### S3 Glacier

- low cost
- cost for storage and object retrieval
- used for archival and backups
- encryption auto-enabled

- **Instant Retrieval**
    - milliseconds retrieval
    - great for once every quarter
    - minimum storage duration of 90 days

- **Flexible Retrieval**
    - minimum storage duration of 90 days
    - Expedited - 1 to 5 minutes

- **Deep Archive**
    - long term
    - minimum storage duration of 180 days
    - Standard - 12 hrs
    - Bulk - 48 hrs
###### S3 Intelligent Tiering

- small monthly monitoring and auto-tiering fee
- automatically move objects automatically b/n Access Tiers based on usage
- no retrieval charges

- **Frequent Access Tier** - (auto) default
- **Infrequent Access Tier** - (auto) objects not accessed for more than 30 days
- **Archive Instant Access Tier** - (auto) objects not accessed for more than 90 days
- **Archive Access Tier** - (optional) objects not accessed between 90 and 700+ days
- **Deep Archive Access Tier** - (optional) objects not accessed between 180 and 700+ days

> [!note]
> Lifecycle rules define accounts to move S3 objects between different storage classes.
##### Encryption

- Server-Side Encryption - default
- Client-Side Encryption
##### SRM for S3

- **AWS is responsible for:**
    - sustaining concurrent loss of data in 2 facilities
    - compliance validation
- **Customer is responsible for:**
    - versioning, policies, replication setup
    - logging and monitoring
    - data encryption at rest/in transit
#### AWS Snow Family (SF)

- offline
- highly secure, portable devices 
- used for 
    - Edge Computing (to collect and process data at the edge)
        - long-term - 1-3 yrs discounted pricing
    - Data Migration (to migrate data into/out of AWS)

- **Snowmobile**
    - EBs of data ($10^6$ TB)
    - each has 100PB capacity
    - secure, temperature controlled, GPS and video surveillance
- **Snowcone**
    - smaller (batteries and cables not included)
    - TBs of data
    - offline or online (AWS DataSync)
    - edge computing
    - storage
    - transfer
- **Snowball Edge**
    - offline and upto PBs of data
    - large data cloud migrations
    - decommisioned data centers
    - disaster recovery
    - recurring transfers

- OpsHub - software for managing SF devices
#### Storage Gateway

- way to expose/bridge S3 data on-premise
- encryption auto-enabled
- used for disaster recovery, backup/restore, tiered storage
- **Types**: Tape, File and Volume
#### Databases
##### Relational
###### Relational Database Service (RDS)

- managed SQL DB on AWS
- can't SSH into instances
- Online Transaction Processing (OLTP)
- free tier
- **Deployments**
    - Read Replicas
        - read scalability
        - upto 15 read replicas
        - write done to main DB
    - Multi-AZ
        - data read/written on main DB
        - can have one other AZ as failover for HA
    - Multi-Region
        - write done to main DB
        - great for disaster recovery
        - local reads - better performance
        - replication cost
###### Aurora DB

- AWS cloud optimized
    - better performance over MySQL / Postgres on RDS
- OLTP
- supports MySQL / Postgres
- more costly, but efficient
- no free tier
##### Redshift

- based on Postgres
- OLAP - online analytical processing
- analytics and data warehousing
- load data once every hour
- performant, HA and scalable (PBs of data)
- ==columnar== data storage (no rows)
- has SQL interface and BI tool integrations
- pay as you go
##### Non-Relational (NoSQL)

- Flexible, horizontally scalable
- high performance
- **Types**: KV, Document, Graph, In-memory, Search
###### ElastiCache

- managed Redis/Memcached
- in-memory DB - high perf, low latency
- useful for read-intensive workloads
###### DynamoDB

- managed, serverless, NoSQL KV DB
- replication across 3 AZs
- fast, consistent, distributed, scalable and HA
- millions of req/sed, trillions of rows, 100s of TB of storage
- single digit ms latency retrieval
- integrated with IAM
- auto-scaling / low cost
- Standard & IA table class

**DynamoDB Accelerator (DAX)**

- fully managed in-memory cache for DynamoDB
- microsecond latency

- ==**Global Tables**== - make a table accessible w/ low latency in multi-regions
    - **Active-Active Replication** - read/write to any region
###### Elastic MapReduce (EMR)

- create Hadoop clusters (Big Data) to analyze/process vast amount of data
- made of hundreds of EC2 instances
- provisioned and configured
- auto-scaling
- used for data processing, ML, web indexing, big data
###### Athena

- Serverless query service to perform analytics against S3 objects
- used for BI, analytics, reporting, analyzing logs
###### QuickSight

- Serverless ML-powered BI service to create interactive dashboards
- integratable with AWS services (e.g. RDS, Aurora DB)
- used for analytics, visualizations, business insights
###### Document DB

- implementation of MongoDB
- similar deployment concepts as Aurora
- managed, HA w/ replication across 3 AZs
- auto-scaling in storage (upto 64TB) & in workloads (millions of req/sec)
###### Neptune

- managed graph DB
- 3 AZ replication (HA),  15 read replicas 
- can store $10^9$ relations w/ ms latency
- used for recommendation engines, social network, fraud detection, knowledge graphs
###### Quantum Ledger DB (QLDB)

- recording financial transactions
- 3 AZ replication (HA),  15 read replicas 
- managed & serverless
- review history of all changes made to your application data
- immutable
- manipulate data with SQL
- *not decentralized*
###### Managed Blockchain

- decentralized and managed service to
    - join public blockchaing networks
    - create your own scalable private network
###### Glue

- serverless and managed ETL (Extract, Transform & Load) service
- prepare data for analytics
##### Database Migration Service (DMS)

- [ Source DB ] -> [ EC2 Instances Running DMS ] -> [ Destination DB ]
- Source DB remains available
- supports
    - homogeneous migration - e.g. Oracle -> Oracle
    - heterogeneous migration - e.g. MS SQL Server -> Aurora
##### SRM for Managed DBs

- **AWS**
    - monitoring, alerting, provisioning
    - OS patches
    - automated backup/restore, ops, upgrades
    - HA, VS, HS
- DBs run on EC2 instances have to be managed by customer.
#### Container Services

##### Elastic Container Service (ECS)

- Launch Docker containers on AWS
- Self-provisioned and self-managed infra (EC2 instances)
- AWS takes care of starting and stopping containers.
- ALBs can be integrated
##### Fargate

- Serverless ECS
- AWS runs containers based on resource requirements (CPU/RAM)
##### Elastic Container Registry (ECR)

- Private Docker registry on AWS where images are stored to be run by ECS or Fargate
#### Serverless Services

- No server provisioning / management
- e.g. S3, DynamoDB, Fargate
##### Lambda

- Event-driven virtual functions that are time and runtime limited
    - short executions
- On demand and auto-scaling
- Multi-lang support
- Pricing calculated per request and compute time
- **Lambda Container Images** - Lambda-specific way to run containers
    - Lambda is not ideal for generic Docker images
##### Amazon API Gateway

- Expose and proxy request to Lambda functions
- Fully managed, serverless and scalable
- support RESTful and WebSocket APIs
- support security, auth, API keys, API throttling, monitoring

##### AWS Batch

- Batches are 
    - jobs with a start and an end.
    - defined as Docket images and run on ECS
- AWS Batch provides managed batch processing at scale
- dynamically launch EC2/Spot instances with right amount of compute
- user schedules jobs, AWS takes care of the rest.
- no time limit
- support any runtime
##### LightSail

- Virtual servers, storage, databases and networking.
- low and predictable pricing
- simpler alternative to other services
    - for people with little cloud experience
- highly available, auto-scaling
- limited AWS integrations
#### Automation

##### CloudFormation

---
## Further

### Books 📚

- AWS Cookbook (John Culkin)

### Ecosystem 🏵

- Flightcontrol
- SST
- Serverless Framework

### Learn 🧠

- [AWS in Action (Playlist by Academind - YouTube)](https://www.youtube.com/playlist?list=PL55RiY5tL51rudermnWTq1LlGC1BL1g3l)

- [AWS Cloud Solutions Architect Professional Certificate - Coursera](https://www.coursera.org/professional-certificates/aws-cloud-solutions-architect)

- [AWS APAC Solutions Architecture (Forage)](https://www.theforage.com/simulations/aws-apac/solutions-architecture-ts4o)

- [Ultimate AWS Certified Developer Associate 2023 NEW DVA-C02](https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/)

- [Ultimate AWS Certified Solutions Architect Associate SAA-C03 - Udemy](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/)

### Resources 🧩

- [Tiny Technical Tutorials (YouTube)](https://www.youtube.com/@TinyTechnicalTutorials/videos)

### Videos 🎥

![Easily Deploy Full Stack Node.js Apps on AWS EC2](https://www.youtube.com/watch?v=nQdyiK7-VlQ)
