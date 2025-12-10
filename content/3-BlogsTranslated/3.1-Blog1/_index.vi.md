---
title: "Blog 1"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Lợi ích về hiệu năng của các phiên bản Amazon EC2 R8a tối ưu hóa bộ nhớ thế hệ mới

Gần đây, chúng tôi công bố việc cung cấp rộng rãi các phiên bản Amazon EC2 R8a — bổ sung mới nhất vào dòng các phiên bản tối ưu hóa bộ nhớ sử dụng CPU AMD. Những phiên bản này được trang bị bộ xử lý AMD EPYC thế hệ thứ 5 (tên mã “Turin”) với tần số tối đa lên tới 4,5 GHz. Trong bài viết này, tôi sẽ thử nghiệm các phiên bản đó và tiến hành benchmark MySQL — nhưng trước hết, hãy cùng điểm qua những đặc điểm quan trọng bạn nên biết về các phiên bản này.

---

## Đặc điểm nổi bật của phiên bản R8a

Mỗi vCPU trên một instance R8a tương ứng với một lõi CPU vật lý (điều mà AWS bắt đầu áp dụng từ các thế hệ AMD thế hệ thứ 7). Điều này nghĩa là không có công nghệ đa luồng đồng thời (SMT). Mỗi vCPU được gán lõi vật lý riêng biệt — giúp mang lại hiệu năng ổn định và nhất quán hơn, bởi tránh được việc chia sẻ tài nguyên hay xung đột giữa các luồng; điều này đặc biệt quan trọng cho các workload nhạy cảm với hiệu năng hoặc độ trễ.

Khi đánh giá và chuyển sang sử dụng R8a, bạn nên xác định lại ngưỡng sử dụng CPU — vì bạn có thể tận dụng nhiều hơn CPU của mỗi instance mà không làm ảnh hưởng đến SLA (Service Level Agreement) của workload.

> *R8a hỗ trợ cấu hình rất rộng — lên đến 192 vCPU với 1.536 GiB RAM. Dưới đây là bảng thông số chi tiết các kích cỡ phổ biến:*

| Instance size | vCPU | Memory (GiB) | Instance storage | Network bandwidth (Gbps) | EBS bandwidth (Gbps) |
|---|---|---|---|---|---|
| r8a.medium | 1 | 8 | EBS Only | Up to 12.5 | Up to 10 |
| r8a.large | 2 | 16 | EBS Only | Up to 12.5 | Up to 10 |
| r8a.xlarge | 4 | 32 | EBS Only | Up to 12.5 | Up to 10 |
| r8a.2xlarge | 8 | 64 | EBS Only | Up to 15 | Up to 10 |
| r8a.4xlarge | 16 | 128 | EBS Only | Up to 15 | Up to 10 |
| r8a.8xlarge | 32 | 256 | EBS Only | 15 | 10 |
| r8a.12xlarge | 48 | 384 | EBS Only | 22.5 | 15 |
| r8a.16xlarge | 64 | 512 | EBS Only | 30 | 20 |
| r8a.24xlarge | 96 | 768 | EBS Only | 40 | 30 |
| r8a.48xlarge | 192 | 1536 | EBS Only | 75 | 60 |
| r8a.metal-24xl | 96 | 768 | EBS Only | 40 | 30 |
| r8a.metal-48xl | 192 | 1536 | EBS Only | 75 | 60 |

---

## Thử nghiệm hiệu năng MySQL với HammerDB

Các phiên bản R8a là lựa chọn tuyệt vời cho cơ sở dữ liệu MySQL, vì vậy tôi cho rằng đây là bối cảnh phù hợp để minh họa những khả năng của các phiên bản này. Để kiểm thử MySQL, tôi sử dụng một loạt script do các đồng nghiệp của tôi phát triển nhằm theo dõi hiệu năng MySQL trên nhiều phiên bản phần mềm và các loại phiên bản EC2 khác nhau. Những script này được lưu trữ trong repository repro-collection, một framework mã nguồn mở, có khả năng mở rộng, được thiết kế cho mục đích kiểm thử hiệu năng dựa trên các workload thực tế thay vì các micro-benchmark.
Framework này được xây dựng để cung cấp một chuẩn tham chiếu đo lường hiệu năng có thể sử dụng trên nhiều tổ chức, hiện tập trung chủ yếu vào MySQL và đang được sử dụng tích cực trong các cuộc trao đổi với các nhà phát triển và maintainer của Linux Kernel. Ngoài ra, nó còn hỗ trợ theo dõi bất kỳ tác động hiệu năng nào phát sinh từ các thay đổi mã nguồn của MySQL.
Các script trong repository này đảm nhận việc thiết lập một cơ sở dữ liệu MySQL để tiến hành kiểm thử, cùng với một load generator chạy benchmark HammerDB.

Đối với bài benchmark này, tôi sử dụng một instance r6a.24xlarge làm load generator, và các instance r6a.xlarge, r7a.xlarge, và r8a.xlarge làm máy chủ cơ sở dữ liệu MySQL, tất cả đều được triển khai trong cùng một AWS Availability Zone (AZ). Tôi chọn cấu hình trong một AZ duy nhất để giảm thiểu độ biến thiên độ trễ có thể phát sinh khi lưu lượng phải đi qua nhiều AZ. Đây không phải là cấu hình mô phỏng môi trường production, và tôi rất khuyến nghị sử dụng nhiều AZ đối với các workload chạy trong môi trường production.
Mỗi instance MySQL được kiểm thử độc lập bằng cùng một load generator HammerDB. Mỗi bài kiểm thử được chạy ba lần và kết quả được tính trung bình trên ba lần chạy đó. Sơ đồ kiến trúc được minh họa trong hình sau:

![](/images/blog-1/image-1.png)

### Kết quả tổng thể HammerDB
Các phiên bản R8a cho thấy hiệu năng vượt trội trong benchmark HammerDB đối với cơ sở dữ liệu MySQL. Ở hạng mục điểm tổng thể của HammerDB, các phiên bản R8a đạt điểm cao hơn 55% so với R7a và cao hơn 74% so với R6a.

![](/images/blog-1/image-2.png)

### Kiểm thử số giao dịch mỗi phút của HammerDB
Các phiên bản R8a cũng thể hiện mức cải thiện đáng kể ở hạng mục này. So với các phiên bản R7a thế hệ trước, R8a cho hiệu năng cao hơn 32%. Khi so với các phiên bản R6a, R8a đạt mức cải thiện lên tới 63%.

![](/images/blog-1/image-3.jpg)

### Kết quả độ trễ P99 của HammerDB
Các phiên bản R8a cho thấy mức cải thiện rõ rệt về độ trễ P99, phản ánh hiệu quả từ bộ xử lý AMD EPYC thế hệ thứ 5 cùng với băng thông bộ nhớ cao hơn. R8a đạt mức giảm 14% độ trễ so với R7a và giảm 25% độ trễ so với R6a.

![](/images/blog-1/image-4.png)

---

## Kết luận
Phiên bản R8a, được xây dựng trên nền tảng AWS Nitro System với các Nitro Cards thế hệ thứ sáu, là lựa chọn lý tưởng cho các workload cần hiệu năng cao, sử dụng nhiều bộ nhớ — ví dụ như cơ sở dữ liệu SQL/NoSQL, cache in-memory quy mô web phân tán, database in-memory, phân tích dữ liệu lớn thời gian thực (real-time big data analytics), và các ứng dụng EDA (Electronic Design Automation).
Với 12 kích cỡ khác nhau (bao gồm 2 cỡ bare-metal), R8a phù hợp từ các ứng dụng nhỏ đến các hệ thống quy mô lớn. R8a đã được chứng nhận SAP và cung cấp 38% SAPS nhiều hơn so với R7a.
Nếu bạn hiện đang dùng các instance R6a (thế hệ 6), bạn nên di chuyển lên R8a để tận dụng lợi ích rõ rệt về giá-hiệu năng. Việc duy trì hạ tầng hiện đại cũng giúp giảm chi phí vận hành và mang lại nhiều tính năng hơn cho khách hàng.