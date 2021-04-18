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
17. EC2 Instance Store: disk space that is attached directly (physically) with the server. High performance, hardware-attached volume for EC2 instance, lost their storage if they are stopped (ephemeral). An instance store provides temporary block-level storage for your EC2 instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for the temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers. Instance storage is temporary, data is lost if instance experiences failure or is terminated.                                                   
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
39. DynamoDB:NOT SQL, NoSQL database (not a relational database, key/value database). Single-digit millisecond latency - low latency retrieval, serverless. Amazon DynamoDB is a key-value and document database that delivers single-digit millisecond performance at any scale. It's a fully managed, multi-Region, multi-master, durable database with built-in security, backup and restore, and in-memory caching for internet-scale applications. DynamoDB offers flexible schema and can easily handle unstructured data.                               
40. DAX (DynamoDB Accelerator): fully managed in-memory cache for DynamoDB. Single-digit millisecond latency                       
41. Redshift: SQL, Online Analytical Processing (OLAP), analytics and data warehousing. Load data once every hour. Columnar storage of data. Integrate with AWS QuickSight or Tableau. Amazon Redshift is a fully-managed petabyte-scale cloud-based data warehouse product designed for large scale data set storage and analysis.                                       
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
54. Lambda: serverless, function in the cloud. Pay per invokation + duration x compute power, 15 minutes time limit. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.                                 
55. Amazon API Gateway: for exam, for building a serverless HTTP API. Lambda function is not exposed as an API by external client. Need API Gateway  to proxy the request.                        
56. Batch: fully managed batch processing at any scale. Batch jobs are defined as Docker Images and run on ECS (auto scale with EC2 instance/ spot instance). AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS.                     
57. LightSail: kind of stand-alone service. get virual servers, storage, databases and networking in one place. low and predictable pricing. for people with little cloud experience, limited AWS integration                    

## Deployment & Managing Infrastructure at Scale

58. CloudFormation: Infrastructure as code, template can be in yaml form            
59. Beanstalk: platform as a service (PaaS), a developer centric view of deploying an application on AWS, with known architecture, NOT serverless           
60. CodeDeploy: deploy our code (application), hybrid service. can auto upgrade version of application in EC2 instance in a single interface. AWS CodeDeploy is a service that automates code deployments to any instance, including EC2 instances and instances running on premises.                      
61. CodeCommit: code repository                 
62. CodeBuild: retrieve code from CodeCommit and build the code and then we will avve ready-to-deploy artifact        
63. CodePipeline: orchestrate different setps to have the code automatically push to production (e.g. CodeCommit -> CodeBuild->CodeDeploy->Beanstalk)                  
64. CodeArtifact: artifact (dependencies) management, CodeBuild can retrieve dependencies from CodeArtifact          
65. CodeStar: unified UI to easily manage SW development activites in one place. Behind the scene it will create CodeCommit repo, a CodeBuild build process, a CodeDeploy, a CodePipeline                      
66. Cloud9: cloud IDE                  
67. SSM (Systems Manager): manage fleet of EC2 and On-premises system at scale, run command across ALL your servers, patch your fleet of EC2 and On-premises servers, need install SSM Agent in the EC2 instances (Linux and Ubuntu has it by default). AWS Systems Manager gives you visibility and control of your infrastructure on AWS. Systems Manager provides a unified user interface so you can view operational data from multiple AWS services and allows you to automate operational tasks across your AWS resources. With Systems Manager, you can select a resource group and view its recent API activity, resource configuration changes, related notifications, operational alerts, software inventory, and patch compliance status. You can also take action on each resource group depending on your operational needs. Systems Manager provides a central place to view and manage your AWS resources, so you can have complete visibility and control over your operations.                                    
68. OpsWorks: managed Chef and Puppet, perform server configuration automatically               

## Leveraging the AWS Global Infrastructure      

69. Route 53: global service, managed DNS (Domain Name System).           
-> simple routing policy (only one with no health check)               
-> weighted routing policy                
-> latency routing policy          
-> failover routing policy             
70. CloudFront: contend delivery network (CDN), global service, improves performance by caching the content of your websites at different edge locations             
71. S3 Transfer Acceleration: S3 bucket are linked to region, S3 Transfer Acceleration increase transfer speed by transfering files to an AWS edge location which will forward the dta to the S3 bucket in the target region (using private AWS network)                 
72. AWS Global Accelerator: when we use this accelerator, we are connected to an edge location closest to us and that edge location will be routing traffic directly to the target instances via private AWS network                
73. AWS Outposts: "server racks" that offers the same AWS infra, services, API and tools to build your own application on-premises just as in the cloud. This service extend cloud service onto your own infrastructure on-premises system             


## Cloud Integration          

74. SQS (Simple Queue Service): fully managed serverless service to decouple applications. Producers will send message into a queue and stored there, then they can be read by consumers who will be polling the queue (i.e. requesting message from the queue), message will be deleted after they are used by consumers                
75. SNS (Simple Notification Services:): event publisher only sends message to one SNS topic, and the SNS topic will send the message to downstream event subscribers                
76. Kinesis: real-time big data streaming          
77. Amazon MQ: managed Apache ActiveMQ which enable traditional protocols such as MQTT, AMQP, STOMP, Openwire, WSS etc, only used if company is migrating to the cloud and needs to use one of these open protocols           

## Cloud Monitoring           
78. CloudWatch: provides metrics for every service in AWS (CPUUtilization, NetworkIn, etc), can create CloueWatch dashboards to view all metrics at the same time. Amazon CloudWatch is a monitoring and observability service built for DevOps engineers, developers, site reliability engineers (SREs), and IT managers. CloudWatch provides data and actionable insights to monitor applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. This is an excellent service for building Resilient systems.                          
79. CloudWatch Alarm: used to trigger notification for any metrics (once above a threshold, trigger a CloudWatch Alarm action such as EC2 actions or ASG action or SNS notification)             
80. CloudWatch Logs: the logs collect from various services like Beanstalk/ECS/Lambda, enable real-time monitoring of logs. Needs CloudWatch log agents on EC2 machines or on-premises servers, hybrid service, by default no logs from EC2 instance go to CloudWatch. You can use Amazon CloudWatch Logs to monitor, store, and access your log files from Amazon Elastic Compute Cloud (Amazon EC2) instances, AWS CloudTrail, Route 53, and other sources such as on-premises servers. CloudWatch Logs enables you to centralize the logs from all of your systems, applications, and AWS services that you use, in a single, highly scalable service. You can then easily view them, search them for specific error codes or patterns, filter them based on specific fields, or archive them securely for future analysis.                   
81. CloudWatch Event/EventBridge: a way for us to react to events happening within AWS, used to do scheduled CRON jobs or reactive job (send message when IAM user sign in), in the console we choose the service we would trigger the event (EC2 instance change) and target (send message to SNS topic)                
82. CloudTrail: enabled by default, provides governance, and audit for your AWS account. Get an history of events / API calls made within your AWS account (console, SDK, CLI, AWS services). You can use CloudTrail to log, monitor and retain account activity related to actions across your AWS infrastructure. CloudTrail provides an event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services.                           
-> CloudTrail Insights: detect unusual activity in your account: bursts of IAM actions etc, events are stored for 90 days in CloudTrail, if want more need log them to S3              
83. X-ray: do tracing and get visual analysis of your application, troubleshoot performance, understand dependencies in the architecture, review request behaviour etc. You can use AWS X-Ray to analyze and debug serverless and distributed applications such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors.                           
84. Service Health Dashboard: shows health of the services for all regions and all services, RSS feed you can subscribe to           
85. Personal Health Dashboard: provides alerts and remediation guidance when AWS is experiencing events that may inpact you or what you have deployted, personalised view into the performances and availability of the AWS services underlying your AWS resources, global service                 

## VPC & Networking   

86. VPC (Virtual Private Cloud): private network to deploy your resources (regional resrouces)                
-> public subnet: accessible from the internet, can have EC2 instances or Load Balancer                          
-> private subnet: not accessible from the internet, can place your database             
-> Route table: define access to internet and between subnet             
87. Internet Gateway: helps VPC instances connect to internet, used by instances in the public subnet         
88. NAT Gateway (AWS managed) or NAT Instances (self-managed): allow instance in the private subnet to access internet (patching etc) without exposing itself, this gateway is in the public subnet and instance in private subnet need to connect to it                  
89. NACL (Network Access Control List): first line of defense for EC2 instances, a firewall which controls traffic in and out subnet, attached to subnet level, rules only include IP address. NACL is stateless (return traffic must be explicitly allowed by rules) Security Groups (stateful, return traffic auto allowed) is 2nd line of defense, can include IP and other SGs.        
90. VPC Flow Logs: a log of all the I traffic going through your interfaces.                  
91. VPC Peering: connect two VPC, privately using AWS's netowrk, make them behavior as if they are in the same network. VPC Peering connection is NOT transitive.                  
92. VPC Endpoints: allow us to connect AWS services (usually all public services) privately instead of public internet network            
-> VPC Endpoint Gateway: S3 and DynomoDB           
-> VPC Endpoint Interface: the rest               
93. Site to Site VPN: connect on-premises data center to VPC over public internet, uses CGW (Customer Gateway) on premisis and VGW (Virtual Private Gateway) at AWS            
94. Direct Connect (DX): establish a phyical connection between on-premises data cent and AWS, private network, 1 month to establish.                       
95. Transit Gateway: VPC can be connected by peer connection, VPN/DX and can be complicated, Transit Gateway can have peering connectiong between thousand of VPC and on-premises with hub-and-spoke (star) connections                   

## Security & Compliance        

96. AWS Shield              
-> Standard: protect against DDoS attack for your website and applications, free and activated by default, layer3/4(TCP) attacks           
-> Advanced: 24/7 premius DDoS protection, EC2/ELB, CloudFront etc                  
97. AWS WAF (Web Application Firewall): fileter requests based on rules, layer 7 (HTTP), defined Web ACL (Access Control List): geo-matching, rate-based rules (to count occurrence in evvent)               
98. Pennetration Testing: can carry out on 8 services without prior approval. cannot do DNS zone walking/DDoS/Port flooding/protocal flooding/request flooding.               
99. Amazon KMS (Key Management Serivce): AWS managed the encryption keys for us (we manage who can access to these keys). AWS Key Management Service (KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications.                                
100. CloudHSM (Hardware Security Module): dedicated hardware provided by AWS. They provision this hardware but we managing key ourselves. AWS CloudHSM is a cloud-based Hardware Security Module (HSM) that enables you to easily generate and use your encryption keys on the AWS Cloud. With CloudHSM, you can manage your encryption keys using FIPS 140-2 Level 3 validated HSMs.              
101. Secrets Manager: meant for storing secrets, secrets to be managed in RDS. AWS Secrets Manager helps you protect secrets needed to access your applications, services, and IT resources. The service enables you to easily rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle. Users and applications retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hardcode sensitive information in plain text.                           
102. Artifact: a portal that provides customers with on-demand access to AWS compliance documentation            
-> Artifact Reports: allows you to download AWS security and compliance documents from 3rd party auditors            
-> Artifact Agreement: review, accept, and track status of AWS agreement like HIPPA, BAA etc                         
103. GuardDuty: use ML algorithm for threat discovery to protect AWS account, input from CloudTrail, VPC Flow Log, DNS log. Can setup CloudWatch Event rules for notification with Lambda or SNS             
104. Inspector: automated security assessment for EC2 instance, running OS against known vulnerability, against inintended network accessibility, must install Inspector Agent on OS in EC2 instances, you will get a report after accessment. Amazon Inspector is an automated, security assessment service that helps you check for unintended network accessibility of your Amazon EC2 instances and for vulnerabilities on those EC2 instances. Amazon Inspector assessments are offered to you as pre-defined rules packages mapped to common security best practices and vulnerability definitions.                                     
105. Config: auditing and recording compliance of your AWS account, record configurations and changes over time, can be stored in S3, can receive alert. AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. Config continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations.                                
106. Macie: use ML and pattern matching to identify and alert you to sensitive , such as personally identifiable information (PII) in your storage like S3.               
107. Security Hub: central security tool to manage security across several AWS account and automate security checks.                   
108. Amazon Detective: analyse, investigate, and quickly identify ROOT cause of security issue or suspecious using ML and graphs, auto collects and process events from VPC Flow Logs, GuardDuty and create a unified view.                    
109. Root user privileges:        
-> change account setting     
-> close AWS account            
-> change or cancel AWS support plan           
-> register as seller in the Reserved Instance Marketplace                 

## Machine Learning              

110. Rekognition: CV, find object, people, text in images and videos, facial search/analysis            
111. Trascribe: speech -> text, using automatic speech recognition (ASR)               
112. Polly: text -> speech, create application that talk              
113. Translate: natual and accurate language translation, allows you to localize content               
114. Lex + Connect: create call center/chatbot              
-> Lex: same tech that powers Alexa, ASR, NLP, can build chatbot           
-> Connect: virtual contact center, can receive calls, create contact flow etc.                 
115. Comprehend: NLP, fully managed and serverless service. extract info, sentiment analysis etc.                   
116. SageMaker: fully managed service for developer to build ML pipeline/model                 

## Account Management, Billing & Support                

117. Organization: manage multiple AWS account, API is available for aumoated AWS account creation          
-> SCP (Service Control Policies): restric account privileges, JSON format, applied at OU or Account level, enforce PCI compliance by explicitly disable services             
-> Master account in the organisation not affected by SCP                      
118. AWS Control Tower: easy way to setup and goven a secure and compliant multi-account AWS environment based on best practice, runs on top of Organisation (it auto setup Organisation for you in the process), can use SSO (Single-Sign On)               
119. Saving Plan:               
-> EC2 Saving Plan: commit to usage of individual instances families in a region (e.g. C5 or M5), up to 72% discount              
-> Compute Saving Plan: very flexible, regardless of Family, Regiom, size, OS, tenancy, compute options (EC2, Fargate, Lambda), up to 66% discount            
120. TCO (Total Cost Ownership) Calculator: estimate the cost saving when using AWS, compared to your applications on-premises, can be used for executive presentations              
121. Cost and Usage Reports: csv, most comprehensive set of AWS cost and usage data available, list each service category used by an account and its IAM users.                         
122. Cost Explorer: visualise, understand and manage AWS costs and usage over time, can be used to choose an optimal Savings Plan, and forecast usage up to 12 months based on previous usage. AWS Cost Explorer has an easy-to-use interface that lets you visualize, understand, and manage your AWS costs and usage over time. AWS Cost Explorer includes a default report that helps you visualize the costs and usage associated with your top five cost-accruing AWS services, and gives you a detailed breakdown of all services in the table view. The reports let you adjust the time range to view historical data going back up to twelve months to gain an understanding of your cost trends. The rightsizing recommendations feature in Cost Explorer helps you identify cost-saving opportunities by downsizing or terminating EC2 instances. You can see all of your underutilized EC2 instances across member accounts in a single view to immediately identify how much you can save.                               
123. Billing Alarm: billing data metric is stored in CloueWatch in us-east-1, just simple alarm                  
124. AWS Budget: create budget and send alarms when costs (including forecasted cost) exceeds budget. AWS Budgets gives the ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount. You can also use AWS Budgets to set reservation utilization or coverage targets and receive alerts when your utilization drops below the threshold you define.                                    
125. AWS Trusted Advisor: analyse your AWS accounts and provides recommendations (analyse 5 types of problems on your account). AWS Trusted Advisor is an online tool that provides you real-time guidance to help you provision your resources following AWS best practices on cost optimization, security, fault tolerance, service limits, and performance improvement. Whether establishing new workflows, developing applications, or as part of ongoing improvement, recommendations provided by Trusted Advisor regularly help keep your solutions provisioned optimally.                         
-> basic tier: Core Checks and recommendation (seems like only Security and Service Limits)                 
-> Full Trusted Advisor (Business & Enterprise Support Plans): programatic access using AWS Support API               
126. Support Plan for AWS:               
-> **Basic**: free, 24x7 access to customer service, documentation etc               
-> **Developer**: great for development, business hour email access to Cloud Supoort Associates               
--> general guidance: less than 24 business hr              
--> system impaird: less than 12 business hr               
-> **Business** (24/7): if you have production workloads            
--> 24x7 phone, email and chat access to Cloud Support Engineers               
--> Production system impaired: less than 4 hr            
--> Production system down: less than 1 hr                
-> **Enterprise** (24/7): if you have mission critical workload              
--> Business-critical system down: less than 15 minutes           
--> access to a dedicated TAM (Technical Account Manager)            
--> Concierge Support Team: The Concierge Support Team are AWS billing and account experts that specialize in working with enterprise accounts. They will quickly and efficiently assist you with your billing and account inquiries.                                 
--> Infrastructure Event Management, Well-Architected & Operations Reviews

## Advanced Identity                

127. Cognito: to provide identity for your web and mobile applications, this is to manager users on AWS               
128. Directory Services: used for Active Directory (Windows system) for log in to multiple machine                
129. SSO (Single-Sign On): centrally manage single-sign on to access multiple accounts and 3rd party business applications             


## Other Services             

130. WorkSpaces: managed Desktop as a Service (DaaS) to easily provision Windows or Linux Desktop                 
131. AppStream 2.0: deliever/use application within a web browser               
132. Sumerian: create and run VR, AR and 3D applications/model.              
133. IoT Core: easily connect IoT devices to AWS Cloud             
134. Elastic Transcoder: convert media files stored in S3 into media files in the formats required by consumer playback devices (phone, tablet, PC, etc)               


## AWS Architecting & Ecosystem               

135. 5 Pillar for Well Architected Framework:          
-> Operational Excellence            
-> Security               
-> Reliability               
-> Performance Efficiency                  
-> Cost Optimization               

136. AWS Professional Service: a global team of experts                
137. APN (AWS Partner Network): a group of people good with cloud:                
-> APN Technology Partner: providing hardware, connectivity, and software (focus on infra). APN Technology Partners provide hardware, connectivity services, or software solutions that are either hosted on or integrated with, the AWS Cloud.                          
-> APN Consulting Partner: professional services firm to help build on AWS. APN Consulting Partners are professional services firms that help customers of all types and sizes design, architect, build, migrate, and manage their workloads and applications on AWS, accelerating their migration to AWS cloud.                                 
-> APN Training Partner: find who can help you learn AWS            
138. AWS Competency Program: grant competencies to APN parneter who have demonstrated technical proficienty and proven customer success in specialsied solution areas            
139. AWS Navigation Prgram: help Partner become better Partner

## Exam tips:         

140. You may see use-cases asking you to select one of CloudWatch vs CloudTrail vs Config. Just remember this thumb rule:             
Think resource performance monitoring, events, and alerts; think CloudWatch.                   
Think account-specific activity and audit; think CloudTrail.                         
Think resource-specific change history, audit, and compliance; think Config.                
          
141. For RDS, need to know:           
-> Multi-AZ deployment: for high availability, sync replication (non-Aurora), asyc replication (Aurora)            
-> Multi-Region deployment: disaster recovery and boost local performance, asyn replication                              
-> Read-replica: for scalability, async replication             

142. AWS Acceptable Use Policy: The Acceptable Use Policy describes prohibited uses of the web services offered by Amazon Web Services
