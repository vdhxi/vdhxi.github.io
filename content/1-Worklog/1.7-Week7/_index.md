---
title: "Worklog Week 7"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Week 7 Goals:
* Implement e-wallet integrated into the auction system


### Tasks to be implemented this week:
| Day | Task | Start Date | End Date | Resource |
| --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|----------------------------------------------------------------|
| Mon | - Integrate VnPay for system deposit function <br/>                                                                                                                                  | 20/10/2025   | 20/10/2025      | https://sandbox.vnpayment.vn/apis/docs/thanh-toan-pay/pay.html |
| Tue | - Fix VnPay bugs                                                                                                                                                                             | 21/10/2025   | 21/10/2025      |                                                                |
| Wed | - Build auxiliary APIs for main functions: <br/> + Verify PIN code <br/> + Change PIN code <br/> + Change daily transfer limit <br/> - Create API to view transaction history | 22/10/2025   | 22/10/2025      |                                                                |
| Thu | - Combine security information verification APIs to implement features: <br/> + Transfer money <br/> + Withdraw money                                                                              | 23/10/2025   | 23/10/2025      |                                                                |
| Fri | - API testing, checking and fixing bugs appearing during development                                                                                                           | 24/10/2025   | 24/10/2025      |                                                                |


### Week 7 Results:

* Completed implementation of e-wallet system into the auction system, serving many other logics with functions such as:
  * Deposit
  * Transfer money
  * Withdraw money
  * View transaction history
