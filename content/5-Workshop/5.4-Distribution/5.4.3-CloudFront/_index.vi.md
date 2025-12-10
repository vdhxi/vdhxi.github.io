---
title: "Amazon CloudFront"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.4.3 </b> "
---

# Amazon CloudFront

CloudFront giúp phân phối nội dung tĩnh từ S3 với độ trễ thấp.

## Các bước thực hiện

1. Truy cập **CloudFront Console** -> **Create distribution**.
2. Tại **Origin domain**, chọn S3 Bucket Frontend.
![CF 1](/images/project/cloudFront/cf-create-1.png)

3. Tại **Origin access**, chọn **Legacy access identities** hoặc **OAC** (Origin Access Control) để hạn chế người dùng truy cập trực tiếp S3. Chọn **Create new OAC**.
4. **Viewer protocol policy**: Redirect HTTP to HTTPS.
5. **Allowed HTTP methods**: GET, HEAD, OPTIONS.
6. **WAF**: Do not enable (để tiết kiệm).
![CF 2](/images/project/cloudFront/cf-create-2.png)

7. **Alternate domain name (CNAME)**: Điền domain frontend (ví dụ `www.example.com`).
8. **Custom SSL certificate**: Chọn chứng chỉ ACM.
![SSL CF](/images/project/cloudFront/ssl-cf.png)

9. **Default root object**: `index.html`.
![CF 3](/images/project/cloudFront/cf-create-3.png)

10. Nhấn **Create distribution**.
11. Sau khi tạo, nhớ update **Bucket Policy** của S3 để cho phép OAC truy cập (Console sẽ gợi ý copy policy).
