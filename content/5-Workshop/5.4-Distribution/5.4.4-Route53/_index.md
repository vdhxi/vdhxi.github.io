---
title: "Amazon Route 53"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 5.4.4 </b> "
---

# Amazon Route 53

Configure DNS to point domain to CloudFront (Frontend) and ALB (Backend).

## Steps

1. Access **Route 53** -> **Hosted zones**.
![R53 1](/static/images/project/route53/route_53_1.png)
2. Select your domain.
![R53 2](/static/images/project/route53/route_53_2.png)
3. Route53 will provide 4 NS records, configure them at your domain registrar to manage the domain in Route53. This process takes a few minutes.
![R53 3](/static/images/project/route53/route_53_3.png)
![R53 4](/static/images/project/route53/route_53_4.png)


### 1. Point to Backend (ALB)
3. **Create record**.
4. Record name: `api` (e.g., `api.example.com`).
5. Record type: **A**.
6. Enable **Alias**.
7. Route traffic to: **Alias to Application and Classic Load Balancer**.
8. Select Region and your ALB.
![Route to ALB](/static/images/project/route53/route-to-alb.png)



### 2. Point to Frontend (CloudFront)
3. **Create record**.
4. Record name: `www` or leave blank (root domain).
5. Record type: **A**.
6. Enable **Alias**.
7. Route traffic to: **Alias to CloudFront distribution**.
8. Select CloudFront distribution.
9. ![Route to CF](/static/images/project/route53/route-to-cf.png)
