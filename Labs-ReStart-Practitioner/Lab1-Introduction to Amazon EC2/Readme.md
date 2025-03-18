##  Introduction to Amazon EC2

<img src="https://github.com/user-attachments/assets/bd2bec6b-76d2-417d-b9a3-f1b11e31c7b3" width="400">


## Lab overview
This lab provides you with a basic overview of launching, resizing, managing, and monitoring an Amazon EC2 instance.

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers.

Amazon EC2's simple web service interface allows you to obtain and configure capacity with minimal friction. It provides you with complete control of your computing resources and lets you run on Amazon's proven computing environment. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.

Amazon EC2 changes the economics of computing by allowing you to pay only for capacity that you actually use. Amazon EC2 provides developers the tools to build failure resilient applications and isolate themselves from common failure scenarios.

## Topics covered
By the end of this lab, you will be able to:

Launch a web server with termination protection enabled

Monitor Your EC2 instance

Modify the security group that your web server is using to allow HTTP access

Resize your Amazon EC2 instance to scale

Test termination protection

Terminate your EC2 instance

## Task 1: Launching your EC2 instance
  In this task, you will launch an Amazon EC2 instance with **Termination protection**. Termination protection prevents you from accidentally terminating an EC2 instance. You will deploy your instance with a User Data script that will allow you to deploy a simple web server.

In the AWS Management Console on the Services menu, choose EC2.
![a1](https://github.com/user-attachments/assets/5ea4e3cc-fad8-40e0-b0b8-ad44d73c5cc8)

In the left navigation pane, choose EC2 Dashboard to ensure that you are on the dashboard page.

Choose Launch instance, and then select Launch instance.
![a2](https://github.com/user-attachments/assets/c2b27b98-9639-413e-9620-0353c2e064da)

## Step 1: Naming your EC2 instance
When you name your instance, AWS creates a key value pair. The key for this pair is Name, and the value is the name you enter for your EC2 instance.

In the Name and tags pane, in the Name text box, enter Web Server.

## Step 2: Choosing an Amazon Machine Image (AMI)
An AMI provides the information required to launch an instance, which is a virtual server in the cloud. An AMI includes the following:

A template for the root volume for the instance (for example, an operating system or an application server with applications)

Launch permissions that control which AWS accounts can use the AMI to launch instances

A block device mapping that specifies the volumes to attach to the instance when it is launched

The Quick Start list contains the most commonly used AMIs. You can also create your own AMI or select an AMI from the AWS Marketplace, an online store where you can sell or buy software that runs on AWS.

Locate the Application and OS Images (Amazon Machine Image) pane. 

Under AMI Machine Image (AMI), notice that the Amazon Linux 2 AMI image is selected by default. Keep this setting.
![a3](https://github.com/user-attachments/assets/ec96ef25-7d16-466b-8fa0-a865f7d2bb90)

## Step 3: Choosing an instance type
Amazon EC2 provides a wide selection of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications. Each instance type includes one or more instance sizes so that you can scale your resources to the requirements of your target workload.

Select a t3.micro instance. This instance type has 2 virtual CPU and 1 GiB of memory.

From the dropdown, select t3.micro.

NOTE: You may be restricted from using other instance types in this lab.

## Step 4: Configuring a key pair
Amazon EC2 uses public–key cryptography to encrypt and decrypt login information. To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance.

In this lab, you do not log in to your instance, so you do not require a key pair.

In the Key pair (login) pane, select Proceed without a key pair (Not recommended).
![a4](https://github.com/user-attachments/assets/70f5941d-0da1-4ad3-9042-5886b3392e22)

## Step 5: Configuring the network settings 
You use this pane to configure networking settings.

The VPC indicates which virtual private cloud (VPC) you want to launch the instance into. You can have multiple VPCs, including different ones for development, testing, and production.

In the Network settings pane, choose Edit

For VPC - required, select Lab VPC.

Still in the Network settings pane, configure the Security Group as follows:

Security group name - required: Web Server security group

Description: Security group for my web server

A security group acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that allow traffic to or from its associated instances. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

Under Inbound security groups rules select the Remove

In this lab, you will not log into your instance using SSH. Removing SSH access will improve the security of the instance.
![a5](https://github.com/user-attachments/assets/728d4f12-f4bb-49db-bab4-8c8f5b95f210)


## Step 6: Adding storage
Amazon EC2 stores data on a network-attached virtual disk called Amazon Elastic Block Store (Amazon EBS).

You launch the EC2 instance using a default 8 GiB disk volume. This is your root volume (also known as a boot volume).

In the Configure storage pane, keep the default storage configuration.
![a6](https://github.com/user-attachments/assets/af16f0b1-6c18-4cee-9c21-c1c7948e99a8)


## Step 7: Configuring advanced details 
Expand the Advanced details pane.

Select the dropdown for Termination protection, then choose Enable.
![a7](https://github.com/user-attachments/assets/6a91d001-59ac-47b8-b7a9-db5103ebdaa4)


When you launch an instance in Amazon EC2, you have the option of passing user data to the instance. These commands can be used to perform common automated configuration tasks and even run scripts after the instance starts. 

Copy the following commands, and paste them into the User data text box.

#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<htm.l><h.1>Hello From Your Web Server!</h.1></html.>' > /var/www/html/index.html (without dots)

The script does the following:

Install an Apache web server (httpd)

Configure the web server to automatically start on boot

Activate the Web server

Create a simple web page

## Step 8: Launching an EC2 instance
Now that you have configured your EC2 instance settings, it is time to launch your instance.

In the right pane, choose Launch instance
![a8](https://github.com/user-attachments/assets/63f75080-cb49-449c-98a8-9a5f465c444d)

Choose View all instances

The instance appears in a Pending state, which means it is being launched. It then changes to Running, which indicates that the instance has started booting. There will be a short time before you can access the instance.

The instance receives a public DNS name that you can use to contact the instance from the Internet.

Select the  box next to your Web Server. The Details tab displays detailed information about your instance.

 To view more information in the Details tab, drag the window divider upward.

Review the information displayed in the Details, Security and Networking tabs.

Wait for your instance to display the following:
![a9](https://github.com/user-attachments/assets/833d4bc0-89b1-440c-bc90-8db09beccaef)


Note: Refresh if needed.

Instance State:  Running

Status Checks:   2/2 checks passed

## Task 2: Monitor Your Instance
Monitoring is an important part of maintaining the reliability, availability, and performance of your Amazon Elastic Compute Cloud (Amazon EC2) instances and your AWS solutions.

Select the instance by checking the box next to the instance and navigate to the bottom of the screen to the Status checks tab.

 With instance status monitoring, you can quickly determine whether Amazon EC2 has detected any problems that might prevent your instances from running applications. Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues.

Notice that both the System reachability and Instance reachability checks have passed.

Select the Monitoring tab.
![a10](https://github.com/user-attachments/assets/b732f9ab-4384-48a0-9fc9-b3ea3d1b488a)


This tab displays Amazon CloudWatch metrics for your instance. Currently, there are not many metrics to display because the instance was recently launched.


You can choose a graph to see an expanded view.

 Amazon EC2 sends metrics to Amazon CloudWatch for your EC2 instances. Basic (five-minute) monitoring is enabled by default. You can enable detailed (one-minute) monitoring.

In the Actions  menu, select Monitor and troubleshoot  Get Instance Screenshot.

<img src="https://github.com/user-attachments/assets/bfb3a636-b38e-48a1-8376-6c5c76ee1158" width="700">

![a11](https://github.com/user-attachments/assets/b7e7d34a-3c92-408d-98b9-25d340b2c087)

This shows you what your Amazon EC2 instance console would look like if a screen were attached to it.
![a12](https://github.com/user-attachments/assets/58b1b377-dbf2-4a94-a0fc-452247e10d03)


 If you are unable to reach your instance via SSH or RDP, you can capture a screenshot of your instance and view it as an image. This provides visibility as to the status of the instance, and allows for quicker troubleshooting.

Select Cancel located at the bottom of the instance screenshot.

 Congratulations! You have explored several ways to monitor your instance.


## Task 3: Update Your Security Group and Access the Web Server
When you launched the EC2 instance, you provided a script that installed a web server and created a simple web page. In this task, you will access content from the web server.

Select the instance by checking the box and select the Details tab.

Copy the Public IPv4 address of your instance to your clipboard.

Open a new tab in your web browser, paste the IP address you just copied, then press Enter.

Question: Are you able to access your web server? Why not?

You are not currently able to access your web server because the security group is not permitting inbound traffic on port 80, which is used for HTTP web requests. This is a demonstration of using a security group as a firewall to restrict the network traffic that is allowed in and out of an instance.

To correct this, you will now update the security group to permit web traffic on port 80.

Keep the browser tab open, but return to the EC2 Management Console tab.
![a13](https://github.com/user-attachments/assets/49440ca5-7062-4020-9f5f-206802cc5142)

In the left navigation pane, select Security Groups located under Network & Security.

Select  Web Server security group.

Select the Inbound rules tab.
![a14](https://github.com/user-attachments/assets/c356ea86-53d4-485a-b4ad-be674e3debef)


The security group currently has no rules.

Select Edit inbound rules then select Add rule and configure the rule with the following settings:

Type: HTTP

Source: Anywhere-IPv4

Select Save rules
![a15](https://github.com/user-attachments/assets/86d46dbf-97e7-4600-8130-49e5db5b9a2c)

Return to the web server tab that you previously opened and refresh  the page.

You should see the message Hello From Your Web Server!

 Congratulations! You have successfully modified your security group to permit HTTP traffic into your Amazon EC2 Instance.

 ![a16](https://github.com/user-attachments/assets/7119bc32-8c82-4e20-9907-301586a0b55f)


## Task 4: Resize Your Instance: Instance Type and EBS Volume
As your needs change, you might find that your instance is over-utilized (too small) or under-utilized (too large). If so, you can change the instance type. For example, if a t3.micro instance is too small for its workload, you can change it to an m5.medium instance. Similarly, you can change the size of a disk.

Stop Your Instance
Before you can resize an instance, you must stop it.


 When you stop an instance, it is shut down. There is no charge for a stopped EC2 instance, but the storage charge for attached Amazon EBS volumes remains.

On the EC2 Management Console, in the left navigation pane, select Instances.

 Web Server should already be selected.

Select Instance state > Stop instance.

Select Stop
![a17](https://github.com/user-attachments/assets/165b78a7-dccf-47f9-88a6-beb67b0d523f)
Your instance will perform a normal shutdown and then will stop running.

Wait for the Instance State to display: stopped
![a18](https://github.com/user-attachments/assets/a19458d9-8ad9-4d9c-a203-1bf20fd83ad6)

Change The Instance Type
In the Actions  menu, select Instance Settings  Change Instance Type, then configure:
![a19](https://github.com/user-attachments/assets/5d316814-a0d7-401e-b304-3e1d73708884)

Instance Type: t3.small

Select Apply
![a20](https://github.com/user-attachments/assets/bd799241-5230-4f4b-9ae7-dabee0781aae)


When the instance is started again it will be a t3.small, which has twice as much memory as a t3.micro instance. NOTE: You may be restricted from using other instance types in this lab.

Resize the EBS Volume
In the left navigation menu, select Volumes located under Elastic Block Store.

Select the volume by checking the box, and navigate to the Actions  menu, select Modify Volume.
![a21](https://github.com/user-attachments/assets/ca4bc902-4f96-4e22-be3a-6317e99cb022)


The disk volume currently has a size of 8 GiB. You will now increase the size of this disk.

Change the size to: 10 NOTE: You may be restricted from creating large Amazon EBS volumes in this lab.
![a22](https://github.com/user-attachments/assets/b97d1285-564b-4179-a8bd-b0e0b3405430)

Select Modify

Select Modify to confirm and increase the size of the volume.

Start the Resized Instance
You will now start the instance again, which will now have more memory and more disk space.

In left navigation pane, select Instances.

Select the Web Server instance by checking the box, then navigate to Instance state > Start instance.
![a23](https://github.com/user-attachments/assets/d49f4c4e-7ef8-4408-8d26-8edb4de94284)

Congratulations! You have successfully resized your Amazon EC2 Instance. In this task you changed your instance type from t3.micro to t3.small. You also modified your root disk volume from 8 GiB to 10 GiB.

 
## Task 5: Test Termination Protection
You can delete your instance when you no longer need it. This is referred to as terminating your instance. You cannot connect to or restart an instance after it has been terminated.

In this task, you will learn how to use termination protection.

In left navigation pane, select Instances.

Select the Web Server instance by checking the box and navigate to the top and select Instance state  menu, select  Terminate instance.

Note: There is a message that says: On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated. Storage on any local drives will be lost. It will ask if you are sure that you want to terminate the instance. You will be able to select the Terminate button.

![a24](https://github.com/user-attachments/assets/ec24addd-e31d-43f4-87fa-f8b8e14d85f1)

Note: You will notice that the instance did not terminate and a red error message pops up at the top that says: Failed to terminate an instance: The instance may not be terminated. This is because it has termination protection enabled.

In the Actions  menu, select Instance settings  Change termination protection.

Uncheck  Enable followed by Save
![a25](https://github.com/user-attachments/assets/86b90c5c-5aa4-4970-9df9-ff083c44679a)

You can now terminate the instance.

In the Actions  menu, select Instance State  Terminate instance.

Select Terminate

![a26](https://github.com/user-attachments/assets/04406cc8-38cf-497e-b048-4b0ea62a0dd6)

 Congratulations! You have successfully tested termination protection and terminated your instance.

## Lab Complete 
Choose  End Lab at the top of this page, and then select Yes to confirm that you want to end the lab.

A panel indicates that DELETE has been initiated... You may close this message box now.

A message Ended AWS Lab Successfully is briefly displayed, indicating that the lab has ended.

