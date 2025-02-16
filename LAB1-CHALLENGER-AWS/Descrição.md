##  Amazon EC2 Instances (Challenge)
 

## Lab overview
- In this challenge lab, you apply what you have learned so far about Amazon Elastic Compute Cloud (Amazon EC2). You follow some high-level steps to create a web application running on an Amazon Linux EC2 instance.

## Objectives
- After completing this challenge, you should be able to do the following:
- Configure a virtual network.
- Place an Amazon Linux EC2 instance into this virtual network.
- Install a web server, and deploy and run a simple application on it.
  
## Launch Your lab environment
- At the top of these instructions, choose Start Lab to launch the lab.
-   A Start Lab panel opens displaying the lab status.
-   Wait until the message "Lab status: ready" appears, and then choose X to close the Start Lab panel.
-   This lab creates a new AWS account for you that you use to create the resources needed to launch an EC2 instance and run a web application.
-   Next to Start Lab, choose AWS to open the AWS Management Console on a new browser tab. The system automatically signs you in.
-   Tip If a new browser tab does not open, a banner or icon at the top of your browser will indicate that your browser is preventing the site from opening pop-up windows. Choose the banner or icon, and choose Allow pop-ups.
 
## Your challenge
 - Create an Amazon Linux EC2 instance to run a web application. The general steps are as follows:
 - Use the AWS Management Console to launch the instance.
 - Use an Amazon Linux Amazon Machine Image (AMI) and a T3 instance type with a size that is smaller than medium.
 - Launch the instance in a new virtual private cloud (VPC) and a new subnet, and auto-assign the instance's public IPv4 address.
 - While you are creating your instance, in the user data, install and start the httpd service as your web server. Give write permission to users to the web server's document root directory (/var/www/html).
 - Use a General Purpose SSD (gp2) volume type for the root volume.
 - Configure the instance, and create the necessary resources so that you can connect to it by using Secure Shell (SSH).
 - Capture a screenshot of the EC2 instance's system log showing that the httpd service was successfully installed.

## To test your web server, deploy the web page in the following steps to your web server.
- Use EC2 Instance Connect to connect to your EC2 instance.
- Copy and paste the following HTML code into a text editor:       

- < !DOCTYPE html>
- < html>
- < body>
- < h1>YOUR-NAME's re/Start Project Work</h1>
- < p>EC2 Instance Challenge Lab</p>
- < /body>
- < /html>

  >>>> remove spaces in the text !!!!!
  
Replace YOUR-NAME with your name, and save the file as projects.html

- Place this file in the /var/www/html directory of your EC2 instance.
- Open a web browser, and navigate to this sample webpage. Capture a screenshot showing that the page was successfully returned and displayed.

---
## Hints
- You need to create an internet gateway and properly configure the subnet's route table in your VPC before you launch your instance.
- You need to use EC2 Instance Connect to connect over SSH to your EC2 instance by using a web browser.
- Make sure that you have the right security group settings. In particular, you should allow for SSH and HTTP traffic.
- Use the public IPv4 address of the instance to access your webpage.
- You need to elevate to sudo to copy the file to the /var/www/html/ directory.
- Refer to the following labs for additional guidance:
- Creating Amazon EC2 Instances

---

## Prints da resolução

![step1](https://github.com/user-attachments/assets/ff674b35-95ce-40af-bfae-10ef29e3055c)
![step2](https://github.com/user-attachments/assets/10f980a9-4c9b-4844-a383-aff192ee3b82)
![STEP3](https://github.com/user-attachments/assets/d504ce24-83e9-478e-8fff-ed01dbf5331f)
![STEP3 1](https://github.com/user-attachments/assets/edea0ffd-da3f-4a79-80e5-8098d30a17c8)
![STEP4](https://github.com/user-attachments/assets/ef9046b2-6b0a-49bd-92c3-41cc4770a9eb)
![STEP5](https://github.com/user-attachments/assets/cbe3e914-c3ba-4e1d-af81-598022010c54)
![STEP5 1](https://github.com/user-attachments/assets/e6b78cee-b183-418c-8705-077ecb29f7f8)
![STEP6](https://github.com/user-attachments/assets/39d75464-0136-4751-b0a5-a6f8c0f14777)
![STEP6 1](https://github.com/user-attachments/assets/073b8b70-35bb-4c21-9d71-09fd2c623dfc)
![step6 2](https://github.com/user-attachments/assets/cd7905e1-42b2-4137-a00e-f5775736daf8)
![SETP7](https://github.com/user-attachments/assets/45276b9b-ed72-4743-89bf-6bce669c2aae)
![STEP8](https://github.com/user-attachments/assets/a6954be5-4459-4df6-a2dc-54abc606f751)
![STEP9](https://github.com/user-attachments/assets/4e7f242c-365b-43d6-b0ff-f3d000610fe5)
![STEP10](https://github.com/user-attachments/assets/371edabc-8612-4801-9bbe-3d8670311d2d)
![STEP11](https://github.com/user-attachments/assets/2494b817-6864-47ab-96f5-93ab5caf513c)
![STEP12](https://github.com/user-attachments/assets/5c90619a-f5de-45eb-a2bf-aab8a4874079)
![STEP13](https://github.com/user-attachments/assets/39b04930-af6c-4f79-b9ec-6391ebd3e32b)
![STEP14](https://github.com/user-attachments/assets/56b6e29f-faaf-484d-af9f-f6b3a023d5b7)
![STEP15](https://github.com/user-attachments/assets/087a664d-98e9-4db2-8c15-d91dc4b10bfe)
![STEP16](https://github.com/user-attachments/assets/65dba41c-54b4-4371-a517-61c59083fdda)
![step17](https://github.com/user-attachments/assets/e33b90de-2961-491e-960f-05fd3d559a32)
![step18](https://github.com/user-attachments/assets/70362165-1642-463a-a225-6c705b540d53)
![step19](https://github.com/user-attachments/assets/05cfb6eb-1ff8-4510-be44-b0e299a5f669)

