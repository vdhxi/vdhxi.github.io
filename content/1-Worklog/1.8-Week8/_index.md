---
title: "Worklog Week 8"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---



### Week 8 Objectives:

* Build delivery process after auction session completion
* Build constraint mechanism, check conditions to avoid users spamming virtual auction sessions in the system

### Tasks to implement this week:
| Day | Task                                                                                                                                                                                                            | Start Date | End Date   | Resources |
| --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|------------|-----------|
| Mon | - Add check conditions in data validation mechanism for users to create new auction sessions <br/> Edit logic code in related functions                                                                         | 27/10/2025 | 27/10/2025 |           |
| Tue | - Create APIs to update post-auction delivery process: <br/> + Seller creates order <br/> + User confirms order <br/> + Allow seller/buyer to update order                                                      | 28/10/2025 | 28/10/2025 |           |
| Wed | - Create APIs allowing order status updates: <br/> + Completed <br/> + Cancel order by buyer/seller <br/> + Create return/refund request                                                                        | 29/10/2025 | 29/10/2025 |           |
| Thu | - Implement return/refund process handled by staff role <br/> - Update wallet balance and transaction history of users in cases                                                                                 | 30/10/2025 | 30/10/2025 |           |
| Fri | - API testing, check and fix errors appearing during development                                                                                                                                                | 31/10/2025 | 31/10/2025 |           |


### Week 8 Achievements:
* Completed building post-auction delivery process:
  * Create order.
  * Buyer/seller confirms, updates information.
  * Completed implementation of confirmation process for completion, cancellation, return/refund.

* Updated auction session creation conditions, edited logic code in other APIs to fit business rules.
