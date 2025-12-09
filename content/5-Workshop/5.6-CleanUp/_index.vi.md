---
title: "Dọn dẹp tài nguyên"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Dọn dẹp tài nguyên (Clean Up)

Để tránh phát sinh chi phí không mong muốn sau khi hoàn thành workshop, hãy xóa các tài nguyên theo thứ tự sau:

## Thứ tự xóa
1. **EC2**: Terminate các instance.
2. **RDS & ElastiCache**: Delete database và cache cluster. Xóa cả Subnet Group và Snapshots.
3. **Load Balancer & Target Group**: Delete ALB sau đó đến Target Group.
4. **CloudFront**: Disable distribution, đợi deploy xong rồi Delete.
5. **S3**: Empty bucket (xóa hết object) sau đó Delete bucket.
6. **NAT Gateway & Elastic IP**: Delete NAT Gateway -> Release Elastic IP.
7. **VPC**: Delete VPC (sẽ tự động xóa Subnets, Internet Gateway, Route Table, Security Group liên quan).

> **Lưu ý**: Kiểm tra kỹ Billing Dashboard vào ngày hôm sau để chắc chắn không còn chi phí phát sinh.
