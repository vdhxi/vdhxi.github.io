---
title: "Amazon RDS"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Khởi tạo Amazon RDS (MySQL)

Chúng ta sẽ sử dụng Amazon RDS MySQL để lưu trữ dữ liệu chính của hệ thống.

## Các bước thực hiện

### 1. Tạo Security Group cho RDS
Trước tiên, cần tạo Security Group cho phép kết nối cổng 3306 từ EC2.
![RDS SG](/images/project/rds/rds_sg.png)

### 2. Tạo Subnet Group
1. Vào **RDS Dashboard** -> **Subnet groups** -> **Create DB subnet group**.
2. Chọn VPC và các Private Subnet đã tạo.
![RDS Subnet Group](/images/project/rds/db_subnet_group.png)

### 3. Tạo Database
1. Chọn **Databases** -> **Create database**.
2. Chọn **Standard create** -> **MySQL**.
3. Chọn phiên bản (Engine Version).
![RDS Create 1](/images/project/rds/rds_create_1.png)

4. Chọn **Free tier** (nếu dùng tài khoản mới) hoặc **Dev/Test**.
![RDS Create 2](/images/project/rds/rds_create_2.png)

5. Đặt tên DB instance identifier, Master username và password.
![RDS Create 3](/images/project/rds/rds_create_3.png)

6. Chọn Instance class (ví dụ `db.t3.micro`).
7. Cấu hình Storage.
![RDS Create 4](/images/project/rds/rds_create_4.png)

8. Cấu hình Connectivity: Chọn VPC, Subnet Group, và Security Group đã tạo.
![RDS Create 5](/images/project/rds/rds_create_5.png)


![RDS Create 6](/images/project/rds/rds_create_6.png)

9. Cấu hình xác thực (Password authentication).
![RDS Create 7](/images/project/rds/rds_create_7.png)

10. Nhấn **Create database**.
![RDS Create 8](/images/project/rds/rds_create_8.png)
