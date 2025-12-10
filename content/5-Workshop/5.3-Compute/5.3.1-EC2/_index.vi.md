---
title: "Amazon EC2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

# Khởi tạo EC2 Instance

## Các bước thực hiện

### 1. Tạo Security Group
Tạo SG cho phép HTTP (80), HTTPS (443), SSH (22) và Custom TCP (8080 - port của Spring Boot).
![EC2 SG](/images/project/ec2/ec2-sg.png)

### 2. Launch Instance
1. Truy cập **EC2 Dashboard** -> **Launch Instances**.
2. Đặt tên: `Auction-Backend`.
3. Chọn OS: **Amazon Linux 2023** hoặc **Ubuntu**.
![EC2 Setup 1](/images/project/ec2/ec2_setup_1.png)

4. Chọn Instance Type: `t3.medium` (như đề xuất).
5. Chọn Key Pair (tạo mới nếu chưa có).
6. Network settings: Chọn VPC, Public Subnet, và Security Group đã tạo.
![EC2 Setup 2](/images/project/ec2/ec2_setup_2.png)

7. Configure storage (mặc định 8GB hoặc tăng lên nếu cần).
8. Advanced details:
    - **IAM instance profile**: Chọn `Auction-EC2-Role`.
![EC2 Setup 3](/images/project/ec2/ec2_setup_3.png)

9. Nhấn **Launch instance**.

### 3. Gán Elastic IP (Tùy chọn)
Nếu bạn muốn IP Public cố định.
1. Vào **Elastic IPs** -> **Allocate Elastic IP address**.
![EIP 1](/images/project/ec2/elastic_ip.png)
2. Chọn IP vừa tạo -> **Associate Elastic IP address**.
![EIP 2](/images/project/ec2/elastic_ip_2.png)
3. Chọn Instance vừa tạo.
![EIP 3](/images/project/ec2/elastic_ip_3.png)
