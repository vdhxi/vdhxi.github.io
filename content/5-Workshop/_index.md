---
title: "System Deployment"
date: "`r Sys.Date()`"
weight: 5
chapter: true
pre: " <b> 5. </b> "
---

# Deploy Auction System on AWS

Welcome to the workshop on deploying an online auction system on the AWS platform. In this workshop, we will build each component of the system together based on the proposed architecture.

## Objectives
Complete the installation and configuration of necessary AWS services to operate the Auction System.

## Architecture
We will follow this architecture:

![Auction System Architecture](/images/2-Proposal/auction-system-architecture.png)

## Steps
1. **Preparation**: Setup VPC, IAM Role.
2. **Database & Storage**: Configure RDS, ElastiCache, S3.
3. **Compute**: Install and configure EC2.
4. **Distribution**: Configure Load Balancer, CloudFront, Route 53.
5. **CI/CD**: Setup automated deployment process with GitLab CI.
6. **Clean up**: Delete resources after completion.
