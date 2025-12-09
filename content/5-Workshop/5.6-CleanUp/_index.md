---
title: "Clean Up"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: " <b> 5.6 </b> "
---

# Clean Up Resources

To avoid unwanted costs after completing the workshop, please delete resources in the following order:

## Deletion Order
1. **EC2**: Terminate instances.
2. **RDS & ElastiCache**: Delete database and cache cluster. Delete Subnet Groups and Snapshots.
3. **Load Balancer & Target Group**: Delete ALB first, then Target Group.
4. **CloudFront**: Disable distribution, wait for deployment to finish, then Delete.
5. **S3**: Empty bucket (delete all objects) then Delete bucket.
6. **NAT Gateway & Elastic IP**: Delete NAT Gateway -> Release Elastic IP.
7. **VPC**: Delete VPC (this will automatically delete Subnets, Internet Gateway, Route Tables, and related Security Groups).

> **Note**: Check the Billing Dashboard the next day to ensure there are no incurring costs.
