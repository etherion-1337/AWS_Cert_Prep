# AWS Certified Solutions Architect Associate                 

# Getting Started with AWS           

## AWS Cloud Overview - Region & AZ                

**AWS Regions**                  
AWS has **Regions** all around the world. Region has a name: us-east-1, eu-west-3, etc.                 
A region is a cluster of data centers.                  
Most AWS services are region-scoped                       

How to choose an AWS Region ?              
1. **Compliance** with data  governance and legal requirements: data never leaves a region without your explicit permission                 
2. **Proximity** to customers: reduced latency                       
3. **Available services** within a Region: not all regions have all services, new services and new features are not available in every region                       
4. **Pricing**: pricing varies region to region and is transparent in the service pricing page                    

For region-scoped services (e.g. EC2), when we switch region in AWS console, we will have a completely new different sets of resources.           

Resources are scoped to the Region for most services in AWS.                 

**AWS Availability Zones**                 
Each region has many availability zones, usually 3, min is 2, max is 6. e.g.             
Region: ap-southeast-2 has 3 AZ:             
ap-southeast-2a                
ap-southeast-2b                 
ap-southeast-2c                   

Each AZ is one or more discrete data centers with redundant power, networking and connectivity                 
They are separate from each other, so that they are isolated from disaters                  
They are connected with high bandwidth, ultra-low latency networking                        
They are linked together and form a region                 

**AWS Points of Presence (Edge Locations)**                             
Amazon has 216 Points of Presence (205 Edge Locations & 11 Regional Caches) in 84 cities across 42 countries.               
Content is delivered to end users with lower latency                

From Global Infrastrucutre, we can see which services are available within region.               

# IAM & AWS CLI           

## IAM Introduction: Users, Groups, Policies                         

**Global** services                    

IAM = Identity and Access Management        

When we create an account, we created a **root** account by default. This should NOT be used or shared.                            

We should create IAM **Users**. **Users** are people within your organisation, and can be grouped.                       

Groups can only contain Users, not other groups.                   
Users don't have to belong to a group, and user can belong to multiple groups.          

<img src="images/aws_group.png" width="700">          

Users or Groups can be assigned JSON documents called policies.                
These policies define the permissions of the user.                 

In AWS you apply the **least privilege principle**: DO NOT give more permissions than a user needs.                                 

This is an example of IAM policy:                       
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
For users, we can add tags, where we can mark the users and add in some attributes.                    

After log in we can notice that if the user accout is something like `stephane@stephane-ccp`, this means that this account is logged in as IAM user. The part after `@` is the account alias (e.g. can be `stephane-aws` for the account `stephane-ccp`, or the account name itself). If the user account is just `stephane-ccp` then this is logged in with root user (`stephane-ccp` is the account name).      

To grant permissions to User, we can either add the user into a group (which has the group policy, so this user will inhereit this group policy) or assign a policy directly to the user (in some cases, this is also called an inline policy). We can also create our own custom policy either use the GUI or write in JSON.          

By clicing on the policy, we can also view what are the services that we have (full) access to.              

<img src="images/iam_policy_structure.png" width="700">                


## IAM MFA Overview

To protect the AWS account, we have 2 defense mechanisms:      

1) IAM Password Policy (helpful against brute force attack)         

-> Set minimum password length      
-> Requires specific character types: upper/lower case letters, numbers or non-alphanumeric characters.       
-> Allow all IAM users to change their own passwords       
-> Require users to change their password after some time                   
-> Prevent password reuse                 

2) Multi Factor Authentication - MFA        

On AWS this is a must and very recommended to use it. **We want to protect Root Account and IAM users**.      
MFA = password you know + security device you own         

MFA devices options in AWS:         
1) Virtual MFA device:       
Google Authenticator: phone only      
Authy: multi-device, and supports multiple tokens on a single device.       

2) Universal 2nd Factor (U2F) Security Key:      
YubiKey by Yubico (3rd party): support for multiple root and IAM users using a single security key, act as an USB-based key                

3) Hardware Key Fob MFA Device:    
Gemalto (3rd party)       

4) Hardware Key Fob MFA Device for AWS GovCloud (US):           
SurePassID (3rd party)             

## AWS CLI             

How can users access AWS ? There are 3 options:    
1) AWS Management Console (protected by password + MFA, for Root Account or other users)       
2) AWS Command Line Interface (CLI): protected by access keys      
3) AWS Software Developer Kit (SDK): this is mainly for code, (when your code is trying to access AWS), also protected by access keys    

Access keys are generated through the AWS Console. Users manage their own access keys and these keys are **private**.    
Access key have 2 components:            
Access Key ID (username) and Secret Access Key (password).         

We have to install (OS specific) client and configure the CLI with the Access Key ID and the Secret Access Key in order to use command line to access AWS.         

AWS Software Development Kit (SDK):              
-> Language-specific APIs (set of libraries)             
-> Enables you to access and manage AWS services programmatically             
-> Embedded within your application (not launced from terminal)            
-> e.g. AWS CLI is built-on AWS SDK for Python               

## AWS CloudShell

There is an alternative to install the CLI and configure it, this is called CloudShell. At the top right corner of the AWS Console there is a `terminal` icon we can launch. This is basically CLI in the cloud with pre-installed tools, storage (1 GB per AWS region) and saved files/settings.       

We can directly run AWS command directly in the CloudShell instead on the local CLI. e.g. `aws --version` to check the version of the AWS CLI installed or `aws iam list-users` to list the IAM users.        

The credentials used by the CloudShell is the same credentials as the user we logged in to the console with, at the moment we launch the CloudShell.             

## IAM Roles for AWS Service           

Some AWS services will need to perform actions on our behalf and on our account. We have to assign permissions to AWS services with IAM Roles.           

IAM Roles are just like users, but they are intended to be used *not* by physical people, but instead used by AWS Services.           

<img src="images/iam_role.png" width="400">             

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
Audit permissions of your account with the IAM Credential Reports (also IAM Access Advisor)    
Never share IAM users and Access keys        

## IAM Summary

Users: mapped to a physical user, has password for AWS Console         
Groups: contains users only (it is best to group users together)     
Policies: JSON document that outlines permissions for users or groups        
Roles: if we are within AWS, we can use roles to give permissions to AWS services to perform tasks      
Security: MFA + password policy        
Access Keys: access AWS using the CLI or SDK        
Audit: IAM Credential Reports and IAM Access Advisor          

# EC2 Fundamentals                

## EC2 Basics

One of the most popular AWS service and it is a Infrastructure as a Service (IaaS).            

EC2 = Elastic Compute Cloud             

It is comprised of many things (and capabilities) at a high level:            
-> You can rent virtual machinese on EC2 (they are called EC2 instances)          
-> You can store data in on their virual drives (they are called EBS volumes)              
-> You can distribute load across machines (Elastic Load Balancer, ELB)          
-> You can scale services using auto-scaling group (ASG)           

Knowing how EC2 works is *fundamental* to understand how Cloud works.      

EC2 sizing & configuration option: what can we choose for our instances (virtual servers) ?     

-> Operating System (OS): Linux or Windows or Mac        
-> How much compute power & cores (CPU)       
-> How much random-access memory (RAM)            
-> How much storage space: Network-attached (EBS & EFS) or hardware-attached (EC2 Instance Store)           
-> The Network card that is attached to the EC2 instance: speed of the card, public IP address        
-> Firewall rules: **security group**              
-> Bootstrap script (configure at first launch): Configuration script needs to be run at first launch, this is called EC2 User Data           

The `t2.micro` instance is included in the AWS free-tier. It has 1 vCPU, 1 GiB Mem and EBS storage.         

**EC2 User Data**            
It is possible to bootstrap our instances using an EC2 User Data scirpt.              
*Bootstrapping* means launching commands when a machine starts             
That script is *only run once* at the instance first start                
EC2 user data is used to automate boot tasks such as:            
-> installing updates           
-> installing software         
-> downloading common files from the internet           
The EC2 User Data Script runs with the root user (any command you have will have the pseudo rights)             

## Create an EC2 Instance with EC2 User Data to have a Website (hands-on)

1. Log in AWS Console, search for EC2, go to EC2 Console    
2. Choose region (e.g. closest to you)
3. Go to `Instances` on the right panel and `Launch Instance`
4. Choose Amazon Machine Image (AMI), we can choose from Quick Start and select Amazon Linux 2 AMI (64-bit x86) which is free-tier eligible.          
5. Choose an Instance Type (e.g. t2.micro for free tier), note that we are launching the instances in a default VPC (if we don't change the settings)          
6. Configure Instance Details: Under `User Data` we can run a user data which is only run at the first boot of the instance. (an example script is given, which is going to launch a web server onto our EC2 instance and write a file to it)
7. Add Storage (check `Delete on Termination`)
8. Add tags
9. Configure Security Group: create a new security group and Add Rule (HTTP, port 80)
10. Review and launch (will be prompted to use a key pair (for SSH)) 
11. Create a new key-pair (public-private key) and download the key pair

We can then use the public IPv4 address to access the website. To stop the instance, we can right click the instance and `Stop Instance`. To get rid of the instance, choose `Terminate Instance`.       

Note that if we stop an instance and restart it again, the public IPv4 **is going to change**. The private IPv4 will not change.        

## EC2 Instance Types Basics

AWS has the following naming convention (example):          
m5.2Xlarge         
m: **instance class**, in this case a general purpose instance         
5: **generation** of the instance (AWS improves them over time)         
2xlarge: **size** within the instance class (more memory, more CPU etc)         

**For exam we need to know this**, for various EC2 Instance Types:              
1. General Purpose        
Great for a diversity of workloads such as web servers or code repositories              
Balance between:        
-> Compute           
-> Memory              
-> Networking                  
t2.micro is a General Purpose EC2 Instance (free tier)             

2. Compute Optimized        
Great for compute-intensive tasks that require high performance processors:      
-> Batch processing workloads       
-> Media transcoding      
-> High performance web server              
-> High performance computing (HPC)            
-> Scientific modeling and machine learning            
-> Dedicated gaming servers               
Currently all the Compute Optimized EC2 Instance start with `c`, e.g. c5 or c6.     

3. Memory Optimized                
Fast performance for workloads that process large data sets in memory (RAM)       
Use cases includes:         
-> High performance, relational/non-relational databases        
-> Distributed web scale cache stores                
-> In-memory databases optimzed for BI           
-> Applications performing real-time processing of big unstructured data                   
These instances starts with `r`.             

4. Storage Optimized                      
Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage     
Use cases include:        
-> High frequency online transaction processing (OLTP) systems    
-> Relational & NoSQL databases            
-> Cache for in-memory databases (e.g. Redis)       
-> Data warehousing applications                 
-> Distributed file systems           
These instance starts with `i`, `d` or `h1`.        

## Security Groups & Classic Ports Overview

Security Groups are the fundamental of network security in AWS.             
They control how traffic is allowed into or out of our EC2 Instances.    
Security Groups only contains *allow* rules, i.e. what is allowed to go in or go out.    
Security Groups rules can reference by IP address (i.e. where is your computer) or by Security Groups (i.e. Security Groups can reference each other).                

<img src="images/ec2_sg_simple.png" width="700">              

For example we are on our computer (i.e. public internet) and we would like to access our EC2 Instance. We will have to create a Security Group around our EC2 Instance (that is the firewall around it) and this Security Group is going to have rules that control which inbound traffic is allowed into the EC2 Instance and if the EC2 Instance can perform some Outbound traffic.      

Security Groups are acting as a "firewall" on EC2 Instance. They regulate:          
1. Access to Ports
2. Authorised IP ranges: IPv4 and IPv6 (e.g. 0.0.0.0/0 means any IP address is authorised)
3. Control of inbound network (i.e. from others to the EC2 Instance)
4. Control of outbound network (i.e. from EC2 Instance to others)

A quick example of Security Group works is shown below:           
<img src="images/security_firewall.png" width="700">     

For unauthorised inbound traffic, it will be a timeout error. By default for any Security Group, it will allow all outbound traffic out of the EC2 Instance. For example, if our EC2 Instance try to access a website, the Security Group is going to allow it.         

Security Groups good-to-know:            
-> can be attached to multiple instances          
-> instances can have multiple security groups              
-> Locked down to region/VPC combination           
-> Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it (i.e. not like an application that runs on EC2)            
-> It is good to maintain one sepearate security group for SSH access                  
-> If your application is not accessible (time out), then it is a security group issue               
-> If your application gives a "connection refused" error, then it is an application error or it is not launched.           
-> By default, all inbound traffic is **blocked**           
-> By default, all outbound traffic is **authorised**                     

Referencing other security groups:                 
<img src="images/ec2_sg_refer.png" width="700">            

In the inbound rule for the EC2 instance, it is authorising Security Group 1 inbound AND Security Group 2. When another EC2 instance has Security Group 2, it can connect straight through on the port of the first EC2 instance. So regardless of the IP address, because they have the right Security Group attached to them, they are able to communicate straight through to other instances.                 

Classic Port we need to know (**EXAM**):        
1. 22 = SSH (Secure Shell) - log into a EC2 Instance on Linux
2. 21 = FTP (File Transport Protocol) - upload files into a file share
3. 22 = SFTP (Secure File Transport Protocol) - upload files using SSH
4. 80 = HTTP - access unsecured websites
5. 443 = HTTPS  - access secured websites
6. 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance

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

## EC2 Instance Role Demo

After we connect to our EC2 Instance (via EC2 Connect) with our user, if we perform something like `aws iam list-users`, the CLI will prompt us to configure AWS to get our credentials. We can use `aws configure` to enter AWS Access Key ID and Secret Access Key but it is very bad practice. We can attach a Role to this instance (for example a Role with `IAMReadOnlyAccess` could allow us to run `aws iam list-users` without inputing credential again)                

## EC2 Instance Launch Types

EC2 Instances purchasing options:         
1. On-Demand Instances: short workload, predictabel pricing     
Sometimes we will need to use the serve for a long time and we can get some cost saving through:        
2. Reserved(**minimum 1 year**): 3 types       
-> Reserved Instances: long workload (e.g. database)       
-> Convertible Reserved Instances: long workload with flexible instances       
-> Scheduled Reserved Instances: example, every Thurs 3-6 pm     
3. Spot Instances: short workloads, cheap, can lose instances (less reliable)      
4. Dedicated Host: book an entire physical server, control instance placement        

Exam will ask you question and expect us to find the best of EC2 for various situations for cost saving or comply with some rules.    

**EC2 On Demand**:      
We pay for what we use:       
-> Linux machine: billing per second, after the first minute         
-> All other OS: billing per hour when instance is running      
Has the *highest* cost but no upfront payment      
No long-term commitment        

Recommended for **short-term** and **un-interrupted workloads**, where you cannot predict how the application will behave.      

**EC2 Reserved Instances**:       
Up to 75% discount compared to On-Demand.        
Reservation period: 1 year = + discount | 3 years = +++ discount (ONLY 1 or 3 years, not any time in between)       
Purchasing options: no upfront | partial upfront = + discount | All upfront = ++ discount        
Reserve a specific instance type (t2.micro etc)      

Recommended for steady-state usage applications (think database)        

Convertible Reserved Instnace:      
-> can change the EC2 instance type (e.g. t2.large to c3.large)        
-> up to 54% discount      

Scheduled Reserved Instances       
-> launch within specific time window you reserve          
-> require a fraction of day / week / month      
-> still commitment over 1 to 3 years      

**EC2 Spot Instances**:       
Provides the highest discount, can get up to 90% compared to On-Demand      
Instances that you can lose at any point of time if your max price (you are willing to pay for them) is less than the current spot price (the spot price changes over time)          
The MOST cost-efficient instances in AWS       

Useful for workloads that are resilient to failure (e.g. won't lose the progress of your work if you lose that instance)       

Recommended: batch jobs, data analysis, image processing, any distributed workloads, workloads with a flexible start and end time.       
Not suitable for critical jobs or databases.          

**EC2 Dedicated Hosts**:         
An Amazon EC2 Dedicated Host is a physical server with EC2 instances capacity fully dedicated to your use. Dedicated Hosts can help you address **compliance requirements** and reduce costs by allowing you to **use your existing server-bound software licenses**.       

These hosts are going to be allocated for a 3-year period reservation.      
More expensive     

Useful for software that have complicated licensing model (BYOL - Bring Your Own License)    
Or for companies that have strong regulatory or complicance needs.        
Since AWS shares all their server with everyone, this will ensure no one is using the server except you.      

**EC2 Dedicated Instances**:      
These are for EC2 Instances running on hardware that is dedicated to you.        
May share hardware with other instances in the same account.         
No control over instance placement (hardware control). So this is more like a software-version of Dedicated Host.           
<img src="images/dedicated_host.png" width="700">      

Which purchasing option is right for me ?       
On-Demand: coming and staying in resort whenever we like, we pay full price.           
Reserved: like planning ahead and if we plan to stay for a long time, we may get a good discount.        
Spot instances: the hotel allows people to bid for the empty rooms and the highest bidder keeps the room. You can get kick out at any time.       
Dedicated: we book entire building of the resort.        

An example of cost comparison using m4.large instance:    
<img src="images/m4_large.png" width="700">   

# EC2 - Solution Architect Associate Level             

## Private vs Public vs Elastic IP        

Networking has two sorts of IPs: **IPv4** and **IPv6**.             
IPv4: 4 numbers seperated by 3 dots, e.g. 1.160.10.240             
IPv6: 3ff2: 1900:4545:3:200:f8ff:f221:67cf                

IPv4 is still the most common format used online         
IPv6 is newer and solves problems for the Internet of Things (IoT)                

IPv4 allows for **3.7 billion** different addresses in the public space:             
[0-255].[0-255].[0-255].[0-255]                  

<img src="images/public_private_ip.png" width="700">              

When you have a public IP, you are accessible over the internet and when you have a private IP, you are only accessible within your private netowrk.             

**Fundamental Differences**:                  
Public IP:          
-> Public IP means the machine can be identified on the internet (WWW)             
-> must be unique across the whole web (not two machines can have the same public IP)           
-> can be geo-located easily           
Private IP:             
-> Private IP means the machine can only be identified on a private network only         
-> IP must be unique across the private network            
-> BUT two different private networks (e.g. 2 companies) can have the same IPs        
-> machines connect to WWW using a NAT + internet gateway (a proxy)         
-> only a specified of IPs can be used as private IP            

**Elastic IPs**         
When you stop and then start an EC2 instance, it can change its public IP.                
If you need to have a fixed public IP for your instance, you need an Elastic IP              
An Elastic IP is a public IPv4 IP you own as long as you don't delete it                
You can attach it to one instance at a time                   
With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account                    

You can only have 5 Elastic IP in your account (you can ask AWS to increase that)               

Overall, try to avoid using Elastic IP.               
-> they often reflect poor architectural decision             
-> instead, use a random public IP and register a DNS name to it                 
-> or, use a Load Balancer and don't use a public IP              

In EC2:         
By default, your EC2 machine comes with:         
-> a private IP for the internal AWS Network         
-> a public IP, for the WWW          

When we are doing SSH into our EC2 machines:         
-> we can't use a private IP, because we are not in the same network          
-> we can only use the public IP (if you don't have a VPN)         

If your machine is stopped and then started, the public IP can change            

We can find the Elastic IP in the EC2 console (under Network & Security), and we can allocate a new IP address from Amazon's pool of IPv4 addresses. By doing this we can create an IP address we own now, and this can be allocated to a specific EC2 instance. Now if we stop and restart an EC2 instance with an Elastic IP, (the public IPv4 is going to be the same as the Elastic IP associated to this EC2 instance), the Public IPv4 will remain the same.                

## Spot Instances & Spot Fleet    

Can get a discount of up to 90% compared to On-Demand          

Define **max spot price** and get the instance while **current spot price < max**              
-> the hourly spot price varies based on offer and capacity             
-> if the current spot price > your max price you can choose to **stop** or **terminate** your instance with a 2 minutes grace period              
Other strategy: **Spot Block**            
-> "block" spot instance during a specified time frame (1 to 6 hours) without interruptions                
-> in rare situations, the instance may be reclaimed             

Used for batch jobs, data analysis, or workloads that are resilient to failures.               
Not great for critical jobs or databases                

How do we terminate a spot instance ?                 

<img src="images/terminate_spot.png" width="700">                          

Consider a spot request: we are defining how many instances we want, maximum price we are willing to pay, launching specifications (AMI etc) and when our request is *valid from* and *valid until* and **request type**.             
There are 2 types of request types: **one-time request** or **persistent request**                

If it is a **one-time request**, as soon as your spot request is fulfiled, our instances are going to be launched and then the spot request **GOES AWAY**. If it is a **persistent**, this means that we want these requested instance as long as the spot request is valid from to valid until. This means that if the instances do get stopped/interrupted, then our spot requests will go back into action. AWS will restart spot instances for us when the conditions are met.                

We can only cancel Spot Instance requests that are open, active or disabled.               
Cancelling a spot request DOES NOT terminate instances (its our responsibility to terminate these spot instances).             
We must first cancel a spot request, and then terminate the associated spot instances, else the spot request will re-start the instances.                 

**Spot Fleets**                  
Spot Fleets = set of Spot Instances + (optional) On-demand Instances                  
The Spot Fleets will try to meet the target capacity with price constraints               
-> define possible launch pools: instance type (m5.large), OS, AZ               
-> we can have multiple launch pools, so that the fleet can choose. The fleet can choose the best and most appropriate launch pool for you                  
-> Spot Fleet stops launching instances when reaching capacity or max cost            

Strategies to allocate Spot Instances (EXAM):                
-> lowestPrice: from the pool with the lowest price (cost optimization, short workload)           
-> diversified: distributed across all pools (great for availability, long workloads)               
-> capacityOptimized: pool with the optimal capacity for the number of instances                 

Spot Fleets allow us to automatically request Spot Instances with the lowest price, i.e. Spot Fleet gives us an extra saving based on spot instances because it is smart enough to choose the right spot instance pools to allow us to get the maximum amount of savings.           

## EC2 Placement Groups

Sometimes we want control over the EC2 instance placement strategy (i.e. how the EC2 instances is placed within the AWS infrastructure)                

That strategy can be defined using placement groups              

When we create a placement group, you specify one of the following strategies for the group:          
-> *Cluster*: clusters instances into a low-latency group (hardware setup) in a single AZ - **high performance, high risk**            
-> *Spread*: spreads instances across underlying hardware (max 7 instances per group per AZ) - **critial applications**             
-> *Partition*: spreads instances across many different partitions (which rely on different sets of racks) within an AZ. Scales to 100s of EC2 instances per group (Hadoop, Cassandra, Kafka).                

**Cluster**:           

<img src="images/placement_cluster.png" width="700">                 

For Cluster, it means that all of our EC2 instances are on the same rack (means same hardware, same AZ).            
Pros: Great network (10 Gbps bandwidth between instances)           
Cons: if the rack fails, all instances fails at the same time                
Use cases:           
-> Big Data job that needs to complete fast            
-> Application that needs extremely low latency and high network throughput              
**Willing to take on the risk of failure**                    

**Spread**:              

<img src="images/placement_spread.png" width="700">               

We have 3 AZ and 6 EC2 instances, and each instance is on a different hardware.          
Pros:           
-> can span across AZ              
-> reduce risk in simultaneous failure             
-> EC2 Instances are on different physical hardware            

Cons:            
-> limited to 7 instances per AZ per placement group           

Use cases:              
-> Application that needs to maximize high availability           
-> Critical applications where each instance must be isolated from failure from each other           

**Partition**:               

<img src="images/placement_partition.png" width="700">             

We can have up to 7 partitions per AZ. And on each partition we can have many EC2 instances.         
Each partition represent a rack on AWS -> so instances are safe from rack failure affecting one another.              
Can span across multiple AZs in the same region               
Up to 100s of EC2 instances.               
The instances in a partition do not share racks with the instances in the other partitions             
A partition failure can affect many EC2 instances but won't affect other partitions             
EC2 instances get access to the partition information as metadata.                

Use cases: HDFS, HBase, Cassandra, Kafka                

We can create new placement group and assign EC2 instances during launching, or directly create the new placement group during the instance launching (after selecting AMIs etc)            


## Elastic Network Interfaces (ENI) - Overview             

Logical component in a VPC that represents a **virtual network card**             
They are used outside of EC2 instances as well.              

<img src="images/eni.png" width="700">             

For example we have 1 EC2 instance in a AZ. There is a primary ENI `Eth0` attached to it.           
This will provide your EC2 instance network connectivity and (e.g.) Private IP.              

Each ENI can have the following attributes:            
-> primary private IPv4, one or more secondary IPv4 (here `Eth1` is a secondary ENI, this will give another IPv4)                                
-> One Elastic IP (IPv4) per private IPv4           
-> One Public IPv4              
-> One or more security groups           
-> a MAC address             

You can create ENI independently and attach them on the fly (move them) on EC2 instances for failover         
In the example above, we can move `Eth1` so that the private IP is moved to the second EC2 instance.                      
Bound to a specific AZ.                 

ENI is automatically created during EC2 Launching, we can create ENI manually and attach to them. These manually created ENI is going to stay (under `Network interfaces`) after the EC2 instances are terminated.                

## EC2 Hibernate          

We can stop and terminate instances:             
-> Stop: the data on disk (EBS) i skept intact in the next start            
-> Terminate: any EBS volumes (root) also *set-up to be destroyed* is lost               

On start, the following happens:          
-> First start: the OS boots & the EC2 User Data script is run             
-> Following start (stop and then restart): the OS boots up, then your application starts, caches get warmed up, and that can take time           

**EC2 Hibernate**       
The in-memory (RAM) state is preserved          
The instance boot is much faster (the OS is not stopped/restarted)             
Under the hood: the RAM state is written to a file in the root EBS volume              
The root EBS volume must be encrypted           

<img src="images/ec2_hibernate.png" width="700">           

Use cases:           
-> long-running processing          
-> saving the RAM state          
-> services that take time to initialise             

EC2 Hibernate - Good to know           

Supported instance families - C3, C4, C5, M3, M4, M5, R3, R4 and R5          
Instance RAM size - must be less than 150 GB          
Instance size - not supported for bare metal instances              
AMI: Amazon Linux 2, Linux AMI, Ubuntu and Windows            
RootVolume: must be EBS (so not Instance Store), encrypted and large               
Available for On-Demand and Reserved Instances                  

An instance cannot be hibernated more than 60 days             

During EC2 launching, we can enable hibernation as an additional stop behavior              

## EC2 - Advanced Concepts (Nito, vCPU, Capacity Reservations)             

1. EC2 Nitro          

Underlying Platform for the next generation of EC2 instances               
New virtualisation technology             
Allows for better performances:               
-> better networking options (enhanced netowrking, HPC, IPv6)               
-> **High Speed EBS (Nitro is necessary for 64,000 EBS IOPS - max is 32,000 on non-Nitro)**           
Better underlying security             
Instance types example:         
-> Virtualised, A1, C5, C5a, C5ad, D3, D3gen, M5, M5a etc. (anything new will have Nitro in it)            
-> Bare metal: a1.metal, c5.metal, c6g.metal, etc.             

2. vCPU           

Multiple threads can run on one CPU or Core (multithreading)            
Each thread is represented as a virtual CPU (vCPU)             
e.g. launching m5.2xlarge:              
-> 4 CPU             
-> 2 threads per CPU (8 threads total)             
-> so 8 vCPU in total

We can optimise CPU options:           
EC2 instances come with a combination of RAM and vCPU              
In some rare cases, you may want to change the vCPU options (e.g. reduce):             
-> no. of CPU cores: you can decrease it (helpful if you need high RAM and low number of CPU) - decrease licensing costs           
-> no. of threads per core: disable multithreading to have 1 thread per CPU - helpful for high performance computing (HPC) workloads           

Only specified during the instance launch            

<img src="images/vcpu_1.png" width="700">             

3. Capacity Reservations         

Capacity Reservations ensure you have EC2 Capacity when needed          
Manual or planned end-date for the reservation         
No need for 1 or 3-year commitment           
Capacity access is immediate, you get billed as soon as it starts           

Specify:       
-> the AZ in which to reserve the capacity (only one), if needed in 3 AZ, we need to do 3 Capacity Reservations              
-> the number of instances for which to reserve capacity            
-> the instance attributes, including the instance type, tenancy, and platform/OS             

Combined with Reserved Instances and Saving Plans to do cost saving                 

# EC2 Instance Storage      

## EBS Overview    

## EBS Overview

An EBS (Elastic Block Store) Volume is a *network* drive you can attach to your instances while they run.         
It allows your instances to persist data, even after their termination: we can re-create the instances and mount the same EBS Volume from before and we will get back our data.              
They can only be **mounted to one instance at a time** (at the CCP exam level)      
They are bound to **a specific availability zone** when we create an EBS Volume: you cannot have an EBS Volume created in US-East-1A and attach to an instance in US-East-1B            

Analogy: think of them as a "network USB stick"             
Free tier: 30GB of free EBS storage of type General Purpose (SSD) or Magnetic per month         

EBS Volume:            
1. network drive (i.e. not a physical drive)            
-> it uses the network to communicate the instance, which means there might be a bit of latency from one computer to reach another server                
-> can be detached from an EC2 Instance and attached to another one quickly    
2. locked to an Availability Zone (AZ)        
-> an EBS volume in us-east-1a cannot be attached to us-east-1b             
-> to move a volume across from different AZ, we need to snapshot it            
3. Have provisioned capacity (i.e. we have to provision capacity in advance): size in GBs, and IOPS (IO operations per second)           

An EBS example is given below, at CCP level, one EBS can only be attached to one EC2 Instance, but multiple EBS volume can be attached to one EC2 Instance:               
<img src="images/ebs_eg.png" width="700">              

**Delete on Termination Attribute**         
When we create EBS volume through EC2 Instances, there is the Delete on Termination attribute.          

<img src="images/ebs_delete_terminate.png" width="700">              

By default, it is ticked for the Root Volume and not the new EBS volume.           
This controls the EBS behavior when an EC3 instance terminates             
-> By default, the root EBS volume is deleted (attribute enabled)             
-> By default, any other attached EBS volume is not deleted (attribute disabled)              
This can be controlled by the AWS console / AWS CLI              

Use case: preserve root volume when instance is terminated                    

## EBS Hands On

In the EC2 services, when we select the EC2 Instance, we can check the `Root Device` and `Block Devices`, and they both link the to same EBS Volume. When we click on them there will be an EBS ID (we can also access the EBS Volume under Elastic Block Store at the side bar).             

We can also create a stand-alone EBS volume in EC2 service. We will have to select the same Availability Zone as our instance. After creating the EBS Volume, it will appear in the `Elastic Block Store` under `Volumes`. We can then attach this volume to an instance.                 

If we terminate the EC2 Instance, the EBS Volumes which do not have "Delete on Termination" set to True will persist after the instance is terminated. By default, the root EBS Volume was created with termination in mind.      

## EBS Snapshots Overview

We can make a backup (snapshot) of our EBS volume at a point in time. We will be able to backup the state of it and even if the EBS volume is terminated later on, we can restore it from that backup.       

It is *not* necessary to detach volume to do snapshot, but *recommended*, just to make sure everything is clean on the EBS volume.      

We can also copy snapshots across Availability Zones or Region: we can transfer data in a different region to leverage on the global infrastructure of AWS.       

A simple illustration: the snapshot of the EBS volume will exist in your Region and can be used to restore into a EBS volume in another Availability Zone.                         
<img src="images/ebs_snapshot.png" width="700">           

We can create the snapshot in EC2 service and the snapshots can be seen under `Elatic Block Store` (at the side bar) under `Snapshots`.      

We can copy snapshot into a new snapshot. This new snapshot can be in *ANY* Region that we want.     

We can create an EBS volume from the snapshot, and we can create the volume in a different Availability Zones (but same Region from the original EBS volume)       

## AMI Overview

AMI = Amazon Machine Image           

They represent a customisation of an EC2 Instance       
-> add our own software, configuration, operating system, monitoring              
-> Faster boot / configuration time because all our software that we want to install is pre-packaged through AMI              

AMI are built for a **specific region**, and can be copied across Regions. 

We can launch EC2 Instances from:             
-> A Public AMI: AWS provided            
-> Your own AMI: you make and maintain them yourself            
-> An AWS Marketplace AMI: An AMI someone else made (and potentially someone sells them)               

AMI Process (from an EC2 Instance)               
-> start an EC2 instance and customize it      
-> stop the instance (for data integrity)        
-> build an AMI: this will create EBS snapshots behind the scenes              
-> finally we can launch instances from other AMIs       

Simple illustration on creating AMI and then use it to launch an EC2 instance:              
<img src="images/custom_ami.png" width="700">                    

To create an AMI from existing EC2 Instance, we right click -> image -> create image.     

After the AMI is created, we can go to Images (at the sidebar) -> AMI, select the AMI and create an EC2 Instance. Go to `Launch Instance` and instead of selecting existing public AMI, we can choose My AMIs. We still needs to select instance type (e.g. t2.micro) but we don't need to input "User Data". This can save a lot of time (e.g. configure and install software on our other EC2 Instances).       

## EC2 Instance Store

EBS volumes are **network drives** with good but "limited" performance         
**If we need a high-performance hardware disk, use EC2 Instance Store.** EC2 Instance is a virtual machine but it is attached to a real hardware server and some of these servers do have disk space that is attached directly with a physical connection onto the server.      

They have better I/O performance       
EC2 Instance Store lose their storage if they are stopped (ephemeral) i.e. the EC2 Instance that has an Instance Store are stopped or terminated                
User case: Good for buffer / cache / scratch data / temporary content but NOT for long-term storage              
Risk of data loss if hardware fails -> Backups and Replication are our responsibility              

If we see very high performance hardware attached volume for EC2 Instance, think local EC2 Instance Store.

## EBS Volume Types           

EBS Volumes come in 6 types.                
-> gp2 / gp3 (SSD): General purpose SSD Volume that balances price and performance for a wide variety of workloads           
-> io1 / io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads           
-> st1 (HDD): Low cost HDD volume designed for frequently accessed, throughput intensive workloads               
-> sc1 (HDD): Lowest cost HDD volume designed for less frequently accessed workloads                

EBS Volumes are characterized in Size | Throughput | IOPS (I/O Ops Per Sec)              

For EC2 instances, only gp2/3, io1/2 can be used as boot volumes (i.e. where the root OS is going to be running).            

EBS Volume Types Use Cases:                 
**General Purpose SSD**:                 
*Cost effective storage, low-latency*         
System boot volumes, Virtual desktops, Development and test environments                
1 GiB - 16 TiB           
gp3:         
-> newer generation of volumes        
-> baseline of 3,000 IOPS and throughput of 125 MiB/s         
-> can increase IOPS up to 16,000 and throughput up to 1000 MiB/s independently            
gp2:        
-> small gp2 volumes can burst IOPS to 3,000           
-> size of the volume and IOPS are linked, max IOPS is 16,000            
-> 3 IOPS per GB, means at 5334 GB we are at the max IOPS              

**Provisioned IOPS (PIOPS) SSD**:             
*Critical business applications* with sustained IOPS performance          
Or applications that need more than 16,000 IOPS        
Great for **database workloads** (sensitive to storage perf and consistency)               
io1 /  io2 (4 GiB - 16 TiB)             
-> max PIOPS: 64,000 for Nitro EC2 instances & 32,000 for other           
-> can increase PIOPS independently from storage size           
-> io2 have more durability and more IOPS per GiB (at the same price as io1)            

io2 Block Express (4 GiB - 64 TiB)           
-> sub-millisecond latency         
-> max PIOPS: 256,000 with an IOPS: GiB ration of 1,000:1            

*Supports EBS Multi-attach*           

**Hard Disk Drives (HDD)**:             
Cannot be a boot volume           
125 MiB to 16 TiB           
Throughput Optimized HDD (st1)           
-> Big Data, Data Warehouses, Log Processing           
-> Max throughput 500 MiB/s - max IOPS 500                 
Cold HDD (sc1)             
-> for data that is infrequently accessed          
-> scenarios where lowest cost is important            
-> Max throughput 250 MiB/s - max IOPS 250                 

Summary:             

<img src="images/ebs_summary.png" width="900">            

if we need more than 32,000 IOPS, we need EC2 Nitro with io1/2.                 

## EBS Multi-Attach           

For io1 / io2 family           

Attach the same EBS volume to multiple EC2 instances in the same AZ.           

<img src="images/ebs_multi.png" width="400">                  

Each instance has full read & write permissions to the volume              

Use case:          
-> achieve **higher application availability** in clustered Linux applications (e.g. Teradata)                
-> applications must manage concurrent write operations             

Must use a file system that's cluster-aware (not XFS, EX4, etc)              

## EBS Encryption           

When you create an encrypted EBS volume, you get the following:         
-> data at rest is encrypted inside the volume           
-> all the data in flight moving between the instance and the volume is encrypted          
-> all snapshots are encrypted         
-> all volumes created from the snapshot are encrypted             

Encryption and decryption are handled transparently (you have nothing to do)              

Encryption has a minimal impact on latency            

EBS Encryption leverages keys from KMS (AES-256)                 

Copying an unencrypted snapshot allows encryption                   

Snapshots of encrypted volumes are encrypted            

**Encrypt an unencrypted EBS volume**:                
Create an EBS snapshot of the volume           
Encrypt the EBS snapshot (using copy, or while copying we can choose to encrypt the copied snapshot)                  
Create new EBS volume from the snapshot (the volume will also be encrypted)              
Now you can attach the encrypted volume to the original instance          

As a shortcut, we can also take an unencrypted snapshot and while creating a volume out of the snapshot, choose encrypt this volume.          

## EBS RAID configurations           

EBS is already redundant storage (replicated within an AZ)         
But what if you want to increase IOPS to say 100,000 IOPS ?               
What if you want to mirror your EBS volumes ?             
You would mount volumes in parallel in RAID settings                  

RAID is possible as long as your OS supports it            
Some RAID options are:             
-> RAID 0                  
-> RAID 1                     
-> RAID 5 (not recommended for EBS - see documentation)             
-> RAID 6 (not recommended for EBS - see documentation)                 

RAID 0 (increase performance)               

<img src="images/raid_0.png" width="400">                   

Say we have one EC2 instance and this is backed by one logical volume. But this logical volume consist of 2 EBS Volume. It is either going to EBS Volume 1 or EBS Volume 2. When you write data, e.g. writing block A, B, C, D. They gets distributed between the two volumes.          

Combining 2 or more volumes and getting the total disk space and I/O.            
But one disk fails, all the data is failed             
We raise performance but increase our risk to have faults.               
Use cases would be:            
-> an application that needs a lot of IOPS and doesn't need fault-tolerance               
-> a database that has replication already built-in             

Using this, we can have a very big disk with a lot of IOPS                 

e.g. two 500 GiB Amazon EBS io1 volumes with 4,000 provisioned IOPS each -> 1,000 GiB RAID 0 array with an available bandwidth of 8,000 IOPS and 1,000 MB/s of throughput                 

RAID 1 (increase fault tolerance)                   

<img src="images/raid_1.png" width="400">                    

We have a similar setup, but this time we are going to write to both at the same time. So anytime we write a block A on Volume 1, it will also go to Volume 2.               

RAID 1 = Mirroring a volume to another              

If one disk fails, our logical volume is still working               
We have to send the data to two EBS volume at the same time (2 x network)                  
So we need the EC2 instance to have more network throughput to handle the writes to 2 EBS volumes at a time.                 

Use cases:             
-> Application that need increase volume fault tolerance              
-> Application where you need to service disks               

e.g. two 500 GiB Amazon EBS io1 volumes with 4,000 privisioned IOPS each -> 500 GiB RAID 1 array with an available bandwidth of 4,000 IOPS and 500 MB/s of throughput.                      

## EFS Overview
     
EFS is a managed NFS (network file system) that can be mounted on **100s of EC2** at a time. Recall that EBS Volume attached to only 1 EC2 Instance at a time. So EFS makes it a shared network file system.            

EFS works only with **Linux EC2 instances** and **works across multiple Availability Zones**. i.e. EFS can be attached to instances in different AZ.        

Highly available, scalable, expensive (3x gp2 EBS Volume), pay per use, no capacity planning            

<img src="images/efs.png" width="700">           

Use case: content management, web serving, data sharing, Wordpress           
Uses NFSv4.1 protocol                       
Uses security group to control access to EFS           
**Compatible with Linux based AMI (no Windows)**               
Encryption at rest using KMS               
POSIX file system (~Linux) that has a standard file API              
File system scales automatically, pay-per-use, no capacity planning              

EFS Scale:            
1000s of concurrent NFS clients, 10GB+/s throughput         
Grow to Petabyte-scale network file system, automatically            

Performance mode (set at EFS creation time)                
-> General purpse (default): latency-sensitive use cases (web server, CMS, Wordpress etc...), there is going to be alot of small files and you can access them very quickly. So EFS is built for that.                              
-> Max I/O - higher latency, throughout, highly parallel (big data, media processing)                

Throughput mode             
-> Bursting (1 TB = 50MiB/s + burst of up to 100 MiB/s)               
-> Provisioned: set your throughput regarless of storage size, e.g. 1 GiB.s for 1 TB storage (throughput usually grows with the file system's size) **small size file system but we want high throughput**                    

Storage Tiers (lifecycle management feature - move file after N days)                    
-> Standard: for frequently accessed files              
-> Infrequent access (EFS-IA): cost to retrieve files, lower price to store                 

**EFS Hands On**             

1. File system settings          
-> Name (optional)              
-> Automatic backup             
-> Lifecycle management (e.g. files not accessed after N days move to EFS Infrequent Access storage class)                 
-> Performance mode (General Purpose vs Max I/O)                 
-> Throughput mode (Bursting vs Provisioned (fixed throughput regardless file system size))                     
-> Encryption           

2. Network access              
-> VPC (choose VPC where you want EC2 instances to connect to your file system)                 
-> Mount targets (a mount target provides NFSv4 endpoint at which you can mount an EFS file system, recommend one mount target per AZ), and for each AZ we can define a security group (create the security group from EC2 console)                              

3. File system policy (optional)                     
4. Review and Create                 

After the EFS is created, we can create a few EC2 instance (in different AZ) to try to connect to the EFS. When we create the EC2 instance we can choose to add directly under "File systems". When configuring Security Group we can name a SG (allows SSH) so we can track and use this SG.                

We can SSH into each of these instance. Next we need to install EFS into the EC2 instances. From the EFS console, we can choose "Attach", and we can choose to mount the EFS via DNS or IP. There is a EFS mount helper, and in order to use this help we need to (go to the documentation) install a small package called `amazon-efs-utils`. So in the EC2 instance (after SSH in), key in:             
```
sudo yum install -y amazon-efs-utils
```
In order to use the helper we also need a directory for EFS, so in the EC2 console we can do:                   
```
mkdir efs
```
and then use the helper:                  
```
sudo mount -t efs -o tls fs-5dafeeac:/ efs
```
"tls" means there will be in flights encryption, and "fs-5dafeeac" is the ID for the EFS.                  

If you do these steps there will be a timeout, this is due to the Security Group of the EFS. We can add the inbound rules of the EFS's SG, the type is "NFS", and the source is the SG of the EC2 instances.          

Once the EFS is setup, then the 2 EC2 instances can access the files within the EFS simultaneously.             

## EBS vs EFS                   

**EBS** (Elastic Block Storage) Volumes:        

In general:              
-> can be attached to only one instance at a time              
-> are locked at the AZ level            
-> gp2: IO increases if the disk size increases                   
-> io1: can increase IO independently (great for running critical database)                  

To migrate an EBS volume across AZ              
-> take a snapshot           
-> restore the snapshot to another AZ            
-> EBS backups use IO and you should not run them while your application is handling a lot of traffic               

Root EBS volumes of instances get terminated by default if the EC2 instance gets terminated (you can disable that)                

<img src="images/ebs_1.png" width="500">                 

**EFS** Elastic File System:             

In general:                 
-> mounting 100s of instances across AZ            
-> EFS share websites files (WordPress)                    
-> Only for Linux Instances (POSIX)               
-> EFS has a higher price point than EBS (about 3x more expensive)            
-> Can leverage EFS-IA for cost savings               

For EFS we get billed only for what we use on EFS, for EBS we have to provision in advance a size that you know for EBS drive and we pay for the provision capacity and not the actual use capacity.             
   
<img src="images/efs_1.png" width="500">                  

# High Availability and Scalability: ELB & ASG

## High Availability and Scalability

**Scalability** means that an application / system can handle greater loads by adapting.        
There are two kinds of scalability in the Cloud:  
1. Vertical Scalability
2. Horizontal Scalability (= elasticity)         

Scalability is linked but different to High Availability.       

**Vertical Scalability**       
Vertical Scalability means increasing the size of the instance.          
For example, your application runs on t2.micro. Scaling that application *vertically* means running it on a t2.large, i.e. we change the size of our instance.         
Vertical scalability is very common for non-distributed system, such as a database. If we want to increase the performance of our database, we just increase the size of our database.           
There is usually a limit to how much you can vertically scale (hardware limit, even though the modern limits can be very very high)        

**Horizontal Scalability**            
Horizontal Scalability means increasing the number of instances / systems for your applications.         
Horizontal Scaling implies that we need to have a distributed system.      
This is very common for web applications / modern applications (usually design them with horizontal scalability in mind).       
It is easy to horizontally scale thanks to cloud offeringss such as AWS EC2.         

**High Availability**        
High Availability usually goes hand in hand with horizontal scaling           
High Availability means running your application / system in at least 2 Availability Zones on AWS        
The goal of high availability is to survive a data center loss (disaster)           

High availablilty can be passive (for RDS Multi AZ for example)               
High availability can be active (for horizontal scaling)                

High Availability & Scalability for EC2:         
Vertical Scaling: increase instance size (= scale up / down)          
-> from: t2.nano - 0.5GB of RAM, 1 vCPU        
-> to: u-12tb1.metal - 12.3 TB of RAM, 448 vCPUs          

Horizontal Scaling: Increase number of instances (= scale out / in)        
-> Auto Scaling Group       
-> Load Balancer        

High Availability: Run instances for the same application across multi AZ           
-> Auto Scaling Group multi AZ         
-> Load Balancer multi AZ            

Scalability vs Elasticity vs Agility (Exam !)       
Scalability: ability to accomodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)        

Elasticity: (more cloud native) once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friendly": pay-per-use, match demand, optimize costs            

Agility: (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minites.      

tbc 

# Things to do            

