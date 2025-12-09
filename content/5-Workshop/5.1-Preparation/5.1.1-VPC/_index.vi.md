---
title: "Tạo VPC"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1.1 </b> "
---

# Khởi tạo Virtual Private Cloud (VPC)

Hệ thống sẽ chạy bên trong một mạng riêng ảo (VPC) để đảm bảo bảo mật và cô lập tài nguyên. Chúng ta sẽ tạo VPC với các Public Subnet (cho Load Balancer) và Private Subnet (cho EC2, RDS).

## Các bước thực hiện

1. Truy cập vào **AWS Console** và tìm kiếm dịch vụ **VPC**.
2. Chọn **Create VPC**.
3. Chọn cấu hình **VPC and more** để tạo nhanh VPC cùng các subnet và Route Table.
4. Điền các thông tin:
    - **Name tag**: `Auction-VPC`
    - **IPv4 CIDR block**: `10.0.0.0/16`
    - **Number of Availability Zones (AZs)**: `2` (để đảm bảo tính sẵn sàng cao)
    - **Number of public subnets**: `2`
    - **Number of private subnets**: `2`
    - **NAT gateways**: `None` (hoặc `1 per AZ` nếu cần EC2 trong private subnet truy cập internet để tải package, nhưng để tiết kiệm chi phí trong bài lab này có thể chọn None hoặc 1). 
5. Nhấn **Create VPC**.

![Create VPC](/static/images/project/vpc/vpc_create.png)

6. Đợi quá trình khởi tạo hoàn tất.
