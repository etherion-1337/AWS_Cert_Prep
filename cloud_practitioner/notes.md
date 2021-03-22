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

3) Hardware Key Fob MFA Device:    
Gemalto (3rd party)      

4) Hardware Key Fob MFA Device for AWS GovCloud (US):           
SurePassID (3rd party)        

