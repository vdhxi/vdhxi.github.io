---
title: "Blog 1"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Performance benefits of the new memory-optimized Amazon EC2 R8a instances

We recently announced the general availability of Amazon EC2 R8a instances — the latest addition to our memory-optimized instance family powered by AMD CPUs. These instances feature 5th Generation AMD EPYC processors (code-named “Turin”) with a maximum frequency of up to 4.5 GHz. In this post, I’ll put these instances to the test and run MySQL benchmarks — but first, let’s look at some important characteristics you should know about them.

---

## Key features of R8a instances

Each vCPU on a R8a instance corresponds to a physical CPU core (a practice AWS began with the 7th generation AMD instances). This means there is no Simultaneous Multithreading (SMT). Each vCPU is assigned its own physical core — delivering more stable and consistent performance by avoiding resource sharing or contention between threads; this is particularly important for performance-sensitive or latency-sensitive workloads.

When evaluating and migrating to R8a, you should re-evaluate your CPU utilization thresholds — as you can likely utilize more CPU per instance without impacting your workload's SLA (Service Level Agreement).

> *R8a supports a very wide range of configurations — up to 192 vCPUs with 1,536 GiB of RAM. Below is a detailed table of common sizes:*

| Instance size  | vCPU | Memory (GiB) | Instance storage | Network bandwidth (Gbps) | EBS bandwidth (Gbps) |
|----------------|------|--------------|------------------|--------------------------|----------------------|
| r8a.medium     | 1    | 8            | EBS Only         | Up to 12.5               | Up to 10             |
| r8a.large      | 2    | 16           | EBS Only         | Up to 12.5               | Up to 10             |
| r8a.xlarge     | 4    | 32           | EBS Only         | Up to 12.5               | Up to 10             |
| r8a.2xlarge    | 8    | 64           | EBS Only         | Up to 15                 | Up to 10             |
| r8a.4xlarge    | 16   | 128          | EBS Only         | Up to 15                 | Up to 10             |
| r8a.8xlarge    | 32   | 256          | EBS Only         | 15                       | 10                   |
| r8a.12xlarge   | 48   | 384          | EBS Only         | 22.5                     | 15                   |
| r8a.16xlarge   | 64   | 512          | EBS Only         | 30                       | 20                   |
| r8a.24xlarge   | 96   | 768          | EBS Only         | 40                       | 30                   |
| r8a.48xlarge   | 192  | 1536         | EBS Only         | 75                       | 60                   |
| r8a.metal-24xl | 96   | 768          | EBS Only         | 40                       | 30                   |
| r8a.metal-48xl | 192  | 1536         | EBS Only         | 75                       | 60                   |

---

## MySQL Performance Testing with HammerDB

R8a instances are an excellent choice for MySQL databases, so I believe this is a fitting context to illustrate their capabilities. To test MySQL, I used a set of scripts developed by my colleagues to track MySQL performance across various software versions and EC2 instance types. These scripts are hosted in the repo-collection repository, an open-source, scalable framework designed for performance testing based on real-world workloads rather than micro-benchmarks.
This framework was built to provide a performance measurement reference standard usable across organizations, currently focused primarily on MySQL and actively used in discussions with Linux Kernel developers and maintainers. Additionally, it supports tracking any performance impacts arising from MySQL source code changes.
The scripts in this repository handle setting up a MySQL database for testing, along with a load generator running the HammerDB benchmark.

For this benchmark, I used a r6a.24xlarge instance as the load generator, and r6a.xlarge, r7a.xlarge, and r8a.xlarge instances as the MySQL database servers, all deployed within the same AWS Availability Zone (AZ). I chose a single-AZ configuration to minimize latency variability that could arise from traffic crossing multiple AZs. This is not a production simulation configuration, and I highly recommend using multiple AZs for production workloads.
Each MySQL instance was tested independently using the same HammerDB load generator. Each test was run three times, and the results were averaged over the three runs. The architecture diagram is illustrated in the following figure:

![](/static/images/blog-1/image-1.png)

### Overall HammerDB Results
R8a instances demonstrated superior performance in the HammerDB benchmark for MySQL databases. In the HammerDB overall score category, R8a instances scored 55% higher than R7a and 74% higher than R6a.

![](/static/images/blog-1/image-2.png)

### HammerDB Transactions Per Minute (TPM) Testing
R8a instances also showed significant improvement in this category. Compared to the previous generation R7a instances, R8a delivered 32% higher performance. When compared to R6a instances, R8a achieved an improvement of up to 63%.

![](/static/images/blog-1/image-3.jpg)

### HammerDB P99 Latency Results
R8a instances showed a clear improvement in P99 latency, reflecting the efficiency of the 5th Generation AMD EPYC processors along with higher memory bandwidth. R8a achieved a 14% reduction in latency compared to R7a and a 25% reduction compared to R6a.

![](/static/images/blog-1/image-4.png)

---

## Conclusion
The R8a instance, built on the AWS Nitro System with sixth-generation Nitro Cards, is the ideal choice for high-performance, memory-intensive workloads — such as SQL/NoSQL databases, distributed web-scale in-memory caches, in-memory databases, real-time big data analytics, and EDA (Electronic Design Automation) applications.
With 12 different sizes (including 2 bare-metal sizes), R8a is suitable for everything from small applications to large-scale systems. R8a is SAP certified and offers 38% more SAPS than R7a.
If you are currently using R6a (6th generation) instances, you should migrate to R8a to take advantage of the clear price-performance benefits. Maintaining modern infrastructure also helps reduce operational costs and delivers more features to customers.
