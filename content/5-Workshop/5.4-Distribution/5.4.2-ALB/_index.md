---
title: "Application Load Balancer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---

# Application Load Balancer (ALB)

ALB will distribute traffic to EC2 instances and handle SSL termination.

## Steps

### 1. Create Security Group for ALB
Allow HTTP (80) and HTTPS (443) from 0.0.0.0/0.
![ALB SG](/static/images/project/alb/alb-sg.png)

### 2. Create Target Group
1. Create a Target Group of type **Instances**.
2. Protocol HTTP/8080 (Backend port).
3. Register EC2 instances into the Target Group.

### 3. Create Load Balancer
1. Go to **Load Balancers** -> **Create load balancer**.
2. Select **Application Load Balancer**.
3. Select VPC and **Public Subnets**.
4. Select the created Security Group.
5. Configure Listeners:
    - HTTP:80 -> Redirect to HTTPS (recommended).
    - HTTPS:443 -> Forward to Target Group.
6. In the HTTPS listener section, select the created ACM Certificate.
![SSL ABL 1](/static/images/project/alb/ssl-alb-1.png)
![SSL ABL 2](/static/images/project/alb/ssl-alb-2.png)
![SSL ABL 3](/static/images/project/alb/ssl-alb-3.png)

7. Click **Create load balancer**.

After creating the Load Balancer, you can reconfigure the security group for the EC2 instance to only accept inbound rules from the Load Balancer.
![Edit EC2 SG](/static/images/project/ec2/edit-ec2-sg.png)
