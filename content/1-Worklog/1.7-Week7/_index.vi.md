---
title: "Worklog Tuần 7"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---


### Mục tiêu tuần 7:
* Triển khai xây dựng ví điện tử tích hợp vào hệ thống đấu giá


### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                 |
| --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|----------------------------------------------------------------|
| 2   | - Tích hợp VnPay cho chức năng nạp tiền vào hệ thống <br/>                                                                                                                                  | 20/10/2025   | 20/10/2025      | https://sandbox.vnpayment.vn/apis/docs/thanh-toan-pay/pay.html |
| 3   | - Fix lỗi VnPay                                                                                                                                                                             | 21/10/2025   | 21/10/2025      |                                                                |
| 4   | - Xây dựng các API phụ trợ cho những chức năng chính: <br/> + Xác nhận mã PIN <br/> + Thay đổi mã pin <br/> + Thay đổi hạn mức chuyển khoản hàng ngày <br/> - Tạo API xem lịch sử giao dịch | 22/10/2025   | 22/10/2025      |                                                                |
| 5   | - Kết hợp các API xác minh thông tin bảo mật để triển khai các tính năng: <br/> + Chuyển tiền <br/> + Rút tiền                                                                              | 23/10/2025   | 23/10/2025      |                                                                |
| 6   | - API testing, kiểm tra và khắc phục các lỗi xuất hiện trong quá trình phát triển                                                                                                           | 24/10/2025   | 24/10/2025      |                                                                |


### Kết quả đạt được tuần 7:

* Triển khai hoàn tất hệ thống ví điện tử vào hệ thống đấu giá, phục vụ cho nhiều logic khác với các chức năng như:
  * Nạp tiền
  * Chuyển tiền
  * Rút tiền
  * Xem lịch sử giao dịch
  
