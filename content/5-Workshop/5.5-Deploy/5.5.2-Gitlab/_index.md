---
title: "GitLab CI"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.5.2 </b> "
---

# Configure GitLab CI

## Steps

### 1. Prepare Variables
Go to **Settings** -> **CI/CD** -> **Variables** on the GitLab Repository.
Add necessary variables:
- `EC2_IP`
- `SSH_PRIVATE_KEY`

![GitLab CI 1](/static/images/project/gitlab%20ci/gitlab%20ci-1.png)
![GitLab CI 2](/static/images/project/gitlab%20ci/gitlab%20ci%20-%202.png)

### 2. Configuration file .gitlab-ci.yml
Create a `.gitlab-ci.yml` file at the root of the project.
The workflow includes:
- **Build**: Build JAR file (Spring Boot) or Docker Image.
- **Deploy**: Copy file to EC2 and restart service.


Example of a successful pipeline:
![Success](/static/images/project/gitlab%20ci/success.png)
