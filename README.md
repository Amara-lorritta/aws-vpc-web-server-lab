## **Build Your VPC and Launch a Web Server**
## **Overview**

This lab demonstrates how to build a custom Amazon Virtual Private Cloud (VPC) from scratch, configure public and private subnets, establish internet connectivity via an Internet Gateway (IGW) and NAT Gateway, and deploy a web server on an EC2 instance within the public subnet.

It provides the understanding of AWS networking, subnet isolation, routing, and security configuration using VPC, EC2, and Security Groups.

## **Objectives & Learning Outcomes**

After completing this lab, I will be able to:

Create and configure a custom VPC.

Set up public and private subnets in multiple Availability Zones.

Associate subnets with route tables for correct traffic flow.

Create a security group that allows inbound HTTP (port 80) access.

Launch and test an EC2 web server within the public subnet.

## **Architecture**

<img width="600" height="400" alt="ecc0dbaf-395b-4813-ae24-9f315e374f61" src="https://github.com/user-attachments/assets/6cdcbe08-c5f3-4dd7-820e-2c368fa45a64" />

## **Flow Summary**

User accesses the AWS Management Console.

A custom VPC (10.0.0.0/16) is created.

Public subnets host the EC2 Web Server and NAT Gateway.

Private subnets host internal components without direct internet access.

Route Tables direct public traffic to the Internet Gateway and private traffic to the NAT Gateway.

Web Security Group allows HTTP access from anywhere.

## **Commands and Steps**
```
bash
# Step 1: Create VPC
VPC Name: Lab VPC
IPv4 CIDR: 10.0.0.0/16

# Step 2: Create Subnets
Public Subnet 1: 10.0.0.0/24
Private Subnet 1: 10.0.1.0/24
Public Subnet 2: 10.0.2.0/24
Private Subnet 2: 10.0.3.0/24

# Step 3: Configure Routing
Public Route Table → Internet Gateway (IGW)
Private Route Table → NAT Gateway

# Step 4: Create Security Group
Name: Web Security Group
Inbound Rule: HTTP (port 80) from Anywhere IPv4

# Step 5: Launch EC2 Instance
AMI: Amazon Linux 2
Instance Type: t3.micro
VPC: Lab VPC
Subnet: Public Subnet 2
Public IP: Enabled
Security Group: Web Security Group

# Step 6: Install Web Server
#!/bin/bash
yum install -y httpd mysql php
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
chkconfig httpd on
service httpd start

# Step 7: Verify
Access the Public IPv4 DNS in a browser → Web page should display success message.
```
## **Screenshots**

vpc-creation.png	Custom VPC created with 10.0.0.0/16 CIDR block

<img width="1621" height="653" alt="Screenshot 2025-10-13 075440" src="https://github.com/user-attachments/assets/6af6ec51-6b26-47a9-ade8-0f4317eda35d" />

subnets.png	Public and private subnets in multiple AZs

<img width="600" height="400" alt="Screenshot 2025-10-13 081103" src="https://github.com/user-attachments/assets/f108fdd3-e5dc-43d5-a828-a70a63615f49" />

security-group.png	HTTP access allowed from any IPv4 address

<img width="600" height="500" alt="Screenshot 2025-10-13 082849" src="https://github.com/user-attachments/assets/781f849c-7556-4b37-bf23-0f0a03a591ee" />

webpage-success.png	Browser confirms web server launched successfully
<img width="600" height="300" alt="Screenshot 2025-10-13 090617" src="https://github.com/user-attachments/assets/32e296fb-55ee-44ed-8763-6bec503ad138" />


## **Tools Used**

Amazon VPC,  Amazon EC2

Internet Gateway (IGW), NAT Gateway

Security Groups,  Route Tables

Apache Web Server


## **What Actually Happened** 

Created a custom VPC (10.0.0.0/16) to define an isolated network.

Added four subnets (two public, two private) across two Availability Zones for high availability.

Configured route tables to direct public traffic through the IGW and private traffic through the NAT Gateway.

Created a Web Security Group that allows inbound HTTP access on port 80.

Deployed an EC2 instance into a public subnet, installed Apache via a user data script, and confirmed successful web hosting.

Verified connectivity by visiting the public DNS, confirming that the web server was serving content correctly.


## **Key Takeaways**

Understood VPC architecture and subnet isolation.

Learned how to route public and private traffic securely.

Implemented least privilege network access with Security Groups.

Gained experience deploying a web server in a custom network.

Reinforced core AWS networking and infrastructure concepts.


## **Author**

Amarachi Emeziem

Cloud Security & IT Support Specialist | AWS & Azure Certified
