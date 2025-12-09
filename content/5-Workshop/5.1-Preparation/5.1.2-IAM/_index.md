---
title: "Create IAM Role"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.1.2 </b> "
---

# Create IAM Role for EC2

EC2 needs access to S3 to retrieve code/images, and permissions to call Rekognition and Textract APIs. Instead of storing Access Keys in the code, we will use an IAM Role attached to the EC2 instance.

## Steps

1. Access **IAM Dashboard**.
2. Select **Roles** -> **Create role**.
3. In the **Trusted entity type** step, select **AWS service**.
4. In **Use case**, select **EC2**.
5. Click **Next**.

![IAM Step 1](/static/images/project/iam/iam-1.png)

6. In the **Add permissions** step, search and select the following Policies:
    - `AmazonS3FullAccess` (Or a policy limited to the project bucket only).
    - `AmazonRekognitionFullAccess`.
    - `AmazonTextractFullAccess`.
    - `AmazonSSMManagedInstanceCore` (To remote into EC2 via Session Manager if needed).
7. Click **Next**.
8. Name the Role `Auction-EC2-Role`.
9. Review and click **Create role**.

![IAM Step 2](/static/images/project/iam/iam-2.png)
