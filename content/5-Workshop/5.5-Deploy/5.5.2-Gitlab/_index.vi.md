---
title: "GitLab CI"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.5.2 </b> "
---

# Cấu hình GitLab CI

## Các bước thực hiện

### 1. Chuẩn bị biến môi trường (Variables)
Vào **Settings** -> **CI/CD** -> **Variables** trên GitLab Repository.
Thêm các biến cần thiết:
- `EC2_IP`
- `SSH_PRIVATE_KEY`

![GitLab CI 1](/images/project/gitlab%20ci/gitlab%20ci-1.png)
![GitLab CI 2](/images/project/gitlab%20ci/gitlab%20ci%20-%202.png)

### 2. File cấu hình .gitlab-ci.yml
Tạo file `.gitlab-ci.yml` tại thư mục gốc của dự án.
Quy trình gồm:
- **Build**: Build file JAR (Spring Boot) hoặc Docker Image.
- **Deploy**: Copy file lên EC2 và restart service.


Ví dụ pipeline thành công:
![Success](/images/project/gitlab%20ci/success.png)

