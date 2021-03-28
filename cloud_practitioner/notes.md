# AWS Certified Cloud Practitioner Course Notes (CLF-C01)

This note summarised the preparation course by Stephane Maarek on Udemy.

# What is Cloud Computing ?

## Traditional IT Overview 

<img src="images/web_site.png" width="700">

An simple example to demonstrate how website works is that we as the Client (using web browser) want to get access to the Server to visualise a website, through a network. The data packet gets routed though the network to the Server and the Server will get back to us, so that we can view the website. Both the Client and the Server has IP address which can be used to send/receive requests. 

So what is in the Server ?     
CPU: computation and finding results.        
RAM: fast memory (storing and retrieving quickly)       
Storage: long term storage of data              
Database: for large structured data      
Network tools: routers, switch, DNS server, etc.       

So what is in the network ?       
Cables: obviously       
Router: networking device that forwards data packets between computer networks        
Switch: when the data packet arrives at the destination, the switch will send the packet to the correct Server/Client on the network.     

So in summary it looks like this: Clients send data to a router, the router will find all its way to the switch through network, and the switch will send the packet to the specific Client/Server in the network.

<img src="images/router_switch.png" width="700">

Traditionally,the infrastructure of building a company or website (e.g. Google) involving buy a lot of server (stored in Data Centre) to satisfy the demand (request) to your website. But there are a few problems with this approach:     

1) pay for the rent for Data Centre     
2) pay for power supply, cooling, maintenance       
3) add and replace hardware takes time      
4) scaling is limited      
5) need a 24/7 team to monitor the infrastructure      
6) natural disaster mitigations        

Let's move to cloud computing !

## What is Cloud Computing ?     

Cloud computing is the **on-demand delivery** of compute power, database storage, applications, and other IT resources. Through a cloud services platform we will **pay as we go pricing**. We can **provision exactly the right tye and size** of computing resource we need and we can get these resources **almost instantly**.     

There are different types of cloud services:       

1) Private Cloud: used by a single organisation, not exposed to the public. Having complete control and security for sensitive applications.                     
2) Public Cloud: Cloud resources owned and operated by a 3rd party cloud service provider (e.g. AWS) deliverd over the internet.         
3) Hybrid Cloud: keep some servers on premises and extend some capabilities to the Cloud. Have control over sensitive assets in our private infrastruture and having flexibility and cost-effectiveness of the public cloud.     

Five characteristics of Cloud Computing:       
1) Fully on-demand self service: use resources without human interaction from the service provider.      
2) Broad network access: resources available over the network, and can be accessed by diverse client platforms.     
3) Multi-tenancy and resource pooling: multiple customers can share the same infrastructure and applications with security and privacy. They are serviced from the same physical resources.             
4) Rapid elasticity and scalability: quickly acqure and discard resources.      
5) Measured service.          

Six advantages of Clould Computing:      
1) Trade capital expense (CAPEX) for operational expense (OPEX): pay-on-demand means no need to own hardware. Reduce Total Cost of Ownership (TCO) and OPEX.           
2) Massive economies of scale: many people are using the service, so the price is low due to AWS is more efficient when the scale is large.       
3) Stop guessing capacity: scale based on actual usage.     
4) Increase speed and agility.      
5) Stop spending money running and maintaining data centers.
6) Go global in minutes: leverage the AWS global infrastructure.         

Problem solved by the Cloud:      
1) Flexibility: change resource types when needed.      
2) Cost-Effectiveness: pay as you go      
3) Scalability: accomodate larger loads                 
4) Elasticity: scale out and scale in when needed       
5) High-availability and fault-tolerance        
6) Agility: rapidly develop, test and launch software applications   

## The Different Types of Cloud Computing     

1) Infrastructure as a Service (IaaS)       
Provide building blocks for cloud IT      
Provide networking, computers, data storage space in its raw form      
Highest level of flexibility     
Easy parallel with traditional on-premises IT      
e.g. EC2     

2) Platform as a Service (PaaS)          
Don't need to mamage infrastructure           
Just focus on the deployment and management of our applications           

3) Software as a Service (SaaS)       
Completed product that is run and managed by the service provider.      

A simple visualisation that shows how each service need to managed each components:    

<img src="images/diff_service.png" width="700">

Some examples:     
1) IaaS: AWS EC2, GCP, Azure      
2) PaaS: AWS Beanstalk, Heroku             
3) SaaS: AWS Rekognition for ML, Gmail, Dropbox, Zoom     

AWS Pricing of the Cloud has 3 pricing fundamentals:      
1) **Compute: Pay for compute time**     
2) **Storage: Pay for data stored in the Cloud**      
3) **Networking: Pay for data transfer OUT of the Cloud**, i.e. any data goes into the Cloud is free.       

## AWS Cloud Overview

AWS Global Infrastructure:     
1) AWS Regions      

**Regions** (orange dot in the AWS map) include locations like Singapore Beijing Sydney etc, and they are all around the world. These regions are connected through the networks. Regions can have names like us-east-1, eu-west-3, etc. A Region is a cluster of data centers. 

**Most AWS services are region-scoped**, this means that if we use one service at Region A and attempt to use the same service in Region B, it will be like a new time using the service.         

How to choose which AWS Region ?        
**Compliance** with data governance and legal requirements: data never leaves a region without explicit permission. So if the government requires data stay in the country, we should launch our application within that country.       
**Proximity** to customers: reduced latency.       
**Available services within a Region**: new services and new features might not be available in every Region.     
**Pricing**: pricing varies region to region and is transparent in the serice pricing page.       

2) AWS Availability Zones       

Each Region has many Availability Zones. (usually 3, min is 2, max is 6, they are blue dots in the AWS map).     
e.g. AWS Region: Sydney: ap-southeast-2         
we will have 3 Availability Zones: ap-southeast-2a, ap-southeast-2b, ap-southeast-2c.       

Each Availability Zones is one or more discrete data centers with redundant power, networking and connectivity. They are separated from each other so they are isolated from disasters. These Availability Zones are connected with high bandwidth, ultra-low latency networking. They are thus linked together to form the Region.          

3) AWS Data Centers         

4) AWS Edge Locations/ Points of Presence           

Amazon has 216 Points of Presence (205 Edge Locations and 11 Regional Caches) in 84 cities across 42 countries. It is helpful to deliver content to end users with lower latency.       
  
AWS has Global Services:      
Identity and Access Management (IAM)        
Route 53 (DNS service)       
CloudFront (Content Delivery Network)      
WAF (Web Application Firewall)          

**Most** AWS services are Region-scoped:       
Amazon EC2 (IaaS)     
Elastic Beanstalk (PaaS)      
Lambda (Function as a Serice)     
Rekognition (SaaS)

We can check out the AWS Region Table to see if a service is available in our Region. Or we can go to AWS Global Infrastructure (just google it) and see AWS Regional Services then we can access which services are available in which Regions. If the Region we are at does not have certain services we can switch to another Region.    

## Shared Responsibility Model & AWS Acceptable Policy    

Customer: Responsible for the security **IN** in the Cloud. This includes security, our data, our OS, our network and firewall configuration.     

AWS: Responsible for the security **OF** the Cloud. In the CCP exam, there *will* be questions about the shared responsibility. 

<img src="images/aws_share_responsibility.png" width="700">

AWS Acceptable Use Policy      
No illgal, harmful or offensive use or content       
No security violation     
No network abuse     
No E-mail or other message abuse

# IAM - Identity and Access Management

This is a **Global** service. This is because in IAM we are going to create our users and assign them to group.    

**Root account** created by default when we create AWS account, this shouldn't be used or shared. This account is only used to setup other account.      

We should create **Users**, they are people within your organisation.     

Group can only contain users, not other groups. Some users don't have to belong to a group and some users can be in multiple groups.        

The reasons for users/groups is to give them various permissions. **Users** and **Groups** can be assigned JSON documents called *policies*.   

An example:     
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "ec2:Describe*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": "elasticcloadbalancing:Describe*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "cloudwatch:ListMetrics",
                "cloudwatch:GetMetricsStatistics",
                "cloudwatch:Describe*"
            ],
            "Resource": "*"
        }
    ]
}
```

Another example for the policy: AdminstratorAccess: (Note the star means everything)             

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}
```

Through these policies we define the permissions of the users. In AWS, we apply **least privilege principle**: don't give more permissions than a user needs.      

For users, we can add tags, where we can mark the users and add in some attributes.   

After log in we can notice that if the user accout is something like `stephane@stephane-ccp`, this means that this account is logged in as IAM user. If the user account is just `stephane-ccp` then this is logged in with root user.      

To grant permissions to User, we can either add the user into a group (which has the group policy, so this user will inhereit this group policy) or assign a policy directly to the user. We can also create our own custom policy either use the GUI or write in JSON.      

## IAM MFA Overview

To protect the AWS account, we have 2 defense mechanisms:      

1) IAM Password Policy (helpful against brute force attack)         

Set minimum password length      
Requires specific character types: upper/lower case letters, numbers or non-alphanumeric characters.       
Allow all IAM users to change their own passwords      
Require users to change their password after some time       
Prevent password reuse                 

2) Multi Factor Authentication - MFA        

On AWS this is a must and very recommended to use it. **We want to protect Root Account and IAM users**.      
MFA = password you know + security device you own         

MFA devices options in AWS:         
1) Virtual MFA device:       
Google Authenticator: phone only   
Authy: multi-device, and supports multiple tokens on a single device.       

2) Universal 2nd Factor (U2F) Security Key:      
YubiKey by Yubico (3rd party): support for multiple root and IAM users using a single security key                

3.1) Hardware Key Fob MFA Device:    
Gemalto (3rd party)      

3.2) Hardware Key Fob MFA Device for AWS GovCloud (US):           
SurePassID (3rd party)        

## AWS CLI    

How can users access AWS ? There are 3 options:    
1) AWS Management Console (protected by password + MFA, for Root Account or other users)       
2) AWS Command Line Interface (CLI): protected by access keys      
3) AWS Software Developer Kit (SDK): this is mainly for code, also protected by access keys    

Access keys are generated through the AWS Console. Users manage their own access keys and these keys are **private**.    
Access key have 2 components: Access Key ID (username) and Secret Access Key (password).   

We have to install (OS specific) client and configure the CLI with the Access Key ID and the Secret Access Key in order to use command line to access AWS.    

## AWS CloudShell

There is an alternative to install the CLI and configure it, this is called CloudShell. At the top right corner of the AWS Console there is a `terminal` icon we can launch. This is basically CLI in the cloud with pre-installed tools, storage (1 GB per AWS region) and saved files/settings.     

We can directly run AWS command directly in the CloudShell instead on the local CLI. e.g. `aws --version` to check the version of the AWS CLI installed or `aws iam list-users` to list the IAM users.     

The credentials used by the CloudShell is the same credentials as the user we logged in to the console with, at the moment we launch the CloudShell.    

## IAM Roles for AWS Services

Some AWS services will need to perform actions on our behalf and on our account. We have to assign permissions to AWS services with IAM Roles.    

IAM Roles are just like users, but they are intended to be used *not* by physical people, but instead used by AWS Services.    

A quick example will be we created an EC2 instance (virtual server), and this EC2 instance would like to perform some action on AWS. To do so we need to give permissions to this EC2 instance. We will create an IAM Roles and together with the EC2 instance (as one entity), they can access AWS.     

Some common roles includes: EC2 Instance Roles, Lambda Function Roles, Roles for CloudFormation.      

## IAM Security Tools    

IAM Credentials Report (account level):      
We can create this report at the account level. This is a report that lists all your account's users and the status of their various credentials.    

IAM Access Advisor (user level):            
Access advisor shows the service permissions granted to a user and when those services were last used. We can use this information to revise your policies based on principle of least privilege.    

## IAM Best Practices

Do not use the Root Account except for AWS account setup      
One physical user = One AWS user       
**Assign users to groups** and assign permissions to groups (such that we manage permissions at a group level)           
Create a strong password policy       
Use and enforce the use of MFA              
Create and use Roles for giving permissions to AWS services           
Use Access Keys for Programmatic Access (CLI/SDK)      
Audit permissions of your account with the IAM Credential Reports     
Never share IAM users and Access keys     

## Shared Responsibility Model for IAM

AWS is responsible for everything they do include:      
Infrastructure (global network security)           
Configuration and vulnerability analysis            
Compliance validation          

For IAM, we are responsible for:     
User, Groups, Roles, Policies management and monitoring         
Enable MFA on all accounts          
Keys are rotated often           
Use IAM tools to apply appropriate permissions     
Analyse access patterns and review permissions          

In short, AWS is responsible for the infrastructure and we are responsible of how we use the infrastructure.           

## IAM Summary

Users: mapped to a physical user, has password for AWS Console         
Groups: contains users only (it is best to group users together)     
Policies: JSON document that outlines permissions for users or groups        
Roles: if we are within AWS, we can use roles to give permissions to AWS services to perform tasks      
Security: MFA + password policy        
Access Keys: access AWS using the CLI or SDK      
Audit: IAM Credential Reports and IAM Access Advisor          

# EC2 - Elastic Compute Cloud

*Before we start our journey in AWS services like EC2, we should set up AWS Cost budget just in case*.       

## EC2 Basics

One of the most popular AWS service and it is a Infrastructure as a Service (IaaS).       

It is comprised of many things (and capabilities) at a high level:       
-> You can rent virtual machinese on EC2 (they are called EC2 instances)     
-> You can store data in on their virual drives (they are called EBS volumes)     
-> You can distribute load across machines (Elastic Load Balancer, ELB)         
-> You can scale services using auto-scaling group (ASG)         

Knowing how EC2 works is *fundamental* to understand how Cloud works.      

EC2 sizing & configuration option: what can we choose for our instances (virtual servers) ?     

-> Operating System (OS): Linux or Windows (*NO* Mac)       
-> How much compute power & cores (CPU)       
-> How much random-access memory (RAM)            
-> How much storage space: Network-attached (EBS & EFS) or hardware-attached (EC2 Instance Store)           
-> The Network card that is attached to the EC2 instance: speed of the card, public IP address        
-> Firewall rules: **security group**              
-> Bootstrap script (configure at first launch): Configuration script needs to be run at first launch, this is called EC2 User Data           

The `t2.micro` instance is included in the AWS free-tier. It has 1 vCPU, 1 GiB Mem and EBS storage.      

## Create an EC2 Instance with EC2 User Data to have a Website (hands-on)

1. Log in AWS Console, search for EC2, go to EC2 Console    
2. Choose region (e.g. closest to you)
3. Go to `Instances` on the right panel and `Launch Instance`
4. Choose Amazon Machine Image (AMI), we can choose from Quick Start and select Amazon Linux 2 AMI (64-bit x86) which is free-tier eligible.  
5. Choose an Instance Type (e.g. t2.micro for free tier)
6. Configure Instance Details: Under `User Data` we can run a user data which is only run at the first boot of the instance. (an example script is given, which is going to launch a web server onto our EC2 instance and write a file to it)
7. Add Storage (check `Delete on Termination`)
8. Add tags
9. Configure Security Group: create a new security group and Add Rule (HTTP, port 80)
10. Review and launch (will be prompted to use a key pair (for SSH)) 
11. Create a new key-pair (public-private key) and download the key pair

We can then use the public IPv4 address to access the website. To stop the instance, we can right click the instance and `Stop Instance`. To get rid of the instance, choose `Terminate Instance`.       

Note that if we stop an instance and restart it again, the public IPv4 **is going to change**.   

## EC2 Instance Types Basics

AWS has the following naming convention (example):     
m5.2Xlarge    
m: instance class, in this case a general purpose instance      
5: generation of the instance (AWS improves them over time)         
2xlarge: size within the instance class         

**For exam we need to know this**, for various EC2 Instance Types:              
1. General Purpose        
Great for a diversity of workloads such as web servers or code repositories              
Balance between: Compute, Memory and Networking     
t2.micro is a General Purpose EC2 Instance (free tier)             

2. Compute Optimized        
Great for compute-intensive tasks that require high performance processors:      
Batch processing workloads       
Media transcoding      
High performance web server              
High performance computing (HPC)            
Scientific modeling and machine learning            
Dedicated gaming servers               
Currently all the Compute Optimized EC2 Instance start with `c`, e.g. c5 or c6.     

3. Memory Optimized
Fast performance for workloads that process large data sets in memory (RAM)       
Use cases includes:         
Floating point number calculations         
Graphic processing                
Data pattern matching        
These instances starts with `r`.             

4. Storage Optimized
Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage     
Use cases include:        
High frequency online transaction processing (OLTP) systems    
Relational & NoSQL databases            
Cache for in-memory databases (e.g. Redis)       
Data warehousing applications                 
Distributed file systems           
These instance starts with `i`, `d` or `h1`.       

## Security Groups & Classic Ports Overview

Security Groups are the fundamental of network security in AWS.             
They control how traffic is allowed into or out of our EC2 Instances.    
Security Groups only contains *allow* rules, i.e. what is allowed to go in or go out.    
Security Groups rules can reference by IP address (i.e. where is your computer) or by Security Groups (i.e. Security Groups can reference each other).                

For example we are on our computer (i.e. public internet) and we would like to access our EC2 Instance. We will have to create a Security Group around our EC2 Instance (that is the firewall around it) and this Security Group is going to have rules that control which inbound traffic is allowed into the EC2 Instance and if the EC2 Instance can perform some Outbound traffic.      

Security Groups are acting as a "firewall" on EC2 Instance. They regulate:          
1. Access to Ports
2. Authorised IP ranges: IPv4 and IPv6 (e.g. 0.0.0.0/0 means any IP address is authorised)
3. Control of inbound network (i.e. from others to the EC2 Instance)
4. Control of outbound network (i.e. from EC2 Instance to others)

A quick example of Security Group works is shown below:           
<img src="images/security_firewall.png" width="700">     

For unauthorised inbound traffic, it will be a timeout error. By default for any Security Group, it will allow all outbound traffic out of the EC2 Instance. For example, if our EC2 Instance try to access a website, the Security Group is going to allow it.     

Classic Port we need to know (**EXAM**):        
1. 22 = SSH (Secure Shell) - log into a EC2 Instance on Linux
2. 21 = FTP (File Transport Protocol) - upload files into a file share
3. 22 = SFTP (Secure File Transport Protocol) - upload files using SSH
4. 80 = HTTP - access unsecured websites
5. 443 = HTTPS  - access secured websites
6. 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance

The Security Groups (i.e. firewall) can be attached to multiple EC2 Instances.     

## SSH Overview

<img src="images/ssh_summary.png" width="700">

## SSH with Mac

When creating the EC2 Instance, we have created a key pair and download it (e.g. `ec2tutorial.pem`). We will need this key pair to SSH into this instance.      
```
ssh -i ec2tutorial.pem ec2-user@35.180.100.144
```
`ec2-user` is basically the Linux user in Amazon Linux machine. `35.180.100.144` is the IPv4 Public IP of the EC2 Instance.      

The above command will **fail**. This is because the first time we download the file, the permission is 0644 for the file. And this is too open for the private key, this means that the private key can leak, and it is accessable by others and it is a bad permission. The remedy is to change the file permission via:      
```
chmod 0400 ec2tutorial.pem
```
Run the SSH command again and we will be able to SSH into the EC2 instance. Once we are inside we can query the user (`whoami`) or ping a website (`ping google.com`)          

Note that in Windows 10 the `chmod` command does not exist. We will have to go to the property of the `.pem` file. We cab go to the Security tab and disable inherentence then remove all other user except yourself.        

To exit we can just press `exit` or `ctrl + d` to close the connection. (or `ctrl + c` or type `exit`)      

Note that on Windows when we use PuTTY, we need the PuTTygen to convert the key pair, which is in `.pem` to `.ppk` format so that PuTTY can use. Then after launching PuTTY and put in the public IPv4 of the EC2 Instance, we need to go to Connection -> SSH -> Auth to link the `.ppk` file.            

## EC2 Instance Connect

There is another way to connect to an EC2 Instance directly from AWS. We can click Connect in the AWS EC2 dashboard (where the list of EC2 Instance is shown). We can connect via EC2 Instance Connect after use a username. Note that this methods do not work with all type of AMIs in AWS. At the backend, it upload a temporary SSH key on your EC2 Instance for you. This methods ultimately still rely on SSH, so if we remove SSH rules from the Security Groups setting we will meet a timeout error if we use EC2 Instance Connect. So even though this method is based on browser, port 22 still needs to be opened for this method








# TO DO         

    