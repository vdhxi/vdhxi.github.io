---
title: "Amazon EC2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

# Initialize EC2 Instance

## Steps

### 1. Create Security Group
Create a Security Group allowing HTTP (80), HTTPS (443), SSH (22), and Custom TCP (8080 - Spring Boot port).
![EC2 SG](/static/images/project/ec2/ec2-sg.png)

### 2. Launch Instance
1. Access **EC2 Dashboard** -> **Launch Instances**.
2. Name: `Auction-Backend`.
3. Select OS: **Amazon Linux 2023** or **Ubuntu**.
![EC2 Setup 1](/static/images/project/ec2/ec2_setup_1.png)

4. Select Instance Type: `t3.medium` (as proposed).
5. Select Key Pair (create new if not exists).
6. Network settings: Select VPC, Public Subnet, and the created Security Group.
![EC2 Setup 2](/static/images/project/ec2/ec2_setup_2.png)

7. Configure storage (default 8GB or increase if needed).
8. Advanced details:
    - **IAM instance profile**: Select `Auction-EC2-Role`.
![EC2 Setup 3](/static/images/project/ec2/ec2_setup_3.png)

9. Click **Launch instance**.

### 3. Assign Elastic IP (Optional)
If you want a fixed Public IP.
1. Go to **Elastic IPs** -> **Allocate Elastic IP address**.
![EIP 1](/static/images/project/ec2/elastic_ip.png)
2. Select the created IP -> **Associate Elastic IP address**.
![EIP 2](/static/images/project/ec2/elastic_ip_2.png)
3. Select the created Instance.
![EIP 3](/static/images/project/ec2/elastic_ip_3.png)
