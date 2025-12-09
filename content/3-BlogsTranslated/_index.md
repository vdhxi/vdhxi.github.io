---
title: "Translated Blogs"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section will list and introduce the blogs you have translated. For example:

###  [Blog 1 - Performance benefits of new Amazon EC2 R8a memory-optimized instances](3.1-Blog1/)
Amazon EC2 R8a instances, powered by 5th Generation AMD EPYC processors and higher memory bandwidth, deliver significant performance improvements for memory-optimized workloads, 
especially MySQL databases. Based on HammerDB benchmarking, R8a demonstrates substantial gains in overall score (55% higher than R7a and 74% higher than R6a), transactions per minute 
(32% higher than R7a and 63% higher than R6a), and P99 latency reduction (14% lower than R7a and 25% lower than R6a). With consistent performance enabled by the 1 vCPU = 1 physical 
core architecture and strong scalability, R8a becomes an optimal choice for database systems and memory-intensive workloads.

###  [Blog 2 - Optimize latency-sensitive workloads with Amazon EC2 detailed NVMe statistics](3.2-Blog2/)
This post explains how to use Amazon EC2 detailed performance statistics for instance store NVMe volumes to monitor latency-sensitive workloads. These new metrics offer per-second granularity for queue length, IOPS, throughput, and latency histograms (including by I/O size), helping to identify performance bottlenecks and fine-tune applications. It covers how to access these statistics via `nvme-cli` or CloudWatch and provides scenarios for troubleshooting issues like exceeding storage limits.

###  [Blog 3 - How to export to Amazon S3 Tables by using AWS Step Functions Distributed Map](3.3-Blog3/)
This article demonstrates a serverless solution for automating document processing and exporting structured data to Amazon S3 Tables using AWS Step Functions Distributed Map. It details a scalable workflow that triggers on S3 uploads, uses Distributed Map for parallel processing of files (e.g., PDFs), extracts data with Amazon Textract, and streams it via Amazon Data Firehose to S3 Tables for downstream analytics with Amazon Athena.

###  [Blog 4 - DISA STIG for Amazon Linux 2023 is now available](3.4-Blog4/)
AWS announces the availability of the Security Technical Implementation Guide (STIG) for Amazon Linux 2023 (AL2023), developed in collaboration with DISA. This guide aids DOD and federal customers in meeting strict security compliance standards (NIST 800-53). The post also discusses how to automate the implementation of these security configurations using AWS Systems Manager and EC2 Image Builder for both existing fleets and new images.

###  [Blog 5 - Architecting for AI excellence: AWS launches three Well-Architected Lenses at re:Invent 2025](3.5-Blog5/)
At re:Invent 2025, AWS introduced new and updated Well-Architected Lenses for AI: the new Responsible AI Lens, and updates to the Machine Learning (ML) Lens and Generative AI Lens. These lenses provide comprehensive best practices for ensuring AI workloads are secure, reliable, efficient, and responsible, covering the entire lifecycle from experimentation to production.

###  [Blog 6 - Announcing the updated AWS Well-Architected Generative AI Lens](3.6-Blog6/)
This post details the updates to the AWS Well-Architected Generative AI Lens. Key additions include guidance for Amazon SageMaker HyperPod, a new Responsible AI preamble covering eight core dimensions, a Data Architecture preamble, and an Agentic AI preamble. It also includes eight new architecture scenarios to help customers apply generative AI to common business problems effectively.
