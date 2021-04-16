# CCP Exam Service Index                         

## Identity and Access Management (IAM)                                    

1. IAM MFA (Multi Factor Authentication)                 
2. AWS CLI (Command Line Interface)                  
3. AWS Software Development Kit (SDK)                    
4. AWS CloudShell: CLI in the cloud with pre-installed tools                  
5. IAM Roles: they are like users, but they are intended to be used not by physical people, but instead used by AWS Services                              
6. IAM Credentials Report: account level, this is a report that lists all your accounts users and the status of their various credentials                          
7. IAM Access Advisor: user level, it shows the service permissions granted to a user and when those services were last used                              

## Elastic Compute Cloud (EC2)                   

8. EC2 Security Group: control traffic in or out of EC2 instances.                      
-> 22 = SSH (Secure Shell) - log into a EC2 instance on Linus                    
-> 21 = FTP (File Transport Protocol) - upload files on to a file share                     
-> 22 = SFTP (Secure File Transport Protocol) - upload files using SSH                             
-> 80 = HTTP - access unsecured website                   
-> 443 = HTTPS - access secured website                
-> 3389 = RDP (Remote Desktop Protocol) - log into a Windows Instance                                 
9. EC2 Instance type:               
-> General Purpose (balanced, for web server. e.g. t2)                        
-> Compute Optimized (HPC, ML, batch processing. e.g. c5 or c6)                   
-> Memory Optimized (float point calculation, graphic processing. e.g. e.g. r)                
-> Storage Optimized (OLTP system, database. e.g. i, d or h1)                                 
10. EC2 Instance Connect: alternative way to connect to EC2 instance from AWS (need SSH rules in the Security Group)                          
11. EC2 Instance Launch type:                       
-> On-Demand                 
-> Reserved (1 or 3 years): 1. Reserved (75% discount) 2. Convertible Reserved (t2.large to c3.large, 54% discount) 3. Scheduled Reserved                  
-> Spot Instance (90% discount)               
-> Dedicated Host: book an entire physical server, control instance placement, 3 years period, address compliance requirement and can use existing server-bound software licenses.                                              
12. EC2 Dedicated Instance: these instance run on hardware that is dedicated to you, may share hardware with other instances in the same account, no hardware control (e.g. instance placement), software-version of Dedicated Host                                

## EC2 Instance Storage                          

13. EBS (Elastic Block Store): network drive, persist data, mounted to one instance at a time (CCP), bound to AZ.                   
14. EBS Snapshots: a back up of EBS volume, can also copy snapshots across AZ or Region, and can be used to restore into an EBS volume in another AZ                  
15. AMI (Amazon Machine Image): represent customisation of EC2 Instance (add your own SW, OS etc, faster boot and configuration), built for a specific region, can be copied across Region                        
16. EC2 Image Builder: automate the creation, maintain, validate and test of Virtual Machine or images                           
17. EC2 Instance Store: disk space that is attached directly (physically) with the server. High performance, hardware-attached volume for EC2 instance, lost their storage if they are stopped (ephemeral)                                 
18. EFS (Elastic File System): managed NFS (network file system) that can be mounted of 100s of EC2 at a time. EFS makes it a shared network file system. Only works with Linux EC2 instance and works across AZ.                                    

## ELB & ASG                           

19. Lingo for Cloud Services:                                    
-> Vertical Scalability: increase the size of the instance. common for non-distributed system like database                   
-> Horizontal Scalability: increase the number of instances/systems for your applications. common for distributed system              
-> Availablility: run your application in at least 2 AZ on AWS. Disaster Recovery                
-> Scalability: ability to accomodate a larger laod by making the hardware stronger (scale up, vertical) or by adding nodes (scale out, horizontal)               
-> Elasticity: more cloud native, auto-scaling so that the system scale based on the load                         
-> Agility: usually distractor, reduce the time to make resource available fast                               
20. ELB (Elastic Load Balancer): a server that will forward internet traffic down to multiple servers (EC2 instance downstream for example)                      
-> Application Load Balancer (HTTP/HTTPS only) - layer 7                   
-> Network Load Balancer (ultra-high performance, allows for TCP, lower level protocol) - layer 4                
-> Classic Load Balancer (slowly retiring) - Layer 4 and 7                     
-> Gateway Load Balancer (new)                                           
21. ASG (Auto Scaling Group): create automatically EC2 instance (or servers based on traffic or demand)                                    


## S3                       

22. S3: infinitely scaling storage.                       
-> bucket: globally unique name across all regions all accounts, defined at region level, act like directory                   
-> object: each object has a Key which is the FULL path to the object. Key = prefix + object name                                  
23. S3 Bucket Policy: bucket wide rules from the S3 console attached directly to your S3 bucket, JSON                        
24. S3 Website: S3 is a great way to host static website and have them accessible on the www. Make sure Bucket Policy allows public read                 
25. S3 Versioning: enabled at the bucket level                           
26. S3 Server Access Logging: log all access to S3 buckets for audit purpose, record these logs in another S3 bucket                             
27. S3 Replication: can be Cross Region Replication (CRR) or Same Region Replication (SRR), must enable Versioning                       
28. S3 Storage Class (99.999999999% 11 9s):                             
-> S3 Standard: general purpose, 99.99% availablity (53 minute a year not available), sustain up to 2 concurrent facility failures                   
-> S3 Standard - Infrequent Access (IA): less frequent access, rapid access when needed. 99.9% availability. sustain up to 2 concurrent facility failures    
-> S3 One Zone Infrequent Access: same as IA but 1 Az. 99.5% availability, 20% cheaper than IA                  
-> S3 Intelligent Tiering: 99.9% availability. cost-optimized by auto moving objects between 2 access tier on changing access patterns (frequent vs  infrequent access)                             
-> S3 Glacier: very low cost (GB/mth). Data returned for years. 3 ways to retrieve data: 1. Expedited (1 to 5 min) 2. Standard (3 to 5 hours) 3. Bulk (5 to 12 hour, multiple files)                     
-> S3 Glacier Deep Archive: cheapest of all S3. 1. Standard (12 hours) 2. Bulk (48 hours)                     
29. Lifecycle rules: transition objects between storage classes                   
30. S3 Object Lock: adopt WORM (Write Once Read Many) model, write the file once to S3 bucket, then block that object version to be deleted for a specific amount of of time                      
31. Glacier Vault Lock: create a lock policy and it prevents future edits to that file, and noone can delete that policy (even admin). For compliance and data retention                                
32. AWS Snow Family:                   
-> Snowball Edge (up to PB, tens of TB): data migration and edge computing. move TBs or PBs of data in/out of AWS. Snowball Edge Storage Optimized (80TB) vs Snowball Edge Compute Optimized (42TB, with powerful computing resource), 1/3 years long term deployment available                                  
-> Snowcone (up to 24 TB): data migration and edge computing. much smaller device, 8TB. send back to AWS offline or use AWS DataSync to send data. 1/3 years long term deployment available                   
-> Snowmobile (up to EB): actual truck transber EBs of data.                            
33. AWS OpsHub: manage Snow Family instead of CLI                        
34. Storage Gateway: bridge between on-premises data and AWS storage                              


## Database & Analytics                      

35. RDS (Relational Database Service):SQL, allows you to create databases in the cloud that are managed by AWS: Postgres, MySOL, MariaDB, Orcale etc, Online Transaction Processing (OLTP)              
36. Aurora:SQL, proprietary technology from AWS, supports PostgreSQL and MySQL, AWS cloud optimised compared to RDS on these 2 type of DB. auto grow in increment 10GB, up to 64TB                      
37. RDS Read Replica: some copies of your RDS databases and our application can read from these. Writing data is only done to the main database (not the replicas)               
-> multi AZ: Failover in case of AZ outage. The Failover DB is not accessable until there is issue with main DB. can only have 1 other AZ as failover                       
-> multi region: disaster recovery (region issue), local performance boost, but need replication cost (inter region)                              
38. ElastiCache: cache are in-memory databases with high performance, low latency, reduce load off databases for read intensive workloads                 
39. DynamoDB:NOT SQL, NoSQL database (not a relational database, key/value database). Single-digit millisecond latency - low latency retrieval, serverless                  
40. DAX (DynamoDB Accelerator): fully managed in-memory cache for DynamoDB. Single-digit millisecond latency                       
41. Redshift: SQL, Online Analytical Processing (OLAP), analytics and data warehousing. Load data once every hour. Columnar storage of data. Integrate with AWS QuickSight or Tableau                        
42. Amazon EMR (Elastic MapReduce): not really databasem helps create Hadeep clusters to analyze/process vast amount of data. The clusters made of hundredds of EC2 Instance                      
43. Athena: SQL, fully serverless database, query data in S3, pay per query, output results back to S3                               
44. Amazon QuickSight: serverless machine learning-powered business intelligent service to create interactive dashboards                     
45. DocumentDB: Not SQL, "AWS-implementation" of MongoDB, used to store, query and index JSON data                       
46. Neptune: fully managed graph database (sort of Not SQL)                     
47. Amazon QLDB (Quantum Ledger Database): fully managed serverless ledger, used to review history of all the changes made to your application data. Immutable system. Financial transaction or ledger purpose. Centralised                                                 
48. Amazon Managed Blockchain: managed service compatibile with Hyperledger Fabric, Ethereum. decentralised blockchain. used to execute transaction without the need for a trusted, central authority                    
49. DMS (Database Migration Service): run EC2 with DMS software to transfer data from source DB to target DB               
-> homogeneous migration: Oracle to Oracle                       
-> heterogeneous migration: Microsoft SQL Server to Aurora                       
50. Glue: manage extract, transform, and load (ETL) serverless service                         

## Other Compute Service                  

51. ECS (Elastic Container Service): launch Docker container on AWS. Need to provision infra (EC2) beforehand                   
52. Fargate: launch Docker containers. You do not provision the infrastructure, serverless                        
53. ECR (Elastic Container Registry): private docker registry on AWS, a place to store Docker Image so that they can be run by ECS and Fargate                    
54. Lambda: serverless, function in the cloud. Pay per invokation + duration x compute power, 15 minutes time limit                   
55. Amazon API Gateway: for exam, for building a serverless HTTP API. Lambda function is not exposed as an API by external client. Need API Gateway  to proxy the request.                        
56. Batch: fully managed batch processing at any scale. Batch jobs are defined as Docker Images and run on ECS (auto scale with EC2 instance/ spot instance)                     
57. LightSail: kind of stand-alone service. get virual servers, storage, databases and networking in one place. low and predictable pricing. for people with little cloud experience, limited AWS integration                    

## Deployment & Managing Infrastructure at Scale

58. CloudFormation: Infrastructure as code, template can be in yaml form            
59. Beanstalk: platform as a service (PaaS), a developer centric view of deploying an application on AWS, with known architecture           
60. CodeDeploy: deploy our code (application), hybrid service. can auto upgrade version of application in EC2 instance in a single interface           
61. CodeCommit: code repository                 
62. CodeBuild: retrieve code from CodeCommit and build the code and then we will avve ready-to-deploy artifact        
63. CodePipeline: orchestrate different setps to have the code automatically push to production (e.g. CodeCommit -> CodeBuild->CodeDeploy->Beanstalk)                  
64. CodeArtifact: artifact (dependencies) management, CodeBuild can retrieve dependencies from CodeArtifact          
65. CodeStar: unified UI to easily manage SW development activites in one place. Behind the scene it will create CodeCommit repo, a CodeBuild build process, a CodeDeploy, a CodePipeline                      
66. Cloud9: cloud IDE                  
67. SSM (Systems Manager): manage fleet of EC2 and On-premises system at scale, run command across ALL your servers, patch your fleet of EC2 and On-premises servers, need install SSM Agent in the EC2 instances (Linux and Ubuntu has it by default)                    
68. OpsWorks: managed Chef and Puppet, perform server configuration automatically               

## Leveraging the AWS Global Infrastructure      




