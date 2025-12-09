---
title: "Worklog Week 5"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Week 5 Goals:

* Design and implement APIs to:
  * Change account security information
  * Manage (add, edit, delete) system categories
  * Manage (edit) user information
  * Build account verification process using Rekognition and Textract
  * Manage (add, edit, delete) auctions
* Understand and apply Redis to cache queries to increase system performance

### Tasks to be implemented this week:
| Day | Task | Start Date | End Date | Resource |
| --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|------------------------------------------------------------------------------------------------------------------------------|
| Mon | - Build API to change login information, account security information                                                                                          | 6/10/2025    | 6/10/2025       |                                                                                                                              |
| Tue | - Build API to manage system categories, manage user information <br/>- Build user information verification process using Rekognition and Textract   | 7/10/2025    | 7/10/2025       |                                                                                                                              |
| Wed | - Build API to manage auctions                                                                                                                          | 8/10/2025    | 8/10/2025       |                                                                                                                              |
| Thu | - Research Redis <br/> - Use Redis to cache queries to increase performance, reduce load on database                                                                  | 9/10/2025    | 9/10/2025       | https://spring.io/projects/spring-data-redis#learn <br/> https://viblo.asia/p/huong-dan-spring-boot-redis-aWj53NPGl6m <br/> https://kungfutech.edu.vn/bai-viet/spring-boot/su-dung-redis-trong-spring-boot |
| Fri | - API testing, fixing bugs arising during development                                                                                                 | 10/10/2025   | 10/10/2025      |                                                                                                                              |


### Week 5 Results:

* Completed implementation of the following APIs:
  * API for users to change password, change email, verify password.
  * API to manage addresses, product categories: Add new, edit, disable.
  * API for users to update personal information: username, avatar.
  * API for staff to edit user information in data fields requiring access in special use cases: authentication status, lock (unlock) login, remove transaction limit time.
  * API to verify user information based on selfie and ID documents: use Rekognition's Face Compare feature to match faces and Textract's Analyze Document ID to extract necessary data.
  * Configured Redis to cache results when querying database, reducing load on database system as the auction web is a high-performance system.
