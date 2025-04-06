## Scaling and Load Balancing Your Architecture

## Lab overview
In this lab, you use the Elastic Load Balancing (ELB) and Amazon EC2 Auto Scaling to load balance and automatically scale your infrastructure.

ELB automatically distributes incoming application traffic across multiple Amazon Elastic Compute Cloud (Amazon EC2) instances. ELB provides the amount of load balancing capacity needed to route application traffic to help you achieve fault tolerance in your applications.

Auto Scaling helps you maintain application availability and gives you the ability to scale your Amazon EC2 capacity out or in automatically according to conditions that you define. You can use auto scaling to help ensure that you are running your desired number of EC2 instances. Auto scaling can also automatically increase the number of EC2 instances during spikes in demand to maintain performance and can decrease capacity during lulls to reduce costs. Auto scaling is well suited to applications that have stable demand patterns or that experience hourly, daily, or weekly variability in usage.  

The following is the starting architecture:
![image](https://github.com/user-attachments/assets/442a4efa-4305-40e6-8600-23c33597847d)

The following is the final architecture:

![image](https://github.com/user-attachments/assets/a0902326-76ce-42cf-9bc2-e953a08c581c)

## Objectives
After completing this lab, you should be able to do the following:

Create an AMI from an EC2 instance.

Create a load balancer.

Create a launch template and an Auto Scaling group.

Configure an Auto Scaling group to scale new instances within private subnets.

Use Amazon CloudWatch alarms to monitor the performance of your infrastructure.

## Task 1: Creating an AMI for auto scaling
In this task, you create an AMI from the existing Web Server 1. This action saves the contents of the boot disk so that new instances can be launched with identical content.

On the AWS Management Console, in the Search bar, enter and choose EC2 to open the Amazon EC2 Management Console.

In the left navigation pane, locate the Instances section, and choose Instances.

The Web Server 1 instance is listed. You now create an AMI based on this instance.

Choose the  Web Server 1 instance, which should appear in a  Running state.

From the Actions  dropdown list, choose Image and templates > Create image, and then configure the following options:

For Image name, enter Web Server AMI

For Image description - optional, enter Lab AMI for Web Server    

Choose Create image.

The confirmation screen displays the AMI ID for your new AMI. You use this AMI when launching the Auto Scaling group later in the lab.
![1](https://github.com/user-attachments/assets/2883fa26-5163-4048-966e-bc2f88b796c1)

![2](https://github.com/user-attachments/assets/9c8e6ad1-11cf-4ce0-b1ef-0d3f3fdd4d9c)

## Task 2: Creating a load balancer
In this task, you create a load balancer that can balance traffic across multiple EC2 instances and Availability Zones.

In the left navigation pane, locate the Load Balancing section, and choose Load Balancers.

Choose Create load balancer.

In the Load balancer types section, for Application Load Balancer, choose Create.

On the Create Application Load Balancer page, in the Basic configuration section, configure the following option:

For the Load balancer name, enter LabELB

In the Network mapping section, configure the following options:

For VPC, choose Lab VPC.

For Mappings, choose both Availability Zones listed.

For the first Availability Zone, choose Public Subnet 1.

For the second Availability Zone, choose Public Subnet 2.

These options configure the load balancer to operate across multiple Availability Zones.

In the Security groups section, choose the X for the default security group to remove it.

From the Security groups dropdown list, choose Web Security Group.

The Web Security Group has already been created for you, which permits HTTP access.

In the Listeners and routing section, choose the Create target group link.

Note: This link opens a new browser tab with the Create target group configuration options.

On the new Target groups browser tab, in the Basic configuration section, configure the following:

For Choose a target type, choose Instances.

For Target group name, enter lab-target-group

At the bottom of the page, choose Next.

On the Register targets page, choose Create target group.

Once the target group has been created successfully, close the Target groups browser tab.

Return to the Load balancers browser tab. In the Listeners and routing section, choose  Refresh to the right of the Forward to dropdown list for Default action.

From the Forward to dropdown list, choose lab-target-group.

At the bottom of the page, choose Create load balancer.

   You should receive a message similar to the following:

    Successfully created load balancer: LabELB

To view the LabELB load balancer that you created, choose View load balancer.

To copy the DNS name of the load balancer, use the copy option , and paste the DNS name into a text editor. 

You need this information later in the lab.

![3](https://github.com/user-attachments/assets/fdbad6e4-32c3-44c0-9269-3219949944ad)
![4](https://github.com/user-attachments/assets/0d4a5ccd-68ea-4d25-b00d-175e49058d85)
![5](https://github.com/user-attachments/assets/20998cf2-35d9-4c92-8b45-2c7edeccdbf1)
![6](https://github.com/user-attachments/assets/03827d00-fe65-4d18-8c8f-1f41b7100e74)
![7](https://github.com/user-attachments/assets/11c17d9f-4b76-4b19-811f-f66feef7594d)
![8](https://github.com/user-attachments/assets/f7271568-240b-4a24-a2c7-59baf6b31670)
![9](https://github.com/user-attachments/assets/caaf256f-0844-4fbe-9e09-73f445b23898)

## Task 3: Creating a launch template 
In this task, you create a launch template for your Auto Scaling group. A launch template is a template that an Auto Scaling group uses to launch EC2 instances. When you create a launch template, you specify information for the instances, such as the AMI, instance type, key pair, security group, and disks.

At the top of the AWS Management Console, in the search bar, enter and choose EC2

In the left navigation pane, locate the Instances section, and choose Launch Templates.

Choose Create launch template.

On the Create launch template page, in the Launch template name and description section, configure the following options:

For Launch template name - required, enter lab-app-launch-template

For Template version description, enter A web server for the load test app

For Auto Scaling guidance, choose  Provide guidance to help me set up a template that I can use with EC2 Auto Scaling.

In the Application and OS Images (Amazon Machine Image) - required section, choose the My AMIs tab. Notice that Web Server AMI is already chosen.

In the Instance type section, choose the Instance type dropdown list, and choose t3.micro.

In the Key pair (login) section, confirm that the Key pair name dropdown list is set to Don't include in launch template.

   Amazon EC2 uses public key cryptography to encrypt and decrypt login information. To log in to your instance, you must create a key pair, specify the name of the key pair when you launch the instance, and provide the private key when you connect to the instance.

  Note: In this lab, you do not need to connect to the instance.

In the Network settings section, choose the Security groups dropdown list, and choose Web Security Group.

  When you launch an instance, you can pass user data to the instance. The data can be used to run configuration tasks and scripts.

Choose Create launch template.

		You should receive a message similar to the following:

		 Successfully created lab-app-launch-template.

Choose View launch templates.
![10](https://github.com/user-attachments/assets/2bffef5f-46b9-4abe-a2c9-10bc662fa057)
![11](https://github.com/user-attachments/assets/c8f8b995-9a5f-4b35-8742-850efff38a9a)
![12](https://github.com/user-attachments/assets/1441fcf9-16fd-4b16-bd7d-dd703ba6303b)
![13](https://github.com/user-attachments/assets/2f06e130-320a-4c30-8a65-d54885eb7796)

## Task 4: Creating an Auto Scaling group
In this task, you use your launch template to create an Auto Scaling group.

Choose  lab-app-launch-template, and then from the Actions  dropdown list, choose Create Auto Scaling group

On the Choose launch template or configuration page, in the Name section, for Auto Scaling group name, enter Lab Auto Scaling Group

Choose Next.

On the Choose instance launch options page, in the Network section, configure the following options:

From the VPC dropdown list, choose Lab VPC.

From the Availability Zones and subnets dropdown list, choose Private Subnet 1 (10.0.1.0/24) and Private Subnet 2 (10.0.3.0/24). 

Choose Next.

On the Configure advanced options – optional page, configure the following options: 

In the Load balancing – optional section, choose Attach to an existing load balancer.

In the Attach to an existing load balancer section, configure the following options:

Choose Choose from your load balancer target groups.

From the Existing load balancer target groups dropdown list, choose lab-target-group | HTTP.

In the Health checks – optional section, for Health check type, choose  ELB.

Choose Next.

On the Configure group size and scaling policies – optional page, configure the following options: 

In the Group size – optional section, enter the following values: 

Desired capacity:2

Minimum capacity: 2

Maximum capacity: 4

In the Scaling policies – optional section, configure the following options:

Choose  Target tracking scaling policy.

For Metric type, choose Average CPU utilization.

Change the Target value to 50

This change tells Auto Scaling to maintain an average CPU utilization across all instances of 50 percent. Auto Scaling automatically adds or removes capacity as required to keep the metric at or close to the specified target value. It adjusts to fluctuations in the metric due to a fluctuating load pattern.

Choose Next.

On the Add notifications – optional page, choose Next.

On the Add tags – optional page, choose Add tag and configure the following options:

Key: Enter Name

Value - optional: Enter Lab Instance

Choose Next.

Choose Create Auto Scaling group.

These options launch EC2 instances in private subnets across both Availability Zones.

Your Auto Scaling group initially shows an Instances count of zero, but new instances will be launched to reach the desired count of two instances.

Note: If you experience an error related to the t3.micro instance type not being available, then rerun this task by choosing the t2.micro instance type instead.

![14](https://github.com/user-attachments/assets/ebb3069c-4377-44a0-ac9b-4013a89685ed)
![15](https://github.com/user-attachments/assets/580efcc7-0d85-41e9-9edc-4a238bf3e947)
![16](https://github.com/user-attachments/assets/a011b618-81db-47ba-ab42-8aa1de96e258)
![17](https://github.com/user-attachments/assets/f7cdfffd-0f11-4660-ac2d-970e8f2ea183)
![18](https://github.com/user-attachments/assets/171c2d09-8c78-4594-99bc-03976beb3289)
![19](https://github.com/user-attachments/assets/552c5fd2-ad19-42b8-ba87-b3ace7603888)
![20](https://github.com/user-attachments/assets/3e070392-df6d-4c1e-a4ff-595a36bb470b)

## Task 5: Verifying that load balancing is working
In this task, you verify that load balancing is working correctly.

In the left navigation pane, locate the Instances section, and choose Instances.

You should see two new instances named Lab Instance. These instances were launched by auto scaling.  If the instances or names are not displayed, wait 30 seconds, and then choose refresh .

First, you confirm that the new instances have passed their health check.

In the left navigation pane, in the Load Balancing section, choose Target Groups.

Choose lab-target-group.

In the Registered targets section, two Lab Instance targets should be listed for this target group.

Wait until the Health status of both instances changes to healthy. To check for updates, choose refresh .

A healthy status indicates that an instance has passed the load balancer's health check. This check means that the load balancer will send traffic to the instance.

You can now access the instances launched in the Auto Scaling group using the load balancer.

Open a new web browser tab, paste the DNS name that you copied before, and press Enter.

The Load Test application should appear in your browser, which means that the load balancer received the request, sent it to one of the EC2 instances, and then passed back the result.

![21](https://github.com/user-attachments/assets/79d9b2b5-6733-4d4d-84c7-7e68bc9ad210)
![22](https://github.com/user-attachments/assets/6ad69bb2-d378-47cd-879f-be75d0d6a6ed)

## Task 6: Testing auto scaling
You created an Auto Scaling group with a minimum of two instances and a maximum of four instances. Currently, two instances are running because the minimum size is two and the group is currently not under any load. You now increase the load to cause auto scaling to add additional instances.

Return to the AWS Management Console, but keep the Load Test application tab open. You return to this tab soon.

In the AWS Management Console, in the search bar, enter and choose CloudWatch

In the left navigation pane, in the Alarms section, choose All alarms.

Two alarms are displayed. The Auto Scaling group automatically created these two alarms. These alarms automatically keep the average CPU load close to 50 percent while also staying within the limitation of having 2–4 instances.

Choose the alarm that has AlarmHigh in its name. This alarm should have a State of OK.

 If the alarm is not showing OK for the State, wait a minute and then choose refresh  until the State changes.

The OK state indicates that the alarm has not been initiated. It is the alarm for CPU Utilization > 50, which adds instances when the average CPU utilization is high. The chart should show very low levels of CPU at the moment. 

You now tell the application to perform calculations that should raise the CPU level.

Return to the browser tab with the Load Test application.

Next to the AWS logo, choose Load Test.

This step causes the application to generate high loads. The browser page automatically refreshes so that all instances in the Auto Scaling group will generate loads. Do not close this tab.

Return to browser tab with the CloudWatch Management Console.

In less than 5 minutes, the AlarmLow alarm status should change to OK, and the AlarmHigh alarm status should change to In alarm.

 To update the display, choose refresh  every 60 seconds.

You should see the AlarmHigh chart indicating an increasing CPU percentage. Once it crosses the 50 percent line for more than 3 minutes, it initiates auto scaling to add additional instances.

Wait until the AlarmHigh alarm enters the In alarm state.

You can now view the additional instance or instances that were launched.

In the AWS Management Console, in the search bar, enter and choose EC2 

In the left navigation pane, locate the Instances section, and choose Instances.

More than two instances named Lab Instance should now be running. Auto scaling created the new instances in response to the alarm.

![23](https://github.com/user-attachments/assets/76f7bf8e-4841-4acb-92cc-d38299bf930f)
![24](https://github.com/user-attachments/assets/a0653c33-628d-419a-8498-4d32a2138227)
![25](https://github.com/user-attachments/assets/627eb759-dc79-4c18-a769-a26c61e1890c)












