---
title: "Compute"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Khởi tạo Amazon EC2

Amazon EC2 (Elastic Compute Cloud) sẽ là nơi chạy ứng dụng backend (Spring Boot).

## Nội dung
1. **EC2 Instance**: Máy chủ ảo chạy ứng dụng.
2. **Security Group**: Tường lửa kiểm soát truy cập.
3. **Elastic IP**: Địa chỉ IP tĩnh (tùy chọn, cần thiết nếu không dùng Load Balancer hoặc cần IP cố định cho outbound).
