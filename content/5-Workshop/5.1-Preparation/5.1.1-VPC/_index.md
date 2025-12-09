---
title: "Create VPC"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.1.1 </b> "
---

# Initialize Virtual Private Cloud (VPC)

The system will run inside a Virtual Private Cloud (VPC) to ensure security and resource isolation. We will create a VPC with Public Subnets (for Load Balancers) and Private Subnets (for EC2, RDS).

## Steps

1. Access the **AWS Console** and search for the **VPC** service.
2. Select **Create VPC**.
3. Choose **VPC and more** configuration to quickly create a VPC along with subnets and Route Tables.
4. Fill in the information:
    - **Name tag**: `Auction-VPC`
    - **IPv4 CIDR block**: `10.0.0.0/16`
    - **Number of Availability Zones (AZs)**: `2` (to ensure high availability)
    - **Number of public subnets**: `2`
    - **Number of private subnets**: `2`
    - **NAT gateways**: `None` (or `1 per AZ` if EC2 in private subnet needs internet access to download packages, but to save costs in this lab, you can choose None or 1).
5. Click **Create VPC**.

![Create VPC](/static/images/project/vpc/vpc_create.png)

6. Wait for the initialization process to complete.
