## Lab overview
AWS Systems Manager is a collection of capabilities that you can use to centralize operational data and automate tasks across your Amazon Web Services (AWS) resources. Systems Manager can configure and manage Amazon Elastic Compute Cloud (Amazon EC2) instances, on-premises servers, virtual machines, and other AWS resources at scale. 

## Objectives
After completing this lab, you should be able to use Systems Manager to do the following:

Verify configurations and permissions.
Run tasks on multiple servers.
Update application settings or configurations.
Access the command line on an instance.

## Task 1: Generate inventory lists for managed instances
You can use Fleet Manager, a capability of Systems Manager, to collect operating system information, application information, and metadata from EC2 instances, on-premises servers, or virtual machines in a hybrid environment. You can also use Fleet Manager to query metadata to quickly understand which instances are running the software and configurations that your software policy requires and which instances you need update.

In this task, you use Fleet Manager to gather inventory from an EC2 instance.

In the AWS Management Console, in the  search box, enter Systems Manager and press Enter. This option takes you to the Systems Manager console page.

In the left navigation pane, for Node Management, choose Fleet Manager.
![1](https://github.com/user-attachments/assets/7f78d360-0da5-491c-a8d4-22941f147a9c)

Choose the Account management dropdown list, and choose Set up inventory.
![2](https://github.com/user-attachments/assets/84de26ea-0850-4e96-b566-dc23277efce8)

To create an association that collects information about software and settings for your managed instance, choose the following options:

In the Provide inventory details section, for Name, enter Inventory-Association

In the Targets section, choose the following options:

For Specify targets by, choose Manually selecting instances.
Select the row for Managed Instance.
Leave the other options as the default settings.

Choose Setup Inventory

A banner with the message "Setup inventory request succeeded" appears on the Fleet Manager page. Inventory, a capability of Systems Manager, now regularly inventories the instance for the selected properties.

Choose the Node ID link, which directs you to the Node overview.

Choose the Inventory tab.
![3](https://github.com/user-attachments/assets/3ac7cc2c-9b95-4065-ba57-73cb6bb594fb)
This tab lists all of the applications in the instance. Take a moment to review the installed applications and other options in the Inventory type dropdown list.

You have successfully created a Systems Manager inventory association for your instance. Using Inventory, you can review and validate software configurations on your instances without needing to connect to each instance by using SSH.

## Task 2: Install a Custom Application using Run Command
In this task, you install a custom web application (Widget Manufacturing Dashboard) by using Run Command, a capability of Systems Manager.
![image](https://github.com/user-attachments/assets/fcde706f-c3c1-42b6-b0be-b49759d412a6)

In the upper-left corner, expand the menu icon. For Node Management, choose Run Command.

Choose Run command
![3](https://github.com/user-attachments/assets/fc99633a-6e79-42e9-af86-f4d29175e065)

A list appears of pre-configured documents for running common commands. 

Choose the search icon  in the box, and a dropdown box appears. Choose the following options: 

Owner
Owned by me
A document appears.

Note: Do not enter Owner or Owned by me. Entering this text does not return results. 

If the document is not already selected, select the button for the document.

The following information appears for this document:

Description Install Dashboard App
Document version: 1 (Default) 
Leave the Document version option set to this default. 

For Target selection, select Choose instances manually.
![4](https://github.com/user-attachments/assets/683b8b1e-f8fc-4b86-8c55-35afcc1a1c8f)

In the Instances section, select Managed Instance.

The Managed Instance has the Systems Manager agent installed. The agent has registered the instance to the service, which allows it to be selected for Run Command.

 It is also possible to identify target instances by using tags. By using tags, you can run a single command on a whole fleet of matching instances.

In the Output options section, clear Enable an S3 bucket.

Expand the AWS command line interface command section.

 This section displays the command line interface (CLI) command that initiates Run Command. You can copy this command and use it in the future within a script rather than having to use the AWS Management Console.

Choose Run
![5](https://github.com/user-attachments/assets/696c98c1-e53e-4e5b-a514-3ff732de1081)

 A banner with the Command ID indicates that it was successfully sent on the Command ID page.

After 1–2 minutes, the Overall status should change to Success. If it doesn't, choose the  refresh icon to update the status.

 You now validate the custom application that was installed.

In the Vocareum console, choose the following options: 

Choose the Details dropdown list at the top of these instructions.
Choose Show
Copy the ServerIP value. (This value is the public IP address.)
Open a new web browser tab, paste the IP address that you copied, and press Enter.

 The Widget Manufacturing Dashboard that you installed appears.
![6](https://github.com/user-attachments/assets/58cb16c7-0863-4a0a-b6a2-c084753e5ddc)

You have successfully used Run Command through Systems Manager to install a custom application onto your instance without needing to remotely access the instance by using SSH.

## Task 3: Use Parameter Store to manage application settings
Parameter Store, a capability of Systems Manager, provides secure, hierarchical storage for configuration data management and secrets management. You can store data such as passwords, database strings, and license codes as parameter values. You can store values as plain text or encrypted data. You can then reference values by using the unique name that you specified when you created the parameter.

In this task, you use Parameter Store to store a parameter that you use to activate a feature in an application.

Keep the Widget Manufacturing Dashboard browser tab open, and return to the AWS Systems Manager tab.

In the left navigation pane, for Application Management, choose Parameter Store.

Choose Create parameter
![7](https://github.com/user-attachments/assets/f41f34f1-fbb5-46ad-8f77-a01f03bf9db9)

Choose the following options:

For Name:, enter /dashboard/show-beta-features
For Description: , enter Display beta features
For Tier:, leave the default option. 
For Type:, leave the default option. 
For Value:, enter True
Choose Create parameter
![8](https://github.com/user-attachments/assets/41f7ef13-1f3c-4d18-84d1-b888f386e31e)

A banner with the message "Create parameter request succeeded" appears at the top of the page. 

The parameter can be specified as a hierarchical path, such as /dashboard/<option>.

The application that is running on Amazon EC2 automatically checks for this parameter. If it finds this existing parameter, then additional features are displayed.
![9](https://github.com/user-attachments/assets/baa0bef1-4638-4009-bab5-e5158d55c0ad)

Return to the web browser tab that displays the application, and refresh the web page.

 If you accidentally closed this browser tab, choose the Details dropdown list at the top of these instructions, choose Show and then copy and paste the ServerIP value into a new browser tab. 

Notice that three charts are displayed. The application is now checking Parameter Store to determine whether the additional chart (which is still in beta) should be displayed. It is common to configure applications to display "dark features" that are installed but not yet activated.

Optional: Delete the parameter, and then refresh the browser tab with the application. The third chart disappears again.

## Task 4: Use Session Manager to access instances
With Session Manager, a capability of Systems Manager, you can manage your EC2 instances through an interactive one-step browser-based shell or through the AWS Command Line Interface (AWS CLI). 
Session Manager provides secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, or manage SSH keys. You can also use Session Manager to help 
comply with corporate policies that require controlled access to instances, strict security practices, and fully auditable logs with instance access details while still providing end users with 
one-step cross-platform access to your EC2 instances.
![image](https://github.com/user-attachments/assets/892bc236-e582-401d-b409-2ca364ec38d4)

n this task, you access the EC2 instance through Session Manager.

In the left navigation pane, for Node Management, choose Session Manager.

Choose Start session
![10](https://github.com/user-attachments/assets/060f03f6-b088-4a9b-bec8-0fdfa456272a)

Select Managed Instance.

Choose Start session
![11](https://github.com/user-attachments/assets/25f5381a-f892-4701-ac3a-0b9529b8b63d)

A new session tab opens in your browser.

To activate the cursor, choose anywhere in the session window.

Run the following command in the session window:

ls /var/www/html
The output lists the application files that were installed on the instance.

Run the following command in the session window:

# Get region
AZ=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone`
export AWS_DEFAULT_REGION=${AZ::-1}

# List information about EC2 instances
aws ec2 describe-instances
The output lists the EC2 instance details for the Managed Instance in JSON format.
![12](https://github.com/user-attachments/assets/49ca6947-e4b8-4de1-9426-235c1013cf7c)

This task demonstrates how you can use Session Manager to log in to an instance without using SSH. You can also verify this capability by confirming that the SSH port is closed for the instance's security group.

You can restrict access to Session Manager through AWS Identity and Access Management (IAM) policies, and AWS CloudTrail logs Session Manager usage. These options provide better security and auditing than traditional SSH access.
