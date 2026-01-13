# aws-vpc-alb-ec2-webapp

# AWS Application Load Balancer with EC2 Web Application

## 📌 Project Overview
This project demonstrates deploying a simple web application on **AWS EC2 instances** and exposing it to the internet using an **Application Load Balancer (ALB)**.  
It focuses on understanding **load balancing, health checks, security groups, and application availability**.

The application is a basic HTML page served using Python’s built-in HTTP server running on **port 8000**.

---

## 🏗️ Architecture Diagram
![Architecture](architecture/architecture-diagram.png)

**Architecture Components:**
- Amazon VPC
- Public Subnets
- Application Load Balancer (ALB)
- Target Group
- EC2 Instances (Ubuntu)
- Security Groups

---

## 🧱 Architecture Details

- **Client** accesses the application using the ALB DNS name
- **ALB** listens on port **80**
- **Target Group** forwards traffic to EC2 instances on port **8000**
- **Health Check Path:** `/`
- **Protocol:** HTTP

---

## 🖥️ Application Details

- **Application Type:** Static HTML Web Page
- **Server:** Python HTTP Server
- **Command Used:**
  ```bash
  python3 -m http.server 8000
| Type       | Protocol | Port | Source             |
| ---------- | -------- | ---- | ------------------ |
| SSH        | TCP      | 22   | My IP              |
| Custom TCP | TCP      | 8000 | ALB Security Group |


🚀 Implementation Steps
1️⃣ Create EC2 Instances

Launched Ubuntu EC2 instances

Placed in public subnet

Assigned correct security group

2️⃣ Deploy Application on EC2

SSH into each EC2 instance and run:

sudo apt update
sudo apt install -y python3
cd /home/ubuntu
python3 -m http.server 8000

3️⃣ Create Target Group

Target Type: Instance

Protocol: HTTP

Port: 8000

Health Check Path: /

4️⃣ Create Application Load Balancer

Type: Application Load Balancer

Listener: HTTP : 80

Forward traffic to the created target group

5️⃣ Health Check Verification

One instance initially appeared Unhealthy

Root Cause:

Application was not running on that EC2 instance

Resolution:

Logged into the instance

Started the Python HTTP server

Result:

Instance transitioned to Healthy

🧠 Key Learning Outcomes

Open ports alone are not sufficient — applications must be running

ALB health checks validate actual application responses

Each EC2 behind ALB must serve traffic independently

Importance of automation using user data for scalability

Clear understanding of ALB vs Target Group roles
