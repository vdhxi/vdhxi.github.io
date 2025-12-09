---
title: "Worklog Tuần 12"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---

### Mục tiêu tuần 12:

* Kiểm thử hệ thống web đấu giá, khắc phục các lỗi trong quá trình phát triển
* Triển khai được hệ thống lên môi trường cloud

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                      | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                             |
| --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------|--------------------------------------------|
| 2   | - Chỉnh sửa lại giao diện, các button, components, font size                                                                                                                   | 24/11/2025   | 24/11/2025      |                                            |
| 3   | - Sửa các lỗi logic ở backend: <br/> + Chỉnh sửa cơ chế đặt cọc số dư khi tạo đấu giá mới <br/> + Chỉnh sửa các lỗi logic liên quan đến verify dữ liệu khi đặt đấu giá         | 25/11/2025   | 25/11/2025      |                                            |
| 4   | - Triển khai hệ thống lên môi trường cloud AWS, cấu hình biến môi trường                                                                                                       | 26/11/2025   | 26/11/2025      | https://cloudjourney.awsstudygroup.com/vi/ |
| 5   | - Sửa lỗi hệ thống, chỉnh sửa Url mapping khi triển khai trên môi trường cloud AWS <br/> - Chỉnh sửa frontend và backend để khắc phục lỗi race condition gây duplicate dữ liệu | 27/11/2025   | 27/11/2025      |                                            |
| 6   | - Tối ưu hoá code backend nhằm tăng hiệu năng, tối ưu query, loại bỏ những service không cần thiết                                                                             | 28/11/2025   | 28/11/2025      |                                            |

### Kết quả đạt được tuần 12:

* Kiểm thử toàn bộ hệ thống web đấu giá, tiếp tục hoàn thiện những chức năng, giao diện còn lại
* Triển khai được hệ thống lên môi trường cloud AWS, sử dụng các dịch vụ:
  * AWS EC2
  * AWS RDS
  * AWS S3 storage
  * AWS Route 53
  * AWS CloudFront
  * AWS Rekognition
  * AWS Textract
* Tối ưu hoá hệ thống bằng cách thiết kế lại logic code

