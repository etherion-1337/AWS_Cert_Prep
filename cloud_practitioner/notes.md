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


