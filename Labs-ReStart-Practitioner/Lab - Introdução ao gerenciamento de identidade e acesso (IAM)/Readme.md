## Introduction to AWS Identity and Access Management (IAM)

In many business environments, access involves a single login to a computer or a network of computer systems that provides the user access to all resources on the network. This access includes rights to personal and shared folders on a network server, company intranets, printers, and other network resources and devices. Unauthorized users can quickly exploit these same resources if the access control and associated authentication procedures are not set up properly.

In this lab, you will explore users, user groups, and policies in the AWS Identity and Access Management (IAM) service.

Objectives
After completing this lab, you should be able to:

Create and apply an IAM password policy
Explore pre-created IAM users and user groups
Inspect IAM policies as applied to the pre-created user groups
Add users to user groups with specific capabilities active
Locate and use the IAM sign-in URL
Experiment with the effects of policies on service access
Here is diagram of the current environment with the listed IAM users and IAM groups.
![image](https://github.com/user-attachments/assets/00acaef1-203f-4a49-a781-44e310808f27)


## Other AWS services

IAM can be used for the following:

1) Manage IAM users and their access: You can create users and assign them individual security credentials (access keys, passwords, and multi-factor authentication devices). You can manage permissions to control which operations a user can perform.

2) Manage IAM roles and their permissions: An IAM role is similar to a user in that a role is an AWS identity with permission policies that determine what the identity can and cannot do in Amazon Web Services (AWS). However, instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it.

3) Manage federated users and their permissions: You can activate identity federation to allow existing users in your enterprise to access the AWS Management Console, to call AWS application programming interfaces (APIs), and to access resources without the need to create an IAM user for each identity.


## Task 1: Create an account password policy
In this task, you create a custom password policy for your AWS account. This policy affects all the users associated with the account.

First, note the Region that you are in (for example, Oregon). The upper-right corner of the console page displays your Region.
![1](https://github.com/user-attachments/assets/0cd6c77d-7b04-43a3-b46f-496fd4ad336e)


In the AWS Management Console, in the search  box, enter IAM and select it.

In the left navigation pane, choose Account settings.
![2](https://github.com/user-attachments/assets/39c63962-daba-4009-8f3d-b95f07cbabc5)


Here you can see the default password policy that is currently in effect. The company that you are working for has much stricter requirements, and you need to update this policy.

Choose Change password policy.

Under Select your account password policy requirements, configure the following options:

For Enforce minimum password length, change 8 to 10 characters.
Select every check box except the check box for Password expiration requires administrator reset.
For Enable password expiration, leave the default option of 90 days. 
For Prevent password reuse, leave the default option of 5 passwords.
Choose Save changes.

These changes take affect at the AWS account level and apply to every user associated with the account.
![3](https://github.com/user-attachments/assets/5d6b8d42-b94f-4841-a361-107c7dae7b3f)

## Summary of task 1
In this task, you strengthened the password requirements by creating a custom password policy. The various password options that you selected have now made the passwords that the users create much more difficult to crack.


## Task 2: Explore users and user groups
In this task, you explore the users and user groups that have already been created for you in IAM.

In the left navigation pane, choose Users.

The following IAM users have been created for you:

user-1
user-2
user-3
Choose user-1.
![4](https://github.com/user-attachments/assets/812b2e8b-6e74-4fd5-91ee-778d12b74256)

This option bring you to a Summary page for user-1. The Permissions tab is displayed. 

Notice that user-1 does not have any permissions.
![5](https://github.com/user-attachments/assets/d4840c04-a7e2-4fd7-a078-a5e4aba74dc9)


Choose the Groups tab.

user-1 is also is not a member of any user groups.
![6](https://github.com/user-attachments/assets/ff8d9f4c-ad52-4a25-b877-9419d6423fee)

 A user group consists of several users who need access to the same data. Privileges can be distributed to the entire group of users rather than to each individual. This option is much more efficient when applying permissions and provides greater overall control of access to resources than applying permissions to individuals.

Choose the Security credentials tab.
![7](https://github.com/user-attachments/assets/ea969310-0478-44ad-98d0-a6905291b959)

user-1 is assigned a Console password.

In the left navigation pane, choose User groups.
![8](https://github.com/user-attachments/assets/fddd7f80-0ca5-4002-af96-6966a5c07ebb)

The following user groups have already been created for you:

EC2-Admin
EC2-Support
S3-Support
Choose the EC2-Support group.

This option brings you to the Summary page for the EC2-Support group.

Choose the Permissions tab.

![9](https://github.com/user-attachments/assets/58d3a85e-ef2f-4a20-bab9-0e25741c003c)

This group has a managed policy associated with it called AmazonEC2ReadOnlyAccess. Managed policies are pre-built policies (built either by AWS or by your administrators) that can be attached to IAM users and user groups. When the policy is updated, the changes to the policy are immediately applied to all users and user groups that are attached to the policy.

Next to the AmazonEC2ReadOnlyAccess policy, select the plus sign to show the policy.

A policy defines what actions are allowed or denied for specific AWS resources. This policy grants permission to list and describe information about Amazon Elastic Compute Cloud (EC2), Elastic Load Balancing (ELB), Amazon CloudWatch, and Amazon EC2 Auto Scaling. This ability to view resources but not modify them is ideal for assigning to a support role.

The following is the basic structure of the statements in an IAM policy:

Effect indicates whether to Allow or Deny the permissions.
Action specifies the API calls that can be made against an AWS service (for example, cloudwatch:ListMetrics).
Resource defines the scope of entities covered by the policy rule (for example, a specific Amazon Simple Storage Service [Amazon S3] bucket, EC2 instance, or * which means any resource).
In the left navigation pane, choose User groups.

Choose the S3-Support group.
![10](https://github.com/user-attachments/assets/68407c18-c15d-4af0-8ecb-13482831cc69)


Choose the Permissions tab.

The S3-Support group has the AmazonS3ReadOnlyAccess policy attached.

Next to the AmazonS3ReadOnlyAccess policy, select the plus sign to show the policy. 

This policy has permissions to get and list resources in Amazon S3.

In the left navigation pane, choose User groups.

Choose the EC2-Admin group.

Choose the Permissions tab.
![11](https://github.com/user-attachments/assets/4083af66-16d5-43fd-b468-125f8646f064)


This group is slightly different from the other two. Instead of a managed policy, it has a Customer inline policy, which is a policy assigned to only one user or group. Inline policies are typically used to apply permissions for one-off situations.

Next to the EC2-Admin-Policy policy, select the plus sign to show the policy. 

This policy grants permission to view (Describe) information about Amazon EC2 and also the ability to start and stop instances.

## Business scenario
For the remainder of this lab, you work with these users and user groups to activate permissions supporting the following business scenario:

Your company is growing its use of AWS and is using many EC2 instances and a great deal of Amazon S3 storage. You want to give access to new staff members depending upon their job function:

User	In Group	Permissions
user-1	S3-Support	Read-only access to Amazon S3
user-2	EC2-Support	Read-only access to Amazon EC2
user-3	EC2-Admin	View, start, and stop EC2 instances

## Task 3: Add users to user groups
You have recently hired user-1 into a role where they will provide support for Amazon S3. You add them to the S3-Support group so that they inherit the necessary permissions via the attached AmazonS3ReadOnlyAccess policy.

 You can ignore any not authorized errors that appear during this task. They are caused by your lab account having limited permissions and should not impact your ability to complete the lab.

## Add user-1 to the S3-Support group
In the left navigation pane, choose User groups.

Choose the S3-Support group.
![12](https://github.com/user-attachments/assets/9db2ee58-4d6b-4b64-8e4a-2ecd6522b027)

Choose the Users tab.

In the Users tab, choose Add users.
![13](https://github.com/user-attachments/assets/79974ae5-0636-4aa6-a637-bbd3f4e7fe3e)

In the Add users to S3-Support window, configure the following options:

Select the check box for user-1.
Choose Add Users.
In the Users tab, you see that user-1 has been added to the group.

## Add user-2 to the EC2-Support group
You have hired user-2 into a role where they provide support for Amazon EC2.

Using the previous steps in this task, add user-2 to the EC2-Support group.

user-2 should now be part of the EC2-Support group.

![14](https://github.com/user-attachments/assets/8d5077f2-8ada-4131-9fdc-fd52a6ba140c)

## Add user-3 to the EC2-Admin group
You have hired user-3 as your Amazon EC2 administrator to manage your EC2 instances.

Using the previous steps in this task, add user-3 to the EC2-Admin group.

user-3 should now be part of the EC2-Admin group.
![15](https://github.com/user-attachments/assets/89d02cbe-38bd-42d1-b31d-0848ec895415)

In the left navigation pane, choose User groups.

Each group should have a 1 in the Users column for the number of users in each group.

If there is not a 1 beside each group, revisit the previous instructions in this task to confirm that each user is assigned to a group as shown in the table at the beginning of the Business scenario section.

## Task 4: Sign in and test user permissions
In this task, you test the permissions of each IAM user.

In the left navigation pane, choose Dashboard.
![16](https://github.com/user-attachments/assets/0b1fc1aa-07d9-41da-b6bd-56028b8a314e)


The AWS Account section includes a Sign-in URL for IAM users in this account. This link should look similar to the following: https://123456789012.signin.aws.amazon.com/console

You can use this link to sign in to the AWS account that you are currently using.

Copy the Sign-in URL for IAM users in this account to a text editor.

Open a private window using the following instructions for your web browser:

![17](https://github.com/user-attachments/assets/fa135ed6-7da4-4b49-a865-cb693cc3b147)

Mozilla Firefox

Choose the menu bars  at the upper-right of the screen.
Choose New Private Window.
Google Chrome

Choose the ellipsis  at the upper-right of the screen.
Choose New Incognito window.
Microsoft Edge

Choose the ellipsis  at the upper-right of the screen.
Choose New InPrivate window.
Microsoft Internet Explorer

Choose the Tools menu option.
Choose InPrivate Browsing.
Paste the Sign-in URL for IAM users in this account into your private window, and press Enter.

You now sign in as user-1, who has been hired as your Amazon S3 storage support staff.

Sign in using the following credentials:

IAM user name: Enter user-1
Password: Enter Lab-Password1
Choose Sign in.

If you see a dialog prompting you to switch to the new console home, choose Switch to the new Console Home.
![18](https://github.com/user-attachments/assets/bd07973d-30fa-47b1-9a8e-564e2e2a6dfe)

From the Services menu, choose S3.

Choose the name of one of your buckets, and browse the contents.

Because your user is part of the S3-Support group in IAM, they have permission to view a list of S3 buckets and their contents.
![19](https://github.com/user-attachments/assets/f7172ffc-2d7f-412f-b08e-2fc66a45a8cf)

Now, test whether they have access to Amazon EC2.

From the Services menu, choose EC2.

In the left navigation pane, choose Instances.

You cannot see any instances. Instead, you see a message that says, You are not authorized to perform this operation. This message appears because your user has not been assigned any permissions to use Amazon EC2.
![20](https://github.com/user-attachments/assets/b1b4eb5f-c13c-4337-84a8-0da6c6f3594b)

You now sign in as user-2, who has been hired as your Amazon EC2 support person.

Paste the Sign-in URL for IAM users in this account into your private window, and press Enter.

This link should be in your text editor.

Sign in using the following credentials:

IAM user name: Enter user-2
Password: Enter Lab-Password2
Choose Sign in.

If you see a dialog prompting you to switch to the new console home, choose Switch to the new Console Home.

From the Services menu, choose EC2.

In the left navigation pane, choose Instances.

You are now able to see an EC2 instance because you have read-only permissions. However, you are not be able to make any changes to Amazon EC2 resources.

 If you cannot see an EC2 instance, then your Region may be incorrect. In the upper-right of the screen, choose the Region menu, and select the Region that you noted at the start of the lab (for example, Oregon).


Sign user-1 out of the AWS Management Console by following these steps:

At the top of the screen, choose user-1.
Choose Sign out.

Your EC2 instance should be selected. If it is not, choose it.

From the Instance state dropdown list, choose Stop instance.

In the Stop instance? window, choose Stop.

You receive an error that says, Failed to stop the instance. You are not authorized to perform this operation. This message demonstrates that the policy gives you permission to only view information and does not give you permission to make changes.
![21](https://github.com/user-attachments/assets/1f6a0320-3297-4bbd-a38d-803372963529)
At the Stop Instances window, choose Cancel.

Next, check if user-2 can access Amazon S3.

From the Services menu, choose S3.

You receive an You don't have permissions to list buckets message because user-2 does not have permission to use Amazon S3.

You now sign in as user-3, who has been hired as your Amazon EC2 administrator.
![22](https://github.com/user-attachments/assets/7cd48229-b8ea-4b0b-88ab-174ddefb9be9)

Sign user-2 out of the AWS Management Console by following these steps:

At the top of the screen, choose user-2.
Choose Sign out.

Paste the Sign-in URL for IAM users in this account into your private window, and press Enter.

If this link is not in your clipboard, retrieve it from the text editor where you pasted it earlier.

Sign in using the following credentials:

IAM user name: Enter user-3
Password: Enter Lab-Password3
Choose Sign in.

If you see a dialog prompting you to switch to the new console home, choose Switch to the new Console Home.

From the Services menu, choose EC2.

In the left navigation pane, choose Instances.
![22](https://github.com/user-attachments/assets/0d203c03-a514-455b-9f65-7915bb82ac6a)

As an EC2 administrator, you should now have permissions to stop the EC2 instance. 

Your EC2 instance should be selected. If it is not, choose  it.

 If you cannot see an EC2 instance, then your Region may be incorrect. In the upper-right of the screen, choose the Region menu, and select the Region that you noted at the start of the lab (for example, Oregon).

From the Instance state dropdown list, choose Stop instance.
![23](https://github.com/user-attachments/assets/8bf23d97-b851-4666-b2f7-3c7d235478d1)

In the Stop instance? window, choose Stop.

The instance should enter the Stopping state and will shut down.
![24](https://github.com/user-attachments/assets/28d7c7a6-ab71-4454-966c-7e1db68af588)

Close your private window.
