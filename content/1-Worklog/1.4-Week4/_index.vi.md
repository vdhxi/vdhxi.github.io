---
title: "Worklog Tuần 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu tuần 4:

* Xây dựng được các API phục vụ cho việc đăng nhập, đăng kí, khôi phục tài khoản

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                            | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                              |
| --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|---------------------------------------------------------------------------------------------|
| 2   | - Tìm hiểu về JWT Token <br/> - Thiết kế quy trình đăng nhập kết hợp xác thực người dùng thực tế, tránh tạo ra nhiều tài khoản ảo<br/> - Xây dựng API xác thực tài khoản dựa trên Spring Security, sử dụng Jwt token | 29/09/2025   | 29/09/2025      | https://www.youtube.com/watch?v=1XC5WPQkXek&list=PL2xsxmVse9IaxzE8Mght4CFltGOqcG6FC&index=9 |
| 3   | - Tìm hiểu về Java Mail Sender <br/> - Triển khai tính năng gửi mail bằng Java Mail Sender <br/> - Xây dựng được API gửi mail đến địa chỉ cụ thể <br/> - Triển khai được tính năng bảo mật email OTP                 | 30/09/2025   | 30/09/2025      | https://mailtrap.io/blog/java-send-email/                                                   |
| 4   | - Tìm hiểu về hệ thống xác thực 2 bước TOTP Google Authenticator<br/> - Tích hợp tính năng xác thực hai bước TOTP vào hệ thống <br/> - Xây dựng được API xác minh OTP                                                | 1/10/2025    | 1/10/2025       | https://www.youtube.com/watch?v=2m2yuaomCTc                                                 |
| 5   | - Thiết kế quy trình khôi phục mật khẩu an toàn, bảo mật <br/> - Triển khai code, kết hợp các API khác để triển khai quy trình khôi phục mật khẩu                                                                    | 2/10/2025    | 2/10/2025       |                                                                                             |
| 6   | - API testing, sửa chữa lỗi trong quá trình triển khai để hoàn thiện tính năng và chuẩn bị cho việc sử dụng vào các quy trình khác yêu cầu tính bảo mật                                                              | 3/10/2025    | 3/10/2025       |                                                                                             |


### Kết quả đạt được tuần 4:
* Xây dựng được các API phục vụ cho các quy trình:
  * Đăng kí: kiểm tra được tính trùng lập, đồng thời hạn chế được việc spam tạo ra các tài khoản rác.
  * Đăng nhập: xây dựng được quy trình đăng nhập, xác thực thông tin người dùng dựa trên JWT token. Đồng thời tích hợp TOTP nhằm tăng tính bảo mật.
  * Khôi phục mật khẩu: xây dựng được quy trình khôi phục mật khẩu một cách bảo mật, chỉ có người sở hữu thật mới có thể khôi phục mật khẩu bằng việc xác minh qua email và TOTP.
  * Thiết kế được các bước xác thực thông tin, liên kết với nhau tạo thành một quy trình bảo mật nghiêm ngặt nhằm mục đích bảo mật, chỉ chủ sở hữu mới có thể thực hiện.



