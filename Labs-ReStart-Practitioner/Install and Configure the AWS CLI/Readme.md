## Install and Configure the AWS CLI

##Lab overview
The AWS Command Line Interface (AWS CLI) is a command line tool that provides an interface for interacting with products and services from Amazon Web Services (AWS).

You can install the AWS CLI on your local machine or a virtual machine such as an Amazon Elastic Compute Cloud (Amazon EC2) instance.

In this activity, you install and configure the AWS CLI on a Red Hat Linux instance because this instance type does not have the AWS CLI pre-installed. Some instance types, such as Amazon Linux, do come pre-installed with the AWS CLI. 

During this activity, you establish a Secure Shell (SSH) connection to the instance. You configure the installation with an access key that can connect to an AWS account. Finally, you practice using the AWS CLI to interact with AWS Identity and Access Management (IAM).

When you finish the activity, it will reflect the following diagram:
![image](https://github.com/user-attachments/assets/fd1819ec-06a8-4cc5-913a-76bb83d7e428)

## Objectives 
After completing this lab, you should be able to do the following:

Install and configure the AWS CLI.
Connect the AWS CLI to an AWS account.
Access IAM by using the AWS CLI.
Duration
This activity requires approximately 45 minutes to complete.

## Accessing the AWS Management Console
At the top of these instructions, choose Start Lab to launch the lab.

Wait until the message "Lab status: ready" appears, and then choose X to close the Start Lab panel.

Next to Start Lab, choose AWS, which opens the AWS Management Console in a new browser tab. The system automatically signs you in.

Tip If a new browser tab does not open, a banner or icon at the top of your browser will indicate that your browser is preventing the site from opening pop-up windows. Choose the banner or icon, and choose Allow pop-ups.

Arrange the AWS Management Console so that it appears alongside these instructions. 

Important: Do not change the lab Region unless specifically instructed to do so.

## Task 1: Connect to the Red Hat EC2 instance by using SSH
In this task, you log in to an existing EC2 instance.

Windows users
These instructions are specifically for Windows users. If you are using macOS or Linux, skip to the next section.

Select the Details drop-down menu above these instructions you are currently reading, and then select Show. A Credentials window will be presented.

Select the Download PPK button and save the labsuser.ppk file.
Typically your browser will save it to the Downloads directory.

Make a note of the PublicIP address.

Then exit the Details panel by selecting the X.

Download  PuTTY to SSH into the Amazon EC2 instance. If you do not have PuTTY installed on your computer, download it here.

Open putty.exe

Configure your PuTTY session by following the directions in the following link: Connect to your Linux instance using PuTTY

Windows Users: Select here to skip ahead to the next task.

## Task 2: Install the AWS CLI on a Red Hat Linux instance
In this task, you follow these steps from the terminal window to install the AWS CLI on a Red Hat Linux instance.

![1](https://github.com/user-attachments/assets/104ee813-6678-4047-a7a6-e94f8f57f61c)

-..To write the downloaded file to the current directory, run the following curl command with the -o option:
>>>> curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

-..To unzip the installer, run the following unzip command with the -u option. In this command, the unzip command prompts you to overwrite any existing files. To skip these prompts, the command includes the -u option.
>>>> unzip -u awscliv2.zip

-..To run the install program, run the following command. This sudo command grants write permissions to the directory. The installation command in the code snippet uses a file named install in the unzipped aws directory to install the AWS CLI. 
>>>>sudo ./aws/install

-..To confirm the installation, run the following command:
>>>> aws --version

-.. The following is an example of the output:
>>>> aws-cli/2.7.24 Python/3.8.8 Linux/4.14.133-113.105.amzn2.x86_64 botocore/2.4.5
Note: The version numbers that are installed change overtime and might not reflect this example.

-.. To verify that the AWS CLI is now working, run the following aws help command. The help command displays the information for the AWS CLI.
>>>> aws help
At the : prompt, enter q to exit.

## Task 3: Observe IAM configuration details in the AWS Management Console
In this task, you observe the IAM configuration details for the EC2 instance in the AWS Management Console. 

In the AWS Management Console, in the Search box, enter IAM and choose IAM. This option takes you to the IAM console page.
![2](https://github.com/user-attachments/assets/b0418af7-79fe-4609-8381-23608318ea6e)

Note: The IAM page that appears contains messages indicating that you do not have permission to observe some IAM service details. You can safely ignore these messages.

In the navigation pane, choose Users, and then choose awsstudent. 

You are now in the Permissions tab. Next to lab_policy, choose the arrow icon, and then choose the {} JSON button.

This lab_policy document is formatted in JSON. The IAM policy grants the awsstudent user access to specific AWS services in this account.

Choose the Security credentials tab. In the Access keys section, locate the awsstudent user's access key ID. 

Note: Once the access key is created, you must save the secret access key locally at the time that the key is created. For this lab, you can find the access key ID and the secret access key in the Details dropdown list at the top of these instructions. 

## Task 4: Configure the AWS CLI to connect to your AWS Account
In the SSH session terminal window, run the configure command for the AWS CLI:

aws configure
At the prompt, configure the following:

AWS Access Key ID: Choose the Details dropdown list, and choose Show. Copy and paste the AccessKey value into the terminal window.
AWS Secret Access Key: Copy and paste the SecretKey value into the terminal window.
Default region name: Enter us-west-2
Default output format: Enter json
Task 5: Observe IAM configuration details by using the AWS CLI
In this task, you observe the IAM configuration details for the EC2 instance using the AWS CLI.

In the terminal window, test the IAM configuration by running the following command:
![3](https://github.com/user-attachments/assets/f7008261-434e-464f-9afd-4007ae8bffae)

aws iam list-users
A successful test shows a JSON response that includes a list of IAM users in the account.
