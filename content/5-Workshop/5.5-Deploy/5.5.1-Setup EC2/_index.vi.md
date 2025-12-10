---
title: "Cài đặt môi trường EC2 instance"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.5.1 </b> "
---

# Cài đặt môi trường cho máy chủ EC2

Trong phần này, chúng ta sẽ thực hiện gán IAM Role cho EC2 và cài đặt các phần mềm cần thiết như Java và MariaDB để chuẩn bị cho việc triển khai ứng dụng.

## 1. Gán IAM role cho EC2

Để EC2 instance có quyền truy cập vào các dịch vụ AWS khác (ví dụ: Session Manager để kết nối mà không cần mở port SSH, hoặc truy cập S3, RDS), chúng ta cần gán IAM Role phù hợp.

1.  Truy cập vào **EC2 Dashboard**, chọn Instance mà bạn vừa khởi tạo.
2.  Chọn **Actions** -> **Security** -> **Modify IAM role**.

![Modify IAM Role](/images/project/ec2/iam%20role/iam-1.png)

3.  Chọn IAM Role đã tạo ở các bước trước (ví dụ: `EC2RoleForSSM`) và nhấn **Update IAM role**.

![Select IAM Role](/images/project/ec2/iam%20role/iam-2.png)

## 2. Cài đặt môi trường

Kết nối vào EC2 Instance (sử dụng Session Manager hoặc SSH). Sau đó thực hiện lần lượt các bước sau:

### 2.1. Cập nhật hệ thống

Chạy lệnh sau để cập nhật các gói phần mềm mới nhất:

```
sudo dnf update -y
```

![Update System](/images/project/ec2/ssh/update-system.png)

### 2.2. Cài đặt Java

Ứng dụng của chúng ta chạy trên nền tảng Java, do đó cần cài đặt Java Development Kit (JDK). Ở đây chúng ta sử dụng Amazon Corretto 21 (phiên bản headless phù hợp hơn cho giao diện dòng lệnh không cần đồ hoạ). 

```
sudo dnf install java-21-amazon-corretto-headless -y
```
![Install Java](/images/project/ec2/ssh/install-java.png)

Kiểm tra phiên bản Java sau khi cài đặt:

```
java -version
```


![Check Install](/images/project/ec2/ssh/check-install.png)

### 2.3. Cài đặt MariaDB Client và Khởi tạo Database

Cài đặt MariaDB client để có thể kết nối và thao tác với RDS.

```
sudo dnf install mariadb105 -y
```

![Install MariaDB](/images/project/ec2/ssh/install-maria-db.png)

Kết nối đến RDS database instance mà bạn đã tạo. Thay thế `<rds-endpoint>`, `<username>` bằng thông tin thực tế của bạn:

```
mysql -h <rds-endpoint> -u <username> -p
```

Sau khi nhập mật khẩu thành công, thực hiện tạo database cho ứng dụng:

```sql
CREATE DATABASE tickets;
SHOW DATABASES;
```

![Create Database RDS](/images/project/ec2/ssh/create-database-rds.png)

### 2.4. Cài đặt service để khởi chạy ứng dụng Java Springboot tự động

Chạy lệnh sau để tạo file service

```
sudo nano /etc/systemd/system/<service-name>.service
```

![Create service](/images/project/ec2/ssh/create-service-file.png)

Nhập nội dung file service, cấu hình biến môi trường cho ứng dụng

![Setup env](/images/project/ec2/ssh/env-setup.png)

Dùng tổ hợp phím Ctrl + O, Enter và Ctrl + X để lưu lại và thoát

Dùng các lệnh sau để áp dụng những thay đổi
```text
sudo systemctl daemon-reload

sudo systemctl restart <service-name>
```

Kiểm tra trạng thái bằng lệnh `status`
![Check status](/images/project/ec2/ssh/check-status-service.png)

Dùng lệnh `enable` để service có thể tự động chạy cùng lúc mỗi khi EC2 instance start
```text
sudo systemctl enable <service-name>
```

Lệnh chỉnh múi giờ để đồng bộ (trong trường hợp ứng dụng Java cần có múi giờ phù hợp với giờ Việt Nam)
```text
sudo timedatectl set-timezone Asia/Ho_Chi_Minh
```

Kiểm tra kết quả bằng lệnh
```text
date
```
