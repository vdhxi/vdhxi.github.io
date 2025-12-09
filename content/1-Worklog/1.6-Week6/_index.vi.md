---
title: "Worklog Tuần 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:

* Tiếp tục xây dựng backend API cho hệ thống web đấu giá

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                        |
| --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|-------------------------------------------------------|
| 2   | - Fix lỗi các API web đấu giá                                                                                                                                                                                               | 13/10/2025   | 13/10/2025      |                                                       |
| 3   | - Fix lỗi các API web đấu giá                                                                                                                                                                                               | 14/10/2025   | 14/10/2025      |                                                       |
| 4   | - API testing, kiểm tra và khắc phục các lỗi còn tồn đọng                                                                                                                                                                   | 15/10/2025   | 15/10/2025      |                                                       |
| 5   | - Xây dựng API đặt giá bid, sử dụng redis lock để khắc phục race condition <br/> - Thiết kế lại database, chỉnh sửa lại relationship giữa các entity <br/> - Tạo các API cơ bản để quản lí ví của người dùng trong hệ thống | 16/10/2025   | 16/10/2025      | https://www.anhdh.net/blog/redis-distributed-locking  |
| 6   | - Xây dựng tính năng gửi yêu cầu hỗ trợ, xử lí yêu cầu hỗ trợ của người dùng <br/> - Xây dựng API để staff có thể dừng các phiên đấu giá không hợp lệ                                                                       | 17/10/2025   | 17/10/2025      |                                                       |


### Kết quả đạt được tuần 6:
* Tiếp tục hoàn thiện được các API cho hệ thống web đấu giá:
  * Xây dựng được API đặt bid áp dụng cơ chế Redis lock distributed
  * Thiết kế lại database để phù hợp với các entity hiện tại của hệ thống
  * Xây dựng được các API phục vụ cho use case của role staff trong hệ thống:
    * Dừng các phiên đấu giá không hợp lệ
    * Xử lí ticket của người dùng
