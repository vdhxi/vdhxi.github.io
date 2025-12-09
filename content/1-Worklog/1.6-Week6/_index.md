---
title: "Worklog Week 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Week 6 Goals:

* Continue building backend API for auction web system

### Tasks to be implemented this week:
| Day | Task | Start Date | End Date | Resource |
| --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|-------------------------------------------------------|
| Mon | - Fix bugs in auction web APIs                                                                                                                                                                                               | 13/10/2025   | 13/10/2025      |                                                       |
| Tue | - Fix bugs in auction web APIs                                                                                                                                                                                               | 14/10/2025   | 14/10/2025      |                                                       |
| Wed | - API testing, checking and fixing remaining bugs                                                                                                                                                                   | 15/10/2025   | 15/10/2025      |                                                       |
| Thu | - Build bid placement API, using redis lock to fix race condition <br/> - Redesign database, modify relationships between entities <br/> - Create basic APIs to manage user wallets in the system | 16/10/2025   | 16/10/2025      | https://www.anhdh.net/blog/redis-distributed-locking  |
| Fri | - Build feature to send support requests, handle user support requests <br/> - Build API for staff to stop invalid auctions                                                                       | 17/10/2025   | 17/10/2025      |                                                       |


### Week 6 Results:
* Continued to perfect APIs for auction web system:
  * Built bid placement API applying Redis distributed lock mechanism
  * Redesigned database to fit current system entities
  * Built APIs serving staff role use cases in the system:
    * Stop invalid auctions
    * Handle user tickets
