---
title: "Worklog Week 9"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---



### Week 9 Objectives:

* Configure websocket in backend to send real-time notifications
* Build interface for auction web system

### Tasks to implement this week:
| Day | Task                                                                                                                                                                                                                               | Start Date | End Date   | Resources                                             |
| --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|------------|-------------------------------------------------------|
| Mon | - Implement websocket to send notifications when there are new events in backend                                                                                                                                                   | 3/11/2025  | 3/11/2025  | https://spring.io/guides/gs/messaging-stomp-websocket |
| Tue | - Build main interfaces for auction web system: <br/> + Home page <br/> + Login page <br/> + Registration page <br/> + Forgot password page <br/> + Auction list page <br/> + Auction detail page <br/>                            | 4/11/2025  | 4/11/2025  |                                                       |
| Wed | - Build user interface for auction web system (1)                                                                                                                                                                                  | 5/11/2025  | 6/11/2025  |                                                       |
| Thu | - Build user interface for auction web system (2)                                                                                                                                                                                  | 6/11/2025  | 6/11/2025  |                                                       |
| Fri | - Link API for main pages                                                                                                                                                                                                          | 7/11/2025  | 7/11/2025  |                                                       |


### Week 9 Achievements:

* Configured WebSocket in backend to send realtime messages to frontend when the following events occur:
  * Update new auction session.
  * Update price, new status for auction session.
  * Balance fluctuation notification.
  * Order notification after successful auction.


* Built interface for main pages, successfully linked API for use cases:
  * Registration
  * Login 
  * Login with OTP verification code
  * Recover login password
  * View current auction sessions
  * View details of an auction session


* Built user interface including pages:
  * Info management: Update info, verify personal info.
  * Auction session management: Create new, update, cancel session.
  * Address management: Create new, update, delete.
  * Wallet management: Create new, top up, transfer, withdraw, change PIN, change limit, view transaction history.
  * Order management: View, edit, confirm status.
  * Support request management: Create new, view.
  * Security info management: Change password, email, enable and disable 2-step verification.
