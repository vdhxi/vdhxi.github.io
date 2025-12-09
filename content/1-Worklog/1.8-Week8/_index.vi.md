---
title: "Worklog Tuần 8"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu tuần 8:

* Xây dựng quy trình giao hàng sau khi hoàn tất phiên đấu giá
* Xây dựng cơ chế ràng buộc, kiểm tra điều kiện để tránh việc người dùng spam tạo phiên đấu giá ảo trong hệ thống

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|----------------|
| 2   | - Thêm điều kiện kiểm tra trong cơ chế xác thực dữ liệu để người dùng tạo phiên đấu giá mới <br/> Chỉnh sử logic code ở các chức năng có liên quan                              | 27/10/2025   | 27/10/2025      |                |
| 3   | - Tạo các API để cập nhật quy trình giao hàng sau đấu giá: <br/> + Người bán tạo đơn hàng <br/> + Người dùng xác nhận đơn hàng <br/> + Cho phép người bán/mua cập nhật đơn hàng | 28/10/2025   | 28/10/2025      |                |
| 4   | - Tạo các API cho phép cập nhật trạng thái đơn hàng: <br/> + Hoàn thành <br/> + Huỷ đơn hàng bởi người mua/bán <br/> + Tạo yêu cầu trả hàng hoàn tiền                           | 29/10/2025   | 29/10/2025      |                |
| 5   | - Triển khai quy trình trả hàng hoàn tiền được xử lí bởi role staff <br/> - Cập nhật số dư ví và lịch sử giao dịch của người dùng trong các trường hợp                          | 30/10/2025   | 30/10/2025      |                |
| 6   | - API testing, kiểm tra và khắc phục các lỗi xuất hiện trong quá trình phát triển                                                                                               | 31/10/2025   | 31/10/2025      |                |

### Kết quả đạt được tuần 8:
* Xây dựng hoàn tất được quy trình giao hàng sau đấu giá:
  * Taọ đơn hàng.
  * Người mua/bán xác nhận, cập nhật thông tin.
  * Triển khai hoàn tất quy trình xác nhận hoàn thành, huỷ bỏ, trả hàng hoàn tiền.

* Cập nhật điều kiện tạo phiên đấu giá, chỉnh sửa logic code ở những API khác để phù hợp với business rule.


