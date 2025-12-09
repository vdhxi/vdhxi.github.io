---
title: "Bản đề xuất"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Auction system build in AWS Cloud infrastructure
## Hệ thống web đấu giá xây dựng trên nền tảng điện toán đám mây của Amazon Web Service  

### 1. Tóm tắt điều hành   
Auction system được thiết kế bởi sinh viên FPTU tại TP. Hồ Chí Minh và vận hành trên nền tảng Cloud AWS. Nền tảng tận dụng các dịch vụ AWS để xây dựng một sàn đấu giá trực tuyến với giao diện thân thiện, dễ dàng sử dụng phù hợp với tất cả mọi người

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Hiện tại những hệ thống đấu giá vẫn chưa tiếp cận được đến nhiều người bởi vì sự khó tiếp cận. Dự án này ra đời để mang đến một nền tảng đấu giá trực tiếp minh bạch, thân thiện dễ tiếp cận đến mọi người.

*Giải pháp*  
Nền tảng sử dụng AWS CloudFront và S3 Storage kết hợp ReactJS cung cấp giao diện web , với máy chủ EC2 đảm nhiệm toàn bộ công việc xử lí trên nền tảng Springboot, Amazon S3 để lưu trữ dữ liệu công khai và riêng tư, AWS RDS để lưu trữ cơ sở dữ liệu. Kết hợp cùng Amazon Rekognition và Textract để trích xuất thông tin, xác minh thông tin người dùng để đảm bảo tính công bằng. Với nền tảng này, người dùng có thể đăng ký tài khoản mới, xác thực và tham gia những phiên đấu giá hấp dẫn trên nền tảng.  

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Dự án mang đến một nền tảng đấu giá trực tuyến dễ dàng tiếp cận đến mọi người. Chi phí hàng tháng ước tính 59.37 USD (theo AWS Pricing Calculator). Không phát sinh chi phí phát triển thêm.   

### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AWS để quản lý dữ liệu. Dữ liệu công khai được lưu trữ trong S3 public bucket và hiển thị đến người dùng qua CloudFront và S3 với ReactJS. Mọi thao tác xử lí được thực hiện trên EC2 với nền tảng Springboot. Các thông tin định danh được xử lí bởi Amazon Rekognition và Textract sau đó lưu trữ trong S3 private bucket 

![Auction System Architecture](/static/images/2-Proposal/auction-system-architecture.png)

*Dịch vụ AWS sử dụng*  
- *AWS VPC*: Tạo môi trường mạng ảo riêng tư.
- *AWS Route 53*: Điều hướng traffic của người dùng.
- *AWS CloudFront*: CDN giúp tăng tốc độ tải trang, giảm độ trễ truy cập web.
- *AWS Load Balancing*: Nhận request từ internet và điều hướng đến EC2, ổn định ứng dụng.
- *Amazon EC2*: Chạy ứng dụng springboot để xử lí backend, giao tiếp với database (RDS), cache query (ElastiCache), gọi các service AI (Rekognition, Textract) và xử lí đấu giá.
- *Amazon S3*: 
  1. Hosting Frontend: Lưu trữ source code của frontend (ReactJS, Tailwind) để CloudFront phân phối.
  2. Data storage: 2 bucket (public/private) để lưu trữ ảnh người dùng tải lên phục vụ cho đấu giá và xác minh tài khoản.
- *Amazon ElastiCache*: Bộ nhớ đệm, giúp lưu trữ truy vấn giảm tải cho database và tăng tốc độ phản hồi API.
- *Amazon RDS*: Lưu trữ dữ liệu chính của hệ thống, được đặt tại private subnet.
- *Amazon Rekognition*: Dịch vụ phân tích hình ảnh bằng AI, thực hiện so sánh khuôn mặt (Face Compare) giữa ảnh chụp selfie và ảnh trên giấy tờ tùy thân để xác minh danh tính (eKYC).
- *Amazon Textract*: Dịch vụ trích xuất văn bản từ tài liệu. Hệ thống sử dụng Textract để tự động đọc (OCR) và bóc tách thông tin từ ảnh chụp giấy tờ tùy thân để điền tự động cho người dùng.
- *Amazon SES*: Backend sử dụng dịch vụ này để gửi email xác thực tài khoản (OTP), thông báo thắng đấu giá hoặc các thông báo hệ thống khác tới người dùng.
- *Amazon CloudWatch*: Hệ thống giám sát và quản lý log.


*Thiết kế thành phần*
- *Tiếp nhận dữ liệu*: Dữ liệu từ người dùng.  
- *Lưu trữ dữ liệu*: Dữ liệu lưu ở 2 S3 bucket (1 cho public và 1 cho private - truy cập qua presigned url) 
- *Xử lý dữ liệu*: EC2 thực hiện việc xử lí dữ liệu.  
- *Giao diện web*: Amazon S3 lưu trữ ứng dụng ReactJS.  


### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án gồm các giai đoạn:  
1. *Nghiên cứu và vẽ kiến trúc*: Nghiên cứu và thiết kế kiến trúc AWS, xác định các dịch vụ sẽ sử dụng, thiết kế database.  
2. *Tính toán chi phí và kiểm tra tính khả thi*: Sử dụng AWS Pricing Calculator để ước tính và điều chỉnh.
3. *Phát triển, kiểm thử, triển khai*: Lập trình Springboot và ứng dụng ReactJS, sau đó kiểm thử ở môi trường local.  
4. *Triển khai trên môi trường Cloud AWS*: Thiết lập Gitlab CI, thiết lập môi trường cloud và triển khai.

*Yêu cầu kỹ thuật*
- Java 21 Springboot
- AWS SDK (S3, Rekognition, Textract, SES)
- MySQL RDS
- ReactJS/Vite/TypeScript/Tailwind
- Gitlab, Gitlab runner CI
- Postman, CloudWatch

### 5. Lộ trình & Mốc triển khai  
- *Trước thực tập (Tháng 0)*: 1 tháng lên kế hoạch và đánh giá trạm cũ.  
- *Thực tập (Tháng 1–3)*:  
    - Tháng 1: Học AWS và thiết kế kiến trúc, thiết kế database, triển khai xây dựng API.  
    - Tháng 2: Triển khai xây dựng API, xây dựng giao diện.  
    - Tháng 3: Triển khai trên môi trường cloud , kiểm thử, đưa vào sử dụng.

### 6. Ước tính ngân sách  
Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=05741eefd9e403091e36a896361a601881ad0aa9)

*Chi phí hạ tầng*
- Amazon Route53: $0.5/tháng (1 hosted zone)
- S3 Standard: $0.72/tháng (10 GB, 30000 request GET, 1000 request PUT, 5 GB Transfer out)
- Application Load Balancer: $18.80/tháng (data process 50GB) 
- Amazon EC2 (t3.medium): $16.35/tháng (3yr, no upfront)
- Amazon ElastiCache (cache.t3.micro): $9.49/tháng (3yr, no upfront)
- Amazon RDS: $8.38/tháng
- Rekognition: $0.13/tháng (100 FaceCompare)
- Textract: $5/tháng (200 Pages document)

*Tổng*: $59.37/tháng.


### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- Mất mạng: Ảnh hưởng lớn, xác suất thấp.
- Vượt ngân sách: Ảnh hưởng trung bình, xác suất thấp.  

*Chiến lược giảm thiểu*
- Chi phí: Cảnh báo ngân sách AWS, tối ưu dịch vụ.  

*Kế hoạch dự phòng*  
- Có backup định kì đề phòng xảy ra sự cố.  
- Sử dụng CloudFormation để khôi phục cấu hình liên quan đến chi phí.  

### 8. Kết quả kỳ vọng
*Giá trị dài hạn*: Có thể tái sử dụng cho các dự án khác trong tương lai.

Tham khảo thêm tại ![Proposal Template](/static/Proposal-Template.docx)