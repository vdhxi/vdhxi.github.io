---
title: "Amazon RDS"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.2.1 </b> "
---

# Initialize Amazon RDS (MySQL)

We will use Amazon RDS MySQL to store the main data of the system.

## Steps

### 1. Create Security Group for RDS
First, we need to create a Security Group allowing connection on port 3306 from EC2.
![RDS SG](/static/images/project/rds/rds_sg.png)

### 2. Create Subnet Group
1. Go to **RDS Dashboard** -> **Subnet groups** -> **Create DB subnet group**.
2. Select the VPC and the created Private Subnets.
![RDS Subnet Group](/static/images/project/rds/db_subnet_group.png)

### 3. Create Database
1. Select **Databases** -> **Create database**.
2. Select **Standard create** -> **MySQL**.
3. Select version (Engine Version).
![RDS Create 1](/static/images/project/rds/rds_create_1.png)

4. Select **Free tier** (if using a new account) or **Dev/Test**.
![RDS Create 2](/static/images/project/rds/rds_create_2.png)

5. Set **DB instance identifier**, **Master username** and **password**.
![RDS Create 3](/static/images/project/rds/rds_create_3.png)

6. Select **Instance class** (e.g., `db.t3.micro`).
7. Configure **Storage**.
![RDS Create 4](/static/images/project/rds/rds_create_4.png)

8. Configure **Connectivity**: Select VPC, Subnet Group, and the created Security Group.
![RDS Create 5](/static/images/project/rds/rds_create_5.png)


![RDS Create 6](/static/images/project/rds/rds_create_6.png)

9. Configure authentication (**Password authentication**).
![RDS Create 7](/static/images/project/rds/rds_create_7.png)

10. Click **Create database**.
![RDS Create 8](/static/images/project/rds/rds_create_8.png)
