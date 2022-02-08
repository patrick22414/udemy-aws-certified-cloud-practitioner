# Udemy AWS Certified Cloud Practitioner Course

# Section 3 - What is Cloud

## Traditional IT

- Servers and data centres
    - Compute: CPU
    - Memory: RAM
    - Storage
    - Database
    - Network
        - Routers, switch, DNS server

## Cloud computing

- Cloud computing is the **on-demand delivery** of compute power, database storage, applications, and other IT resources
- Cloud services platform has **pay-as-you-go** pricing
- Choose your own type and size of computing resources as you need
- (Almost) instant access, with simple and friendly interface
- Types of cloud
    - Private cloud
    - Public cloud (Azure, AWS, GCP)
    - Hybrid cloud: keep some servers on premises, and extend to the cloud
        - Control of sensitive information
        - Flexibility and cost-effectiveness of public cloud
- 5 characteristics
    - On-demand self service
    - Broad network access
    - Multi-tenancy and resource pooling
    - Rapid elasticity and scalability
    - Measured service: pay by usage
- 6 advantages
    - Trade capital expense for operational expense
    - Massive economies of scale
    - Stop guessing capacity
    - Increase speed and agility
    - No maintainance cost
    - Global infrastructure

### Types of Cloud Computing

- IaaS (Infrastructure as a Service)
    - AWS EC2
- PaaS (Platform as a Service)
    - AWS Elastic Beanstalk
- SaaS (Software as a Service)
    - Machine learning, etc

## AWS Overview

- AWS 3 pricing fundamentals
    - **Compute**: pay for compute time
    - **Storage**: pay for data stored
    - **Network**: pay for data transferred OUT of the cloud
- AWS infrastructure
    - AWS Regions
        - A **Region** is a cluster of data centres
        - Most AWS services are **region-scoped**
        - eg. us-east-1, eu-west-3
    - AWS Availability Zones
        - Each region has multiple AZs
        - Each AZ is one or more discrete data centre(s)
        - Connected with high-bandwidth low-latency networking
        - eg, us-east-1a, us-east-1b
    - AWS Data Centres
    - AWS Edge Locations / Points of Presence
- How to choose an AWS Region?
    - **Compliance**
    - **Proximity** / latency
    - **Available services**: some services may not be availble in certain regions
    - **Pricing**
- Shared Responsibility Model
    
    ![Untitled](Udemy%20AWS%20Certified%20Cloud%20Practitioner%20Course%20e34cff4b4eba4ddf9c6bd8799aee46de/Untitled.png)
    

# Section 4 - IAM

- IAM = Identity and Access Management (a **global** service)
    - Root account
    - Users: people can be grouped
    - User can belong to 0 or multiple groups
    - Users or Groups can be assigned JSON documents called policies
    - least privileges principle
- AWS Access
    - AWS Management Console
    - AWS Command Line Interface (CLI)
    - AWS Software Developmer Kit (SDK)

## IAM Policies

- Version
- Id (id for the policy, optional)
- Statements
    - Sid (id for the statement, optional)
    - Effect (Allow / Deny)
    - Principal (acoount, user, role)
    - Action
    - Resource
    - Condition (optional)
- Password policy
    - minimum password length
    - require specific char types
    - allow IAM users to change their passwords
    - require change of password after some time (password expiration)
    - prevent password re-use
- MFA (multi-factor authentication)
    - Virtual MFA device
        - Google Authenticator / Authy
    - Universal 2nd factor (U2F) security key
    - Other hardware MFA devices

## IAM Roles

- assign permissions to AWS services (and other parties)

## IAM Security Tools

- IAM Credentials Report (account-level)
- IAM Access Advisor (user-level)

## IAM Guidelines & Best Practices

- Do NOT use root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Strong password policy
- MFA
- Roles for AWS services
- Access keys for CLI/SDK
- Audit permissions with IAM Credentials Report
- NEVER share users and access keys

# Section 5 - EC2

EC2 = Elastic Compute Cloud = IaaS

Many capabilities:

- virtual machines
- virtual drives

## EC2 config

- OS
- CPU
- RAM
- Storage (network-attached / hardware)
- Network
- Firewall (security group)
- Bootstrap script (EC2 User Data)

## EC2 Instance Types

[Amazon EC2 Instance Types - Amazon Web Services](https://aws.amazon.com/ec2/instance-types/)

- Instance types
    - General Purpose
    - Compute Optimised
    - Memory Optimised
    - ...
- Naming convention
    - eg: `m5.2xlarge`
    - `m`: instance class
    - `5`: generation
    - `2xlarge`: size

## EC2 Security Groups

- control traffic IN and OUT of EC2 instances
- only contain **allow** rules
- SG rules can reference by IP or by group
    - Reference by other SG allow instances with the referenced SG attached to go through
- Regulate:
    - Ports
    - Authorised IP ranges
    - Inbound network (outside → instance)
    - Outbound network (instance → outside)
- SGs and Instances are **many-to-many**
- Locked-down to region and VPC
- Good practice: maintain one separate SG for SSH access
- Connections blocked by SG result in time-out
- Inbound traffic is **blocked** by default
- Outbound trafffic is **authorised** by default
- SGs can refern
- Classic ports:
    - `22`: SSH
    - `21`: FTP
    - `22`: SFTP
    - `80`: HTTP
    - `443`: HTTPS
    - `3389`: RDP (Windows instances)

## EC2 Purchasing Options

- On-demand
- Reserved
    - Up to 75% discount
    - 1 year | 3 year | no upfront | partial upfront | all upfront
    - Convertible Reserve Instance
    - Scheduled Reserve Instance
- Spot
    - Up to 90% discount
    - You can lose instances
    - Failure resilient workloads
- Dedicated Host
    - Compliance requirements and server-bound software licenses
    - 3-year reservation
- Dedicated Instances

# Section 6 - EC2 Instance Storage

- **EBS** (Elastic Block Storage)
    - Network drive
    - Can persist data even after termination (unless Delete on Termination is set)
    - Bound to availability zones
    - Single attach at CCP level, multi-attach at Associate level
    - **EC2 Snapshots** for backup and transfer across AZs
- **AMI** (Amazon Machine Images)
    - Ready-to-use instance images with customisations
    - **EC2 Image Builder**: automated AMI build, testing and distribution
- **EC2 Instance Storage**
    - Ephemeral
    - Much faster than EBS
    - Good for cache / buffer / temp files
- **EFS** (Elastic File System)
    - Managed network file system that can be attached to 100s of EC2
    - cross availability zones
    - EFS Infrequent Access (**EFS-IA**)
- Amazon **FSx**
    - Lauch 3rd-party high-perf file systems on AWS
    - **FSx for Lustre** (for High Performance Computing)
    - **FSx for Windows File Server** (Windows-native)

# Section 7 - ELB & ASG

Elastic Load Balancing and Auto Scaling Groups

- Scalability
    - Vertical scalability (scaling up / down)
        - Increase the size of the instance: eg. t2.micro → t2.large
    - Horizontal scalability (elasticity) (scaling out / in)
        - Increase the number of instances
        - Auto Scaling Groups
        - Load Balancer
- High availability
    - Running your application in at least ***two AZs***
    - Goes hand in hand with horizontal scalability
    - Auto Scaling Group Multi-AZ
    - Load Balancer Mutli-AZ
- Scalability vs Elasticity vs Agility
    - S: the ability to accommodate larger load by scaling up or scaling out
    - E: the ability of “auto-scaling” for a scalable system; pay-per-use cost optimisation
    - A: not related. New IT resources are easily available to your developers

## Elastic Load Balancing (ELB)

- Load balancers are **servers** that forward internet traffic to multiple downstram EC2 instances
- Why?
- AWS provides 2 kinds of load balancers
    - Application LB (HTTP / HTTPS only) - Layer 7
    - Network LB (ultra-high performance, TCP allowed) - Layer 4
    - Gateway LB (new)
    - Classic LB (deprecating)

## Auto Scaling Group (ASG)

- Scale out / in to match load (with a min / max number of instances)
- Auto register new servers to LB
- Replace unhealthy servers
- Huge cost saving
- ASG Scaling Strategies
    - Manual scaling
    - Dynamic scaling
        - Simple / Step scaling
        - Target tracking scaling
        - Scheduled scaling
    - Predictive scaling

# Section 8 - S3

- “Infinitely scaling” storage
- Use cases:
    - Backup and storage
    - Disaster recovery
    - Archive
    - Hybrid Cloud storage
    - Application hosting
    - Media hosting
    - Data lakes & big data analytics
    - Software delivery
    - Static website
- Overview
    - Buckets (directories)
        - Globally uniquely named with certain naming convention
        - Defined in a Region
    - Objects (files)
        - **Key** is the full path
        - Example key: s3://my-bucket/my_folder/another_folder/my_file.txt
            - Bucket
            - Prefix
            - Object name
        - There is no concept of “directories” within a bucket, though the UI will trick you into thinking there is.
        - Max object size: 5TB
        - Multi-part upload from: 5GB

## S3 Security

- User based
    - IAM policies
- Resource based
    - Bucket policies
    - Object Access Control List (ACL) - finer grain
    - Bucket Access Control List - not common
- IAM permissions and resources policies are OR based
- Encryption
- Examples:
    - Public access - use bucket polices
    - IAM user access - use IAM permissions
    - EC2 instance access - use IAM roles
    - Cross-account access - use bucket policies
- S3 Bucket Policies
    - JSON policies

## S3 Website

## S3 Versioning

- Enabled at **bucket level**
- Files not versioned prior to enabling versioning will have version “null”
- Suspending versioning does not delete previous versions

## S3 Server Access Logging

- All access request will be logged into another S3 bucket

## S3 Replication

- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)
- Must enable versioning in src and dst buckets
- Must give proper IAM permissions to S3
- Copying is asynchronous
- Can copy across accounts

## S3 Storage Classes

- S3 Standard - General Purpose (99.99% av.)
- S3 Standard-IA (Infrequent Access) (99.9% av.)
    - Low cost, but retrieval fee
- S3 Intelligent-Tiering (99.9% av.)
    - When you don’t know it’s frequently or infrequently accessed
- S3 One Zone-IA (99.95% av.)
    - Secondary backups, data you can recreate
- Glacier - Archive
- Glacier Deep Archive
    - Lowest cost
    - Long term storage (years)
    - Long retrieval time + retrieval fee
- Object can transition between classes

## Durability & Availability

- Durability
    - How often do you lose a file
    - 99.999999999% durability - 11 9’s
- Availability
    - 99.99% availability - 53 mins per year

## S3 Encryption

- No encryption
- Server-side encryption
- Client-side encryption

## S3 Snow Family

- Snowcone (8TB)
- Snowball (80TB, petabyte-scale as a fleet)
- Snowmobile (<100PB, exabyte-scale)
- Data migration & Edge computing

# Section 9 - Databases

- Data in files vs Data is databases
    - Structured
    - Indexing
    - Relationships
- Relational Databases
    - SQL
- Non-relational Databases (NoSQL)
- Shared Responsibility of databases on AWS
    - AWS managed databases
        - 
    - EC2 hosted databases
        - 

## AWS RDS (Relational Database Service)

- Managed RD by AWS
    - Postgres
    - MySQL
    - ...
- RDS Read Replicas
    - (Same-AZ) Read replicas
        - Scale the read workload
        - 5 replicas at most
    - Multi-AZ read replicas
        - Failover
        - 1 failover AZ at most
    - Multi-Region
        - Disaster recovery for region issue
        - Local performance for global reads
        - Replication cost

## Amazon Aurora

- “AWS” cloud-optimised (5x MySQL perf, 3x Postgres pref)

## ElastiCache

- Managed Redis or Memcached
- In-memory databases
    - High perf and low latency
- Reduce load off databases

## DynamoDB

- Fully managed highly available with replication across 3 AZs
- **NoSQL** Key-value database
- Massive scale, distributedd, **serverless** database
- Low-latency retrieval
- DynamoDB Accelerator (DBX)
    - Fully managed in-memory cache for DynamoDB
    - 10x pref improvements
- DynamoDB Global Table
    - Low-latency read and write **across regions**
    - Active-active replication

## Redshift

- Based on PostgresSQL (SQL interface)
- **Analytics** and **data warehousing** (OLAP - online analytical processing)
- Load data once every hour
- Scale to PBs of data
- **Columnar**
- Massively Parallel Query Execution (MPP) with SQL support
- BI tools integresion (AWS Quicksight / Tableau)

## Amazon EMR (Elastic MapReduce)

- Hadoop clusters
    - a cluster can be made of hundreds of EC2 instances

## Amazon Athena

- Serverless query service to perform analytics against S3 objects
- Use compressed or columnar data for cost-saving

## Quicksight

- Serverless
    - Machine learning-powered
        - Business intelligence service
            - to create interative dashboards
- Integrated with RDS, Aurora, Athena, Redshit, S3...

## DocumentDB

- “AWS-implementation” for MongoDB
    - similar to Aurora to Postgres / MySQL
- NoSQL

## Neptune

- Managed **Graph** database

## QLDB

- Quantum Ledger Database
- Recording financial transactions
- Immutable; review all changes made to your data
- No decentralisation - compliant with financial regulations

## Amazon Managed Blockchain

- Decentralised
- Compatible with Hyperledger Fabric and Ethereum

## DMS (Database Migration Servive)

- Src DB → EC2 → Dst DB
- Sec DB remains available during migration
- Homogeneous or Heterogeneous migration

## AWS Glue

- Managed **extract, transform, and load** (ETL) service
- Prepare and transform data for analytics
- Serverless
- Glue Data Catalog

## Databases and Analytics Summary

- **Relational Databases - OLTP**: RDS & Aurora
- **Read replicas, Multi-AZ**, Multi-Region
- **In-memory database**: ElastiCache
- **Key-value database**: DynamoDB (with DynamoDB Accelerator cache)
- **Data warehousing** - OLAP: Redshift (SQL)
- **Hadoop Cluster**: EMR
- **Athena**: query data on S3 (serverless and SQL)
- **QuickSight**: serverless dashboards
- **DocumentDB**: “Aurora for MongoDB” (JSON and NoSQL)
- **Amazon QLDB**: financial ledger, centralised
- **Amazon Managed Blockchain**: managed blockchains, decentralised
- **Glue**: managed ETL
- **DMS**: Database Migration Service
- **Neptune**: graph database

# Section 10 - Other Services

## Containers

### ECS (Elastic Container Service)

- Launch Docker containers on AWS
- *You must provision the infrastructure yourself (EC2 instances)*
- AWS manages starting / stopping containers
- Application Load Balancer integration

### Fargate

- Launch Docker containers on AWS - serverless!
- *You do not provision the infrastructure*
- AWS runs containers based on your CPU/RAM need

### ECR (Elastic Container Registry)

- Private Docker register on AWS

## Lambda

- Event-driven
- Pay per request and compute time
- Versus EC2
    - Virtual functions - serverless!
    - Limited by time (vs limited by CPU and RAM)
    - Run on-demand
    - Automatd scaling

## API Gateway

- Build serverless (RESTful and WebSocket) APIs
- Client → *REST API* → API Gateway → *Proxy request* → Lambda → *CRUD* → DynamoDB

## AWS Batch

- Fully managed batch processing jobs at any scale
- Versus Lambda
    - No time limit
    - Any runtime (Docker images)
    - Rely on EBS or instance storage
    - Has servers (EC2s managed by AWS)

## Amazon Lightsail

- Much simpler
- For people with *little* cloud experience
- High availability, no auto-scaling, limited AWS integration

# Section 15 - VPC & Networking

## Virtual Private Cloud

- A VPC is a Regional resource
- **Subnets**: partition your network inside your VPC
    - Subnets are AZ resources
    - A **public subnet** is accessible from the internet
        - EC2, Load Balancer, ...
    - A **private subnet** is not accessible
        - EC2, Databases, ... (added security)
    - **Route Tables**: define access to the internet and between subnets
    - CIDR range: cidr.xyz
- Internet Gateways (IGW)
    - Connect VPC to the internet
- NAT Gateways (AWS-managed) & NAT instances (self-managed)
    - Allow your private subnets to access the internet while remaining private

## Security Groups and Network ACL

- NACL (Network Access Control List)
    - A firewall controls traffic to and from subnets
    - ALLOW or DENY
    - Rules include IP addresses
    - Is stateless: return traffic must be explicitly allowed
- Security Groups
    - A firewall controls traffic to and from an ENI / EC2 instance
    - ALLOW only
    - Rules include IP addresses and other SGs
    - Is stateful: return traffic is automatically allowed

## VPC Flow Logs and Peering

- Flow logs
    - Capture information about IP traffic going into your interfaces
        - VPC flow logs
        - Subnet flow logs
        - ENI (Elastic Network Interface) flow logs
    - Can capture flow to AWS managed services as well
    - Destination: AWS CloudWatch logs or S3 buckets
- Peering
    - Connect 2 VPCs
        - behave as if they are in the same network
    - NOT transitive

## VPC Endpoints

- Endpoints allow you to connect to AWS services using a *private network*
- **Endpoint Gateway**: connect to S3 and DynamoDB
- **Endpoint Interface**: connect to other services

## Site-toSite VPN & Direct Connect

- Connect on-premise Datacentres to AWS VPC
- Site-to-Site VPN
    - Encrypted connection through public internet
    - On-premise DC → Customer Gateway (CGW) → Virtual Private Gateway (VGW) → AWS
- Direct Connect (DX)
    - A physical connection between on-premise and AWS
    - More private
    - Expensive and takes time to establish

## Transit Gateway

- Transitive peering between *thousands* of VPCs and on-premises
- Hub-and-spoke
- Works with AWS VPCs, VPN connections, Direct Connect
- A single gateway