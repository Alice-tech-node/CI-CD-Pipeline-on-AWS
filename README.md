CI/CD Pipeline on AWS (GitHub → CodePipeline → CodeDeploy → EC2)

📌 Project Overview

This project demonstrates how to implement a Continuous Integration and Continuous Deployment (CI/CD) pipeline using AWS services. The pipeline automatically deploys a web application to an Amazon EC2 instance whenever changes are pushed to a GitHub repository.
The goal was to eliminate manual deployments and implement an automated, production-style workflow.

🏗️ Architecture

<img width="714" height="462" alt="Architecture" src="https://github.com/user-attachments/assets/a18bc00b-5ebd-4956-b7de-5a9866a04fdf" />


 
 Step 1: Launch EC2 Instance
 Launched Amazon Linux 2 EC2 instance and allowed port HTTP nas SSH in security group.
 <img width="777" height="300" alt="launch instance" src="https://github.com/user-attachments/assets/012d0dc5-f3a0-4baa-8573-7a2bbd748bcd" />

