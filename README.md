**CI/CD Pipeline on AWS (GitHub → CodePipeline → CodeDeploy → EC2)**

📌 **Project Overview**

This project demonstrates how to implement a Continuous Integration and Continuous Deployment (CI/CD) pipeline using AWS services. The pipeline automatically deploys a web application to an Amazon EC2 instance whenever changes are pushed to a GitHub repository.
The goal was to eliminate manual deployments and implement an automated, production-style workflow.

🏗️ Architecture

<img width="714" height="462" alt="Architecture" src="https://github.com/user-attachments/assets/a18bc00b-5ebd-4956-b7de-5a9866a04fdf" />

 **Step 1: Launch EC2 Instance**
 
 *Launched Amazon Linux 2 EC2 instance and allowed port HTTP nas SSH in security group.*
 <img width="777" height="300" alt="launch instance" src="https://github.com/user-attachments/assets/012d0dc5-f3a0-4baa-8573-7a2bbd748bcd" />
 
**Step 2: Install Apache Web Server**

*Installed Apache Web server and codedeploy agent on the newly created EC2 Instance and tested using http://EC2-Public-IP*

•	sudo yum update -y

•	sudo yum install httpd -y

•	sudo systemctl start httpd

•	sudo systemctl enable httpd


 <img width="723" height="397" alt="Apache" src="https://github.com/user-attachments/assets/ed972a67-c721-4117-a426-47e1cd77896d" />

<img width="723" height="436" alt="Apache1" src="https://github.com/user-attachments/assets/5134d959-ddd3-46fa-b50c-58ec85aef6e2" />

**Step 3: Install CodeDeploy Agent on EC2**
 
*Install CodeDeploy agent on EC2.*

•	sudo yum install ruby -y

•	sudo yum install wget -y

•	cd /home/ec2-user

•	wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install

•	chmod +x ./install

•	sudo ./install auto

•	sudo systemctl status codedeploy-agent


<img width="674" height="326" alt="codedeploy agent" src="https://github.com/user-attachments/assets/f546ad35-c704-4e5c-950d-6f2e94fb3003" />

 <img width="725" height="369" alt="codedeploy agent1" src="https://github.com/user-attachments/assets/21833caa-e134-49a6-98f5-9a70533a7d38" />

**Step 4: Prepare Application Files**

*Created project folder structure with index.html,appspec.yml and script folder with install_apache.sh inside:*

 <img width="724" height="330" alt="app files" src="https://github.com/user-attachments/assets/cebceb62-1974-4a81-bd0c-649c0825bef8" />


 **Step 5: Push Files to GitHub**
 
*Created new GitHub repository, upload project files, verify the structure is correct.*

<img width="733" height="405" alt="push" src="https://github.com/user-attachments/assets/e221e2af-86a9-4d2f-8cce-60387a802319" />

 
**Step 6: Create IAM Roles**

*CodeDeploy Service Role*

•	Created IAM Role

•	Trusted entity: CodeDeploy

•	Attached policy: AWSCodeDeployRole

•	Named role: CodeDeployServiceRole

 <img width="701" height="404" alt="roles1" src="https://github.com/user-attachments/assets/8372ca8e-cda4-4547-b316-f25f6c9b5647" />

🔹 EC2 Instance Role

•	Created IAM Role

•	Trusted entity: EC2

•	Attached policy: AmazonEC2RoleforAWSCodeDeploy

•	Attached role to EC2 instance

<img width="723" height="452" alt="role2" src="https://github.com/user-attachments/assets/4d87596c-4209-4753-a04b-af689cc624c6" />

 
**Step 7: Create CodeDeploy Application**

*Create CodeDeploy application and then create the deployment group*

 <img width="646" height="370" alt="deploy app" src="https://github.com/user-attachments/assets/ebe19344-157b-48fb-92ae-11c5b187bc2e" />

**Step 8: Create CodePipeline**

*Create the pipeline, source being github (via Code Connections), then add the deployment stage and the selected deployment group.*

   <img width="727" height="429" alt="pipeline" src="https://github.com/user-attachments/assets/237e1e81-807a-443e-8428-2b39f12de763" />

**Step 9: Test the Pipeline**
*Push the changes to GitHub and the CodePipeline will be triggered automatically. Website will be updated without manual intervention and it succeeded.*
 
<img width="733" height="405" alt="push" src="https://github.com/user-attachments/assets/d5b29d54-1b8a-4b73-bb51-4147101b72d8" />


**❌ Mistakes I Made and How I Fixed Them**

This section shows real troubleshooting experience.



*Mistake 1: appspec.yml.txt Instead of appspec.yml*

Problem:
Windows saved file as .txt, so CodeDeploy ignored it.

Fix:

Enabled "File name extensions" in Windows and renamed file correctly to:
appspec.yml



*Mistake 2: CodeDeploy Service Role Error (ARN must start with arn:)*

Problem:

Typed role name manually instead of selecting from dropdown.

Also initially created incorrect role type.

Fix:

•	Deleted incorrect role

•	Recreated role with:

o	Trusted entity: CodeDeploy

o	Policy: AWSCodeDeployRole

•	Selected role from dropdown (not typed)



*Mistake 3: CodePipeline Source Stage Failed*

Problem:

Pipeline could not access GitHub repository.

Cause:

GitHub connection not authorized correctly.

Fix:

•	Reconnected GitHub via CodeConnections

•	Re-authorized AWS GitHub App

•	Confirmed correct repository and branch (main)



*Mistake 4: Load Balancer Enabled by Default*

Problem:

Deployment group had load balancer enabled even though project did not use one.

Fix:

Unchecked "Enable load balancing" in deployment group settings.



*Mistake 5: CodeDeploy Agent Not Running*

Problem:

Deployment failed because agent was not running.

Fix:

•	Verified agent status: sudo systemctl status codedeploy-agent

•	Restarted service if necessary: sudo systemctl restart codedeploy-agent



🎯 Key Skills Gained

•	Implemented CI/CD pipeline on AWS

•	Integrated GitHub with AWS services

•	Configured IAM roles securely

•	Installed and managed CodeDeploy agent

•	Troubleshot deployment failures

•	Understood real DevOps automation workflow

•	Learned how production deployments are structured



Final Outcome

Successfully built a fully automated CI/CD pipeline where:

•	Code pushed to GitHub

•	CodePipeline triggers automatically

•	CodeDeploy updates EC2

•	Website updates without manual SSH access


💡 Reflection

This project strengthened my understanding of automation, permissions, cloud architecture, and troubleshooting in AWS. It demonstrated how modern teams deploy applications efficiently and reliably.



 


