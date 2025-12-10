---
title: "Amazon ElastiCache"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 5.2.2 </b> "
---

# Initialize Amazon ElastiCache (Redis)

Redis helps cache frequent queries and store user sessions.

## Steps

### 1. Create Subnet Group
1. Go to **ElastiCache Dashboard** -> **Subnet groups** -> **Create subnet group**.
![Redis Subnet](/images/project/redis/redis-subnet.png)

### 2. Create Security Group
Create a Security Group allowing port 6379 from EC2.
![Redis SG](/images/project/redis/redis-sg.png)

### 3. Create Redis Cluster
1. Select **Redis OSS caches** -> **Create cache**.
2. Select **Configure and create a new cluster**.
3. Select **Cluster mode disabled** (for simplicity and cost savings).
![Redis Create 1](/images/project/redis/redis-create-1.png)

4. Configure Redis info.
![Redis Create 2](/images/project/redis/redis-create-2.png)

5. Configure Node type, e.g., `cache.t3.micro`.
![Redis Create 3](/images/project/redis/redis-create-3.png)

6. Select Subnet group.
![Redis Create 4](/images/project/redis/redis-create-4.png)

7. Select Security Group.
![Redis Create 5](/images/project/redis/redis-create-5.png)

8. Click **Create**.
