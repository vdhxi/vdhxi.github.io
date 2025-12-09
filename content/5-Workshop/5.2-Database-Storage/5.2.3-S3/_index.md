---
title: "Amazon S3"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.2.3 </b> "
---

# Initialize Amazon S3 Buckets

We need 3 buckets for different purposes.

### 1. Frontend Bucket
Used for static web hosting (ReactJS).
1. Create a bucket with a unique name.
2. Uncheck **Block all public access** (as the web needs to be public).
![S3 FE 1](/static/images/project/s3/s3_fe_1.png)
3. Enable **Static website hosting**.
![S3 FE 2](/static/images/project/s3/s3_fe_2.png)

### 2. Public Storage Bucket
Stores auction product images (public read).
1. Create a bucket.
2. Uncheck **Block all public access**.
![S3 Public 1](/static/images/project/s3/s3_public_1.png)
3. Configure Bucket Policy to allow `s3:GetObject`.
![S3 Public 2](/static/images/project/s3/s3_public_2.png)

### 3. Private Storage Bucket
Stores identity documents for account verification (private).
1. Create a bucket.
2. Keep **Block all public access** checked.
![S3 Private 1](/static/images/project/s3/s3_private_1.png)
3. (Optional) Configure Server-side encryption.
![S3 Private 2](/static/images/project/s3/s3_private_2.png)
