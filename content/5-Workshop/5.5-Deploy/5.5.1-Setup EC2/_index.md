---
title: "Setup EC2 Instance Environment"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.5.1 </b> "
---

# Environment Setup for EC2 Server

In this section, we will assign an IAM Role to the EC2 instance and install necessary software such as Java and MariaDB to prepare for application deployment.

## 1. Assign IAM role to EC2

To allow the EC2 instance to access other AWS services (e.g., Session Manager for connection without opening SSH ports, or accessing S3, RDS), we need to assign an appropriate IAM Role.

1.  Access **EC2 Dashboard**, select the Instance you just created.
2.  Select **Actions** -> **Security** -> **Modify IAM role**.

![Modify IAM Role](/static/images/project/ec2/iam%20role/iam-1.png)

3.  Select the IAM Role created in previous steps (e.g., `EC2RoleForSSM`) and click **Update IAM role**.

![Select IAM Role](/static/images/project/ec2/iam%20role/iam-2.png)

## 2. Environment Setup

Connect to the EC2 Instance (using Session Manager or SSH). Then perform the following steps sequentially:

### 2.1. Update System

Run the following command to update to the latest software packages:

```
sudo dnf update -y
```

![Update System](/static/images/project/ec2/ssh/update-system.png)

### 2.2. Install Java

Our application runs on the Java platform, so installing the Java Development Kit (JDK) is required. Here we use Amazon Corretto 21 (headless version is more suitable for command-line interfaces without graphics).

```
sudo dnf install java-21-amazon-corretto-headless -y
```
![Install Java](/static/images/project/ec2/ssh/install-java.png)

Check Java version after installation:

```
java -version
```


![Check Install](/static/images/project/ec2/ssh/check-install.png)

### 2.3. Install MariaDB Client and Initialize Database

Install MariaDB client to connect and interact with RDS.

```
sudo dnf install mariadb105 -y
```

![Install MariaDB](/static/images/project/ec2/ssh/install-maria-db.png)

Connect to the created RDS database instance. Replace `<rds-endpoint>`, `<username>` with your actual information:

```
mysql -h <rds-endpoint> -u <username> -p
```

After successfully entering the password, create the database for the application:

```sql
CREATE DATABASE tickets;
SHOW DATABASES;
```

![Create Database RDS](/static/images/project/ec2/ssh/create-database-rds.png)

### 2.4. Setup Service for Auto-starting Java Springboot Application

Run the following command to create a service file

```
sudo nano /etc/systemd/system/<service-name>.service
```

![Create service](/static/images/project/ec2/ssh/create-service-file.png)

Enter the service file content, configure environment variables for the application

![Setup env](/static/images/project/ec2/ssh/env-setup.png)

Use key combination Ctrl + O, Enter and Ctrl + X to save and exit.

Use the following commands to apply changes

```text
sudo systemctl daemon-reload

sudo systemctl restart <service-name>
```

Check status using command `status`
![Check status](/static/images/project/ec2/ssh/check-status-service.png)

Use command `enable` so the service automatically runs every time the EC2 instance starts
```text
sudo systemctl enable <service-name>
```

Command to set timezone to synchronize (in case Java application needs to match Vietnam time)
```text
sudo timedatectl set-timezone Asia/Ho_Chi_Minh
```

Check result with command
```text
date
```
