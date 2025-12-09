---
title: "Worklog Tuần 11"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---



### Mục tiêu tuần 11:

* Tạo được trang admin và hoàn thiện
* Triển khai được websocket để nhận thông báo message từ backend realtime

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|----------------|
| 2   | - Tạo trang admin <br/> - Liên kết được các API                                                                                                   | 17/11/2025   | 17/11/2025      |                |
| 3   | - Triển khai websocket để nhận thông báo realtime từ backend <br/> - Cập nhật lại giao diện ở frontend cho phù hợp với các thông tin cần hiển thị | 18/11/2025   | 18/11/2025      |                |
| 4   | - Sửa lỗi websocket khi nhận message từ backend, cập nhật dữ liệu khi nhận message từ backend                                                     | 19/11/2025   | 19/11/2025      |                |
| 5   | - Sửa lỗi backend khi gửi message đến frontend, cấu hình lại websocket cho phép frontend subscribe websocket                                      | 20/11/2025   | 20/11/2025      |                |
| 6   | - Cấu hình, sửa lỗi json với redis ở backend gây lỗi hiển thị ở frontend <br/> - Cập nhật lại giao diện trang chi tiết đấu giá ở frontend         | 21/11/2025   | 21/11/2025      |                |

### Kết quả đạt được tuần 11:

* Hoàn thiện được trang admin để quản lí hệ thống
  * Quản lí danh mục: tạo mới, sửa, xoá
  * Quản lí điạ chỉ: tạo mới, sửa, xoá

* Triển khai được websocket để nhận message realtime từ backend để cập nhật thông tin nhanh chóng:
  * Cập nhật thông tin khi có đấu giá mới
  * Cập nhật giá và thời gian kết thúc, người thắng khi có bước giá mới được đặt cho 1 phiên đấu giá
  * Cập nhật thông tin số dư ví và lịch sử giao dịch
  * Cập nhật thông báo hệ thống

* Cấu hình websocket và redis:
  * Cho phép frontend nhận thông báo riêng tư
  * Sửa lỗi parse Json khi cache data bằng redis

