## Build Your VPC and Launch a Web Server
 

## Objectives
After completing this lab, you should be able to:

Create a virtual private cloud (VPC)
Create subnets
Configure a security group
Launch an Amazon Elastic Compute Cloud (Amazon EC2) instance into a VPC
Duration
This lab takes approximately 45 minutes to complete.

## Scenario
In this lab, you use Amazon Virtual Private Cloud (VPC) to create your own VPC and add additional components to produce a customized network for a Fortune 100 customer. 
You also create security groups for your EC2 instance. You then configure and customize an EC2 instance to run a web server and launch it into the VPC that looks like the following customer diagram:

## Customer diagram
![architecture](https://github.com/user-attachments/assets/c5e1f53d-2efb-4dde-961d-fec89c899cce)

## AWS service restrictions
In this lab environment, access to AWS services and service actions might be restricted to the ones that you need to complete the lab instructions. You might encounter errors if you attempt to access 
other services or perform actions beyond the ones that this lab describes.

## Task 1: Create your VPC
In this task, you use the VPC Wizard to create a VPC, an internet gateway, and two subnets in a single Availability Zone. An internet gateway is a VPC component that allows communication between instances in your VPC and the internet.

After creating a VPC, you can add subnets. Each subnet resides entirely within one Availability Zone and cannot span zones. If a subnet's traffic is routed to an internet gateway, the subnet is known as a public subnet. If a subnet does not have a route to the internet gateway, the subnet is known as a private subnet.

The wizard also creates a NAT gateway, which is used to provide internet connectivity to EC2 instances in private subnets.

At the upper-right of these instructions, choose AWS. The AWS Management Console opens in a new tab.

Once you are in the AWS console, type and search for VPC in the search bar at the top. Select VPC from the list.

You are now in the Amazon VPC dashboard. You use the Amazon Virtual Private Cloud (Amazon VPC) service to build your VPC.

Choose Create VPC and configure the following options:

**Resources to create:** Choose **VPC and more**

**Name tag auto-generation:** UnCheck the box **Auto-generate**

**IPv4 CIDR:** Enter 10.0.0.0/16

**IPv6 CIDR block:** Choose **No IPv6 CIDR block.**

**Tenancy:** Choose Default.

**Number of Availability Zones (AZs)** :  1

**Number of public subnets:**  1

**Number of private subnets:**  1

**Expand Customize subnets CIDR blocks**

**Public subnet CIDR block in us-west-2a: 10.0.0.0/24**
**Private subnet CIDR block in us-west-2a: 10.0.1.0/24**
**NAT gateways: Choose In 1 AZ**

**VPC endpoints: Choose None**

On the Preview pane, name the resources as follows:

VPC: **Lab VPC**

Subnets (2)

First box, Public subnet one without name tag: Public Subnet 1
Second box, Private subnet one without name tag: Private Subnet 1
Route tables (2)

First box, Public route table without name tag: Public Route Table
Second box, Private route table without name tag: Private Route Table
**Choose Create VPC.**

On the next screen, Success message is displayed with VPC details. 

Choose View VPC. 

Lab VPC details are displayed as per configuration.
![1](https://github.com/user-attachments/assets/957f1d4a-9043-44cc-9770-6fc78e709a28)
![2](https://github.com/user-attachments/assets/8c86c8ec-d982-46ed-9ba9-50e339b8a965)
![3](https://github.com/user-attachments/assets/077ba6ae-5f26-49a7-98f0-63f0a2a0acd9)


## Task 2: Create additional subnets
In this task, you create two additional subnets in a second Availability Zone. This option is useful for creating resources in multiple Availability Zones to provide high availability.

In the left navigation pane, choose Subnets.

To configure the second public subnet, choose Create subnet and configure the following options:
![4](https://github.com/user-attachments/assets/352b7ec5-6f57-49b8-9f44-42748c12ea44)

**VPC ID:** From the dropdown list, choose Lab VPC.
**Subnet name:** Enter Public Subnet 2    
**Availability Zone:** No preference
**IPv4 CIDR block:** Enter 10.0.2.0/24
**Choose Create subnet.**
![5](https://github.com/user-attachments/assets/d83f61f6-0e9e-4579-90b6-d8725b11fd0d)

The subnet will have all IP addresses starting with **10.0.2.x.**

To configure the second private subnet, choose Create subnet and configure the following options:

**VPC ID:** From the dropdown list, choose Lab VPC.
**Subnet name:** Enter Private Subnet 2
**Availability Zone:** No preference
**IPv4 CIDR block:** Enter 10.0.3.0/24
**Choose Create subnet.**
![6](https://github.com/user-attachments/assets/5670ee9e-1fb5-432d-b605-c0d65f44ab04)

The subnet will have all IP addresses starting with 10.0.3.x.
![7](https://github.com/user-attachments/assets/11b3f6e3-beee-4039-9c9e-3ca370a55058)

## Task 3: Associate the subnets and add routes
In the left navigation pane, choose **Route Tables.**

Choose Public **Route Table**

In the lower pane, choose the **Subnet associations** tab.

Under **Subnets without explicit associations**, choose **Edit subnet associations.**
![8](https://github.com/user-attachments/assets/d8fbd425-e4ad-411a-a2b6-72ca498afaf1)

Select the check boxes for **Public Subnet 2.**

Choose **Save associations.**
![9](https://github.com/user-attachments/assets/3fddf8aa-e7de-45e0-ac56-d358abfd188a)

 You now configure the route table that is used by the private subnets.

Choose **Private Route Table**

In the lower pane, choose the **Subnet associations tab.**

Under Subnets without explicit associations, choose **Edit subnet associations.**

Select the check boxes for **Private Subnet 2.**

**Choose Save associations.**
![10](https://github.com/user-attachments/assets/46773970-d490-4388-82d4-f2ad652226dc)

 Your VPC now has public and private subnets configured in two Availability Zones:
 ![architecture1](https://github.com/user-attachments/assets/dc8f8831-e95d-481d-944d-22785d45a136)
 *Figure: The creation of the networking resources and routing components and attachment of these resources that make the VPC functional as a network.*

## Task 4: Create a VPC security group
In this task, you create a VPC security group, which acts as a virtual firewall for your instance. When you launch an instance, you associate one or more security groups with the instance. You can add rules to each security group that allow traffic to or from its associated instances.

In the left navigation pane, choose **Security Groups.**

Choose **Create security group.**

Configure the security group with the following options:
![11](https://github.com/user-attachments/assets/9e362f94-a412-497e-82db-4d9b1a0156cd)

**Security group name:** Enter Web Security Group
**Description:** Enter Enable HTTP access
**VPC:** Choose Lab VPC.
Under Inbound rules, choose **Add rule.**

Configure the following options:

**Type:** Choose HTTP.
**Source:** Choose Anywhere IPv4.
**Description:** Enter Permit web requests
**Choose Create security group.**
![12](https://github.com/user-attachments/assets/afad9a6b-cadc-4580-8c3d-9e54c9e9d40a)

You use this security group in the next task when launching an EC2 instance.

## Task 5: Launch a web server instance
In this task, you launch an EC2 instance into the new VPC. You configure the instance to act as a web server.
![13](https://github.com/user-attachments/assets/9d87b520-634d-49d2-af86-e64c9015d640)

On the AWS Management Console, in the Search bar, enter and choose EC2 to go to the **EC2 Management Console.**
In the left navigation pane, choose **Instances.**
Choose **Launch instances** and configure the following options:
In the Name and tags section, Name:  **Web Server 1.**

In the **Application and OS Images (Amazon Machine Image)** section, configure the following options:

Quick Start: **Choose Amazon Linux.**
Amazon Machine Image (AMI): From dropdown, Choose **Amazon Linux 2 AMI (HVM).**
In the Instance type section, choose **t3.micro.**

In the Key pair (login) section, choose **vockey.**

In the Network settings section, choose Edit and configure the following options:
VPC - required: **Choose Lab VPC.**

**Subnet: Choose Public Subnet 2.**

**Auto-assign public IP: Choose Enable.**

**Firewall (security groups): Choose Select existing security group.**

**Choose Web Security Group.**
Expand Advanced details

Under User data, copy and paste the following code:
#!/bin/bash
#Install Apache Web Server and PHP
yum install -y httpd mysql php
#Download Lab files
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
#Turn on web server
chkconfig httpd on
service httpd start

Choose **Launch instance.**
![14](https://github.com/user-attachments/assets/318dbf23-48ff-43f1-8722-9cb3ddc0244c)
![15](https://github.com/user-attachments/assets/f32fb458-1715-4a31-924c-5ff563804d6f)
![16](https://github.com/user-attachments/assets/43bd1ea5-2830-4008-8e76-828b41e2d1db)

To display the launched instance, choose View all instances.

Wait until the Web Server 1 shows 2/2 checks passed in the Status check column.

 This may take a few minutes. To update the page, choose refresh  at the top of the page.

You now connect to the web server running on the EC2 instance.

Select the check box for the instance, and choose the Details tab.

**Copy the Public IPv4 DNS value.**

Open a new web browser tab, paste the Public IPv4 DNS value, and press Enter.
![17](https://github.com/user-attachments/assets/36c40667-7443-4570-ad37-5dd843bf6ec9)
![18](https://github.com/user-attachments/assets/3ac48ee7-2758-42a4-8733-2b7d59ae51f6)

When successful, the page should look like the following:


*Figure: A picture of the end product, which is the delivery of the exact customer request: a fully functional VPC with its resources (network and security) and a web server*
![architecture](https://github.com/user-attachments/assets/8f46e419-594e-4490-b38d-b5bece85fac5)
