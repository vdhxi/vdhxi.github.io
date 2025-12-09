---
title: "Worklog Tuần 2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Mục tiêu tuần 2:

* Hiểu được các kiến thức cần thiết khi hosting website trên môi trường cloud
* Xây dựng và deploy thành công website trên môi trường cloud

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                      | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|-----------------| ----------------------------------------- |
| 2   | - Tìm hiểu về máy chủ ảo EC2<br/> - Thực hành tạo máy chủ EC2, cấu hình security group, kết nối đến EC2 bằng mobaXterm<br/>- Hosting backend tại máy chủ EC2                                   | 15/09/2025   | 15/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu về AWS S3<br/> - Thực hành tạo S3 bucket, upload, quản lí file<br/> - Thực hành hosting web với S3                                                                                  | 16/09/2025   | 16/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tìm hiểu về AWS RDS<br/> - Thực hành kết nối EC2 và RDS                                                                                                                                      | 17/09/2025   | 17/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu về Route53, CloudFront, AWS SES<br/> - Cấu hình quản lí dns cá nhân thông qua Route53<br/>- Cấu hình AWS SES để gửi mail                                                            | 18/09/2025   | 18/09/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Thực hành hosting website kết hợp EC2, AWS S3, Route53, CloudFront và RDS<br/>- Config security group để có thể truy cập SSH vào máy chủ để quản lí<br/> - Config elastic IP cho máy chủ EC2 | 19/09/2025   | 19/09/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Tìm hiểu được kiến thức về các dịch vụ cơ bản khi xây dựng website
* Ứng dụng được các dịch vụ đã tìm hiểu vào việc hosting website
* Hiểu cách để deploy một website thành công trên môi trường cloud
* Cấu hình được security group để truy cập SSH đến website, cấu hình và quản lí máy chủ
  * Cài đặt java cho hosting backend java
  * Cài đặt certbot để đăng kí SSL
  * Cài đặt nginx để chuyển truy cập đến máy chủ từ port 8080 giao thức HTTP sang port 443 giao thức HTTPS
