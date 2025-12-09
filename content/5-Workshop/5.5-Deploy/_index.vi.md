---
title: "CI/CD"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

# Tích hợp và Triển khai liên tục (CI/CD)

Sử dụng GitLab CI để tự động hóa quy trình build và deploy ứng dụng lên AWS.

## Nội dung
1. SSH vào EC2 instance để cài đặt những ứng dụng cần thiết
2. **GitLab Runner**: Cấu hình runner trên EC2 (hoặc dùng Shared Runner).
3. **Pipeline**: Định nghĩa file `.gitlab-ci.yml`.
