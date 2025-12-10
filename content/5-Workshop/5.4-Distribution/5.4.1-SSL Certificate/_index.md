---
title: "Certificate Manager"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

# AWS Certificate Manager (ACM)

To use HTTPS, we need an SSL certificate.

## Steps

1. Access **ACM Console**.
2. Select **Request a certificate**.
3. Select **Request a public certificate**.
![Cert 1](/images/project/certificate/cert-1.png)

4. Enter Domain name (e.g., `*.example.com`).
![Cert 2](/images/project/certificate/cert-2.png)

5. Select **DNS validation**.
6. Click **Request**.
7. After requesting, click on the certificate ID, select **Create records in Route 53** for automatic validation.
![Cert 3](/images/project/certificate/cert-3.png)
![Cert 4](/images/project/certificate/cert-4.png)
8. Wait for status to change to **Issued**.
