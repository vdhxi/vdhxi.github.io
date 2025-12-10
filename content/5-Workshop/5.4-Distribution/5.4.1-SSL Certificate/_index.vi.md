---
title: "Certificate Manager"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

# AWS Certificate Manager (ACM)

Để sử dụng HTTPS, chúng ta cần chứng chỉ SSL.

## Các bước thực hiện

1. Truy cập **ACM Console**.
2. Chọn **Request a certificate**.
3. Chọn **Request a public certificate**.
![Cert 1](/images/project/certificate/cert-1.png)

4. Nhập Domain name (ví dụ `*.example.com`).
![Cert 2](/images/project/certificate/cert-2.png)

5. Chọn **DNS validation**.
6. Nhấn **Request**.
7. Sau khi request, nhấn vào ID của chứng chỉ, chọn **Create records in Route 53** để xác thực tự động.
![Cert 3](/images/project/certificate/cert-3.png)
![Cert 4](/images/project/certificate/cert-4.png)
8. Đợi trạng thái chuyên sang **Issued**.
