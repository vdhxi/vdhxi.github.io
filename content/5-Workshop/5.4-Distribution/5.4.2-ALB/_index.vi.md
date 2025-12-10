---
title: "Application Load Balancer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---

# Application Load Balancer (ALB)

ALB sẽ phân phối traffic tới các EC2 instance và xử lý SSL termination.

## Các bước thực hiện

### 1. Tạo Security Group cho ALB
Cho phép HTTP (80) và HTTPS (443) từ 0.0.0.0/0.
![ALB SG](/images/project/alb/alb-sg.png)

### 2. Tạo Target Group
1. Tạo Target Group loại **Instances**.
2. Protocol HTTP/8080 (Port backend).
3. Register EC2 instances vào Target Group.

### 3. Tạo Load Balancer
1. Vào **Load Balancers** -> **Create load balancer**.
2. Chọn **Application Load Balancer**.
3. Chọn VPC và **Public Subnets**.
4. Chọn Security Group vừa tạo.
5. Cấu hình Listener:
    - HTTP:80 -> Redirect to HTTPS (được khuyến nghị).
    - HTTPS:443 -> Forward to Target Group.
6. Tại phần HTTPS listener, chọn ACM Certificate đã tạo.
![SSL ABL 1](/images/project/alb/ssl-alb-1.png)
![SSL ABL 2](/images/project/alb/ssl-alb-2.png)
![SSL ABL 3](/images/project/alb/ssl-alb-3.png)

7. Nhấn **Create load balancer**.

Sau khi tạo Load Balancer, ta có thể cấu hình lại security group cho EC2 instance chỉ nhận inbound rule từ Load Balancer
![Edit EC2 SG](/images/project/ec2/edit-ec2-sg.png)