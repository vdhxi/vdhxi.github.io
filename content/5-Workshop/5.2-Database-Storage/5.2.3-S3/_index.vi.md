---
title: "Amazon S3"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Khởi tạo Amazon S3 Buckets

Chúng ta cần 3 bucket cho các mục đích khác nhau.

### 1. Frontend Bucket
Dùng để hosting static web (ReactJS).
1. Tạo bucket với tên unique.
2. Bỏ chọn **Block all public access** (vì cần public web).
![S3 FE 1](/static/images/project/s3/s3_fe_1.png)
3. Bật **Static website hosting**.
![S3 FE 2](/static/images/project/s3/s3_fe_2.png)

### 2. Public Storage Bucket
Lưu ảnh sản phẩm đấu giá (public read).
1. Tạo bucket.
2. Bỏ chọn **Block all public access**.
![S3 Public 1](/static/images/project/s3/s3_public_1.png)
3. Cấu hình Bucket Policy cho phép `s3:GetObject`.
![S3 Public 2](/static/images/project/s3/s3_public_2.png)

### 3. Private Storage Bucket
Lưu ảnh giấy tờ tùy thân cho việc xác minh tài khoản (private).
1. Tạo bucket.
2. Giữ nguyên **Block all public access**.
![S3 Private 1](/static/images/project/s3/s3_private_1.png)
3. (Tùy chọn) Cấu hình Server-side encryption.
![S3 Private 2](/static/images/project/s3/s3_private_2.png)
