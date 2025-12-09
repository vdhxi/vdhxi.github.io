---
title: "Worklog Week 11"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---



### Week 11 Objectives:

* Create admin page and complete it
* Implement websocket to receive realtime message notifications from backend

### Tasks to implement this week:
| Day | Task                                                                                                                                              | Start Date | End Date   | Resources |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------|------------|------------|-----------|
| Mon | - Create admin page <br/> - Link APIs                                                                                                             | 17/11/2025 | 17/11/2025 |           |
| Tue | - Implement websocket to receive realtime notifications from backend <br/> - Update frontend interface to fit information needing display         | 18/11/2025 | 18/11/2025 |           |
| Wed | - Fix websocket error when receiving message from backend, update data when receiving message from backend                                        | 19/11/2025 | 19/11/2025 |           |
| Thu | - Fix backend error when sending message to frontend, reconfigure websocket to allow frontend to subscribe to websocket                           | 20/11/2025 | 20/11/2025 |           |
| Fri | - Configure, fix json error with redis in backend causing display error in frontend <br/> - Update auction detail page interface in frontend      | 21/11/2025 | 21/11/2025 |           |

### Week 11 Achievements:

* Completed admin page to manage system
  * Manage categories: create new, edit, delete
  * Manage addresses: create new, edit, delete

* Implemented websocket to receive realtime messages from backend to update information quickly:
  * Update information when there is a new auction
  * Update price and end time, winner when a new bid is placed for an auction session
  * Update wallet balance information and transaction history
  * Update system notifications

* Configured websocket and redis:
  * Allow frontend to receive private notifications
  * Fix Json parse error when caching data with redis
