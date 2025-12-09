---
title: "Amazon ElastiCache"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Khởi tạo Amazon ElastiCache (Redis)

Redis giúp cache các truy vấn thường xuyên và lưu session người dùng.

## Các bước thực hiện

### 1. Tạo Subnet Group
1. Vào **ElastiCache Dashboard** -> **Subnet groups** -> **Create subnet group**.
![Redis Subnet](/static/images/project/redis/redis-subnet.png)

### 2. Tạo Security Group
Tạo Security Group cho phép cổng 6379 từ EC2.
![Redis SG](/static/images/project/redis/redis-sg.png)

### 3. Tạo Redis Cluster
1. Chọn **Redis OSS caches** -> **Create cache**.
2. Chọn **Configure and create a new cluster**.
3. Chọn **Cluster mode disabled** (để đơn giản và tiết kiệm chi phí).
![Redis Create 1](/static/images/project/redis/redis-create-1.png)

4. Cấu hình Redis info
![Redis Create 2](/static/images/project/redis/redis-create-2.png)

5. Cấu hình Node type, ví dụ `cache.t3.micro`.
![Redis Create 3](/static/images/project/redis/redis-create-3.png)

6. Chọn Subnet group.
![Redis Create 4](/static/images/project/redis/redis-create-4.png)

7. Chọn Security Group.
![Redis Create 5](/static/images/project/redis/redis-create-5.png)

8. Nhấn **Create**.
