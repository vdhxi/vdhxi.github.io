---
title: "Triển khai hệ thống"
date: "`r Sys.Date()`"
weight: 5
chapter: true
pre: " <b> 5. </b> "
---

# Triển khai hệ thống Auction trên AWS

Chào mừng bạn đến với workshop triển khai hệ thống đấu giá trực tuyến trên nền tảng AWS. Trong workshop này, chúng ta sẽ cùng nhau xây dựng từng thành phần của hệ thống dựa trên kiến trúc đã đề xuất.

## Mục tiêu
Hoàn thành việc cài đặt và cấu hình các dịch vụ AWS cần thiết để vận hành hệ thống Auction System.

## Kiến trúc
Chúng ta sẽ bám sát kiến trúc sau:

![Auction System Architecture](/static/images/2-Proposal/auction-system-architecture.png)

## Các bước thực hiện
1. **Chuẩn bị (Preparation)**: Thiết lập VPC, IAM Role.
2. **Cơ sở dữ liệu & Lưu trữ (Database & Storage)**: Cấu hình RDS, ElastiCache, S3.
3. **Tính toán (Compute)**: Cài đặt và cấu hình EC2.
4. **Phân phối (Distribution)**: Cấu hình Load Balancer, CloudFront, Route 53.
5. **CI/CD**: Thiết lập quy trình triển khai tự động với GitLab CI.
6. **Dọn dẹp (Clean up)**: Xóa tài nguyên sau khi hoàn thành.
