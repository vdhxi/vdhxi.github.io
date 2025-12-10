---
title: "Amazon Route 53"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 5.4.4 </b> "
---

# Amazon Route 53

Cấu hình DNS để trỏ domain về CloudFront (Frontend) và ALB (Backend).

## Các bước thực hiện

1. Truy cập **Route 53** -> **Hosted zones**.
![R53 1](/images/project/route53/route_53_1.png)
2. Chọn domain của bạn.
![R53 2](/images/project/route53/route_53_2.png)
3. Route53 sẽ cấp 4 bản ghi NS, hãy cấu hình nó tại nơi đăng kí domain của bạn để có thể quản lí domain tại Route53. Quá trình này mất khoảng vài phút
![R53 3](/images/project/route53/route_53_3.png)
![R53 4](/images/project/route53/route_53_4.png)


### 1. Trỏ về Backend (ALB)
3. **Create record**.
4. Record name: `api` (ví dụ `api.example.com`).
5. Record type: **A**.
6. Bật **Alias**.
7. Route traffic to: **Alias to Application and Classic Load Balancer**.
8. Chọn Region và ALB của bạn.
![Route to ALB](/images/project/route53/route-to-alb.png)



### 2. Trỏ về Frontend (CloudFront)
3. **Create record**.
4. Record name: `www` hoặc để trống (root domain).
5. Record type: **A**.
6. Bật **Alias**.
7. Route traffic to: **Alias to CloudFront distribution**.
8. Chọn CloudFront distribution.
9. ![Route to CF](/images/project/route53/route-to-cf.png)


