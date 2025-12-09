---
title: "Worklog Week 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Week 4 Goals:

* Build APIs for login, registration, and account recovery

### Tasks to be implemented this week:
| Day | Task | Start Date | End Date | Resource |
| --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|---------------------------------------------------------------------------------------------|
| Mon | - Research JWT Token <br/> - Design login process combined with real user verification, avoiding creation of multiple virtual accounts<br/> - Build account verification API based on Spring Security, using Jwt token | 29/09/2025   | 29/09/2025      | https://www.youtube.com/watch?v=1XC5WPQkXek&list=PL2xsxmVse9IaxzE8Mght4CFltGOqcG6FC&index=9 |
| Tue | - Research Java Mail Sender <br/> - Implement email sending feature using Java Mail Sender <br/> - Build API to send email to specific address <br/> - Implement email OTP security feature | 30/09/2025   | 30/09/2025      | https://mailtrap.io/blog/java-send-email/                                                   |
| Wed | - Research Google Authenticator TOTP 2-step verification system<br/> - Integrate TOTP 2-step verification feature into the system <br/> - Build OTP verification API                                                | 1/10/2025    | 1/10/2025       | https://www.youtube.com/watch?v=2m2yuaomCTc                                                 |
| Thu | - Design safe and secure password recovery process <br/> - Implement code, combine with other APIs to implement password recovery process                                                                    | 2/10/2025    | 2/10/2025       |                                                                                             |
| Fri | - API testing, fixing bugs during implementation to complete features and prepare for use in other processes requiring security                                                              | 3/10/2025    | 3/10/2025       |                                                                                             |


### Week 4 Results:
* Built APIs serving processes:
  * Registration: checked for duplicates, while limiting spam creation of junk accounts.
  * Login: built login process, user information verification based on JWT token. Also integrated TOTP to increase security.
  * Password recovery: built secure password recovery process, only the real owner can recover password by verifying via email and TOTP.
  * Designed information verification steps, linked together to create a strict security process for security purposes, only the owner can perform.
