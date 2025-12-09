---
title: "Proposal"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Auction system built in AWS Cloud infrastructure

## Auction web system built on Amazon Web Service cloud platform

### 1. Executive Summary
The Auction system is designed by a FPTU student in Ho Chi Minh City and operates on the AWS Cloud platform. The platform utilizes AWS services to build an online auction marketplace with a user-friendly interface, easy to use and suitable for everyone.

### 2. Problem Statement
*Current Problem*
Currently, auction systems have not reached many people due to difficulties in accessibility. This project was born to bring a transparent live auction platform that is friendly and accessible to everyone.

*Solution*
The platform uses AWS CloudFront and S3 Storage combined with ReactJS to provide the web interface, with EC2 servers handling all processing tasks on the Springboot platform, Amazon S3 for storing public and private data, and AWS RDS for database storage. Combined with Amazon Rekognition and Textract to extract information and verify user information to ensure fairness. With this platform, users can register new accounts, verify identities, and participate in exciting auctions on the platform.

*Benefits and Return on Investment (ROI)*
The project brings an online auction platform that is easily accessible to everyone. Estimated monthly cost is $59.37 USD (according to AWS Pricing Calculator). No additional development costs incurred.

### 3. Solution Architecture
The platform applies AWS architecture for data management. Public data is stored in public S3 buckets and displayed to users via CloudFront and S3 with ReactJS. All processing operations are performed on EC2 with the Springboot platform. Identity information is processed by Amazon Rekognition and Textract and then stored in private S3 buckets.

![Auction System Architecture](/static/images/2-Proposal/auction-system-architecture.png)

*AWS Services Used*
- *AWS VPC*: Create a private virtual network environment.
- *AWS Route 53*: Route user traffic.
- *AWS CloudFront*: CDN helps accelerate page loading speed, reduce web access latency.
- *AWS Load Balancing*: Receive requests from the internet and route to EC2, stabilizing the application.
- *Amazon EC2*: Run springboot application to handle backend processing, communicate with database (RDS), cache queries (ElastiCache), call AI services (Rekognition, Textract) and process auctions.
- *Amazon S3*:
  1. Hosting Frontend: Store frontend source code (ReactJS, Tailwind) for CloudFront distribution.
  2. Data storage: 2 buckets (public/private) to store images uploaded by users for auctions and account verification.
- *Amazon ElastiCache*: Cache memory, helping store queries to reduce load for database and accelerate API response speed.
- *Amazon RDS*: Store main system data, placed in private subnet.
- *Amazon Rekognition*: AI image analysis service, performing Face Compare between selfie photos and ID photos to verify identity (eKYC).
- *Amazon Textract*: Text extraction service from documents. The system uses Textract to automatically read (OCR) and extract information from ID photos to automatically fill for users.
- *Amazon SES*: Backend uses this service to send account verification emails (OTP), auction winning notifications or other system notifications to users.
- *Amazon CloudWatch*: Service for monitoring and log management.


*Component Design*
- *Data Ingestion*: Data from users.
- *Data Storage*: Data stored in 2 S3 buckets (1 for public and 1 for private - accessed via presigned url)
- *Data Processing*: EC2 performs data processing.
- *Web Interface*: Amazon S3 stores ReactJS application.


### 4. Technical Implementation
*Implementation Stages*
The project includes the following stages:
1. *Research and Architecture Design*: Research and design AWS architecture, identify services to be used, design database.
2. *Cost Calculation and Feasibility Check*: Use AWS Pricing Calculator to estimate and adjust.
3. *Development, Testing, Deployment*: Program Springboot and ReactJS application, then test in local environment.
4. *Deployment on AWS Cloud Environment*: Set up Gitlab CI, set up cloud environment and deploy.

*Technical Requirements*
- Java 21 Springboot
- AWS SDK (S3, Rekognition, Textract, SES)
- MySQL RDS
- ReactJS/Vite/TypeScript/Tailwind
- Gitlab, Gitlab runner CI
- Postman, CloudWatch

### 5. Roadmap & Implementation Milestones
- *Pre-internship (Month 0)*: 1 month for planning and evaluating the old station.
- *Internship (Month 1–3)*:
    - Month 1: Learn AWS and design architecture, design database, implement API construction.
    - Month 2: Implement API construction, build interface.
    - Month 3: Deploy on cloud environment, test, put into use.

### 6. Budget Estimate
Costs can be viewed on [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=05741eefd9e403091e36a896361a601881ad0aa9)

*Infrastructure Costs*
- Amazon Route53: $0.5/month (1 hosted zone)
- S3 Standard: $0.72/month (10 GB, 30000 request GET, 1000 request PUT, 5 GB Transfer out)
- Application Load Balancer: $18.80/month (data process 50GB)
- Amazon EC2 (t3.medium): $16.35/month (3yr, no upfront)
- Amazon ElastiCache (cache.t3.micro): $9.49/month (3yr, no upfront)
- Amazon RDS: $8.38/month
- Rekognition: $0.13/month (100 FaceCompare)
- Textract: $5/month (200 Pages document)

*Total*: $59.37/month.


### 7. Risk Assessment
*Risk Matrix*
- Network Loss: High impact, low probability.
- Budget Overrun: Medium impact, low probability.

*Mitigation Strategy*
- Cost: AWS budget alerts, service optimization.

*Contingency Plan*
- Periodic backups in case of incidents.
- Use CloudFormation to restore cost-related configurations.

### 8. Expected Results
*Long-term Value*: Can be reused for other projects in the future.

More information at ![Proposal Template](/static/Proposal-Template.docx)