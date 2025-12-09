---
title: "Worklog Tuần 5"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Mục tiêu tuần 5:

* Thiết kế, triển khai được các API để:
  * Thay đổi thông tin bảo mật tài khoản
  * Quản lí (thêm, chỉnh sửa, xoá) danh mục hệ thống
  * Quản lí (chỉnh sửa) thông tin người dùng
  * Xây dựng quy trình xác minh tài khoản bằng Rekognition và Textract
  * Quản lí (thêm, chỉnh sửa, xoá) các phiên đấu giá
* Hiểu và ứng dụng được Redis trong việc cache query để tăng hiệu năng của hệ thống

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                            | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                               |
| --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|------------------------------------------------------------------------------------------------------------------------------|
| 2   | - Xây dựng API để thay đổi thông tin đăng nhập, thông tin bảo mật tài khoản                                                                                          | 6/10/2025    | 6/10/2025       |                                                                                                                              |
| 3   | - Xây dựng API để quản lí danh mục hệ thống, quản lí thông tin người dùng <br/>- Xây dựng quy trình xác minh thông tin người dùng dựa bằng Rekognition và Textract   | 7/10/2025    | 7/10/2025       |                                                                                                                              |
| 4   | - Xây dựng API để quản lí các phiên đấu giá                                                                                                                          | 8/10/2025    | 8/10/2025       |                                                                                                                              |
| 5   | - Tìm hiểu về Redis <br/> - Sử dụng Redis để cache query nhằm tăng hiệu năng, giảm tải cho database                                                                  | 9/10/2025    | 9/10/2025       | https://spring.io/projects/spring-data-redis#learn <br/> https://viblo.asia/p/huong-dan-spring-boot-redis-aWj53NPGl6m <br/> https://kungfutech.edu.vn/bai-viet/spring-boot/su-dung-redis-trong-spring-boot |
| 6   | - API testing, sửa chữa các lỗi phát sinh trong quá trình phát triển                                                                                                 | 10/10/2025   | 10/10/2025      |                                                                                                                              |


### Kết quả đạt được tuần 5:

* Triển khai hoàn tất các API sau:
  * API để người dùng đổi mật khẩu, thay đổi email, xác minh mật khẩu.
  * API quản lí địa chỉ, danh mục sản phẩm: Thêm mới, chỉnh sửa, disable.
  * API để người dùng cập nhật thông tin cá nhân: username, avatar.
  * API để staff có quyền chỉnh sửa thông tin người dùng ở các trường dữ liệu cần truy cập trong các use case đặc biệt: trạng thái xác thực, khoá (mở khoá) đăng nhập, xoá thời gian giới hạn giao dịch.
  * API để xác minh thông tin người dùng dựa vào ảnh selfie và giấy tờ tuỳ thân: sử dụng tính năng Face Compare của Rekognition để so sánh độ khớp khuôn mặt và Analyze Document ID của Textract để trích xuất dữ liệu cần thiết.
  * Cấu hình được Redis để cache kết quả khi thực hiện query database, giảm tải cho hệ thống database khi web đấu giá là một hệ thống yêu cầu cao về mặt hiệu năng.


