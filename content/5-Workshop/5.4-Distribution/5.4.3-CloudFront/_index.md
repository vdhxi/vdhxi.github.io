---
title: "Amazon CloudFront"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 5.4.3 </b> "
---

# Amazon CloudFront

CloudFront helps distribute static content from S3 with low latency.

## Steps

1. Access **CloudFront Console** -> **Create distribution**.
2. In **Origin domain**, select the Frontend S3 Bucket.
![CF 1](/static/images/project/cloudFront/cf-create-1.png)

3. In **Origin access**, select **Legacy access identities** or **OAC** (Origin Access Control) to restrict direct user access to S3. Select **Create new OAC**.
4. **Viewer protocol policy**: Redirect HTTP to HTTPS.
5. **Allowed HTTP methods**: GET, HEAD, OPTIONS.
6. **WAF**: Do not enable (to save costs).
![CF 2](/static/images/project/cloudFront/cf-create-2.png)

7. **Alternate domain name (CNAME)**: Enter frontend domain (e.g., `www.example.com`).
8. **Custom SSL certificate**: Select ACM certificate.
![SSL CF](/static/images/project/cloudFront/ssl-cf.png)

9. **Default root object**: `index.html`.
![CF 3](/static/images/project/cloudFront/cf-create-3.png)

10. Click **Create distribution**.
11. After creation, remember to update the **Bucket Policy** of S3 to allow OAC access (Console will suggest copying the policy).
