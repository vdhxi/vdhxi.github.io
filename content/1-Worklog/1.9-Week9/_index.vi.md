---
title: "Worklog Tuần 9"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---


### Mục tiêu tuần 9:

* Cấu hình websocket ở backend để gửi thông báo real time
* Xây dưng giao diện cho hệ thống web đấu giá

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                        |
| --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|-------------------------------------------------------|
| 2   | - Triển khai websocket để gửi thông báo khi ở backend có các sự kiện mới                                                                                                                                                           | 3/11/2025    | 3/11/2025       | https://spring.io/guides/gs/messaging-stomp-websocket |
| 3   | - Xây dựng các giao diện chính cho hệ thống web đấu giá: <br/> + Trang chủ <br/> + Trang đăng nhập <br/> + Trang đăng kí <br/> + Trang quên mật khẩu <br/> + Trang hiển thị danh sách đấu giá <br/> + Trang chi tiết đấu giá <br/> | 4/11/2025    | 4/11/2025       |                                                       |
| 4   | - Xây dựng giao diện user cho hệ thống web đấu giá (1)                                                                                                                                                                             | 5/11/2025    | 6/11/2025       |                                                       |
| 5   | - Xây dựng giao diện user cho hệ thống web đấu giá (2)                                                                                                                                                                             | 6/11/2025    | 6/11/2025       |                                                       |
| 6   | - Liên kết API cho các trang chính                                                                                                                                                                                                 | 7/11/2025    | 7/11/2025       |                                                       |

### Kết quả đạt được tuần 9:

* Cấu hình được WebSocket ở backend để gửi message realtime cho frontend khi có các sự kiện sau:
  * Cập nhật phiên đấu giá mới.
  * Cập nhật giá, trạng thái mới cho phiên đấu giá.
  * Thông báo biến động số dư.
  * Thông báo về đơn hàng sau khi đấu giá thành công.


* Xây dựng được giao diện cho các trang chính, liên kết API thành công cho các use case:
  * Đăng kí
  * Đăng nhập 
  * Đăng nhập với mã xác thực OTP
  * Khôi phục mật khẩu đăng nhập
  * Xem các phiên đấu giá hiện tại
  * Xem chi tiết một phiên đấu giá


* Xây dựng được giao diện user gồm các trang:
  * Quản lí thông tin: Cập nhật thông tin, xác minh thông tin cá nhân.
  * Quản lí các phiên đấu giá: Tạo mới, cập nhật, huỷ bỏ phiên.
  * Quan lí địa chỉ: Tạo mới, cập nhật, xoá.
  * Quản lí ví: Tạo mới, nạp tiền, chuyển tiền, rút tiền, thay đổi mã pin, thay đổi hạn mức, xem lịch sử giao dịch.
  * Quản lí đơn hàng : Xem, chỉnh sửa, xác nhận trạng thái.
  * Quản lí yêu cầu hỗ trợ: Tạo mới, xem.
  * Quản lí thông tin bảo mật: Đổi mật khẩi, email, bật và tắt tính năng xác thực 2 bước.
  

