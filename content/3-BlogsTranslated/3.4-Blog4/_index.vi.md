---
title: "Blog 4"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
---

# DISA STIG cho Amazon Linux 2023 hiện đã có sẵn

Hôm nay, chúng tôi thông báo về sự sẵn có của Hướng dẫn Triển khai Kỹ thuật Bảo mật (STIG) cho [Amazon Linux 2023 (AL2023)](https://aws.amazon.com/linux/amazon-linux-2023/), được phát triển thông qua sự hợp tác giữa Amazon Web Services (AWS) và [Cơ quan Hệ thống Thông tin Quốc phòng](https://public.cyber.mil/stigs/) (DISA). Các hướng dẫn STIG rất quan trọng đối với [Bộ Quốc phòng Hoa Kỳ](https://www.defense.gov/) (DOD) và các khách hàng Liên bang cần tuân thủ bảo mật nghiêm ngặt bắt nguồn từ [Viện Tiêu chuẩn và Công nghệ Quốc gia (NIST) 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) và các tài liệu liên quan. Hướng dẫn triển khai kỹ thuật mới này cung cấp các cấu hình làm cứng (hardening) bảo mật Hệ điều hành (OS) chi tiết cho các tổ chức triển khai AL2023 trong môi trường DOD và các cơ quan khác yêu cầu sự phù hợp với DISA STIG. AL2023 STIG cung cấp cho khách hàng quyền truy cập vào hướng dẫn OS tuân thủ các tiêu chuẩn bảo mật nghiêm ngặt của chính phủ. Hướng dẫn này để triển khai các cấu hình STIG sẽ hợp lý hóa các quy trình bảo mật cho các tổ chức đang tìm kiếm các biện pháp kiểm soát an ninh mạng mạnh mẽ, cho dù họ cần duy trì sự tuân thủ DOD hay tự nguyện áp dụng các thực tiễn bảo mật tốt nhất này để nâng cao vị thế bảo mật của họ.

---

## Triển khai AL2023 DISA STIG với AWS

AWS Systems Manager (SSM) và EC2 Image Builder cung cấp các giải pháp gốc để triển khai các cấu hình AL2023 DISA STIG trong môi trường của bạn. Đối với các khách hàng có khối lượng công việc AL2023 EC2 hiện có, họ có thể sử dụng AWS Systems Manager (SSM) để hợp lý hóa việc triển khai STIG. Đối với các khách hàng muốn xây dựng các instance AL2023 EC2 tuân thủ STIG để sử dụng cho việc triển khai, họ có thể sử dụng EC2 Image Builder và tự động hóa việc áp dụng AL2023 DISA STIG.

## Xây dựng các Image tuân thủ STIG thông qua EC2 Image Builder

Khách hàng có thể sử dụng EC2 Image Builder để nâng cao và hợp lý hóa việc triển khai AL2023 DISA STIG của họ. Cách tiếp cận tích hợp này làm giảm đáng kể chi phí vận hành thường liên quan đến việc duy trì sự tuân thủ STIG. Do đó, khách hàng của chúng tôi có thể tập trung vào các nhiệm vụ cốt lõi của họ trong khi vẫn duy trì các tiêu chuẩn bảo mật cao nhất. Khách hàng của chúng tôi có thể sử dụng các thành phần làm cứng Linux hiện có của AWS EC2 Image Builder, hiện hỗ trợ các phát hiện AL2023 Category I, II và III để tự động tạo các image AL2023 EC2 tuân thủ STIG với sự can thiệp thủ công tối thiểu. Sự tự động hóa này làm giảm đáng kể thời gian và công sức thường cần thiết cho việc triển khai làm cứng bảo mật. Thành phần làm cứng Linux của EC2 Image Builder mở rộng các khả năng đã được chứng minh của nó cho AL2023, cung cấp quy trình cấu hình bảo mật hợp lý tương tự có sẵn cho các bản phân phối Linux khác. Để biết thêm thông tin, hãy tham khảo [tài liệu Image Builder](https://docs.aws.amazon.com/imagebuilder/latest/userguide/ib-stig.html).

## Tự động hóa STIG cho các đội tàu hiện có thông qua Systems Manager

Đối với các instance AL2023 EC2 hiện có, bạn có thể sử dụng các tài liệu lệnh SSM do AWS quản lý để tự động hóa việc triển khai các cấu hình STIG. Các tài liệu lệnh này có thể được thực thi thông qua bảng điều khiển SSM, API hoặc Giao diện dòng lệnh AWS (AWS CLI). Cơ chế chính ở đây là tài liệu lệnh Systems Manager do AWS quản lý, chứa các cấu hình STIG được xác định trước. Bằng cách tận dụng các tài liệu lệnh này thông qua các khả năng thực thi của Systems Manager, khách hàng có thể triển khai và duy trì một cách có hệ thống các cấu hình AL2023 STIG trên toàn bộ đội tàu instance EC2 của họ. Điều này tạo ra các đường cơ sở bảo mật nhất quán đáp ứng các yêu cầu của chính phủ và doanh nghiệp. Giải pháp này đặc biệt hiệu quả đối với các môi trường có các instance AL2023 EC2 hiện có vì nó cho phép khách hàng thực hiện các biện pháp kiểm soát STIG mà không cần xây dựng lại hoặc triển khai lại các instance. Để biết thêm thông tin về tài liệu lệnh, hãy tham khảo [Áp dụng cài đặt STIG với Systems Manager](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-ssm-cmd-doc.html) trong Hướng dẫn sử dụng EC2.

AL2023 STIG đại diện cho cam kết liên tục của Amazon Linux trong việc cung cấp cho khách hàng các công cụ và hướng dẫn bảo mật mà họ cần để thành công trong các môi trường được quy định chặt chẽ. Amazon Linux, phối hợp với DISA đang cung cấp cho khách hàng của họ quyền truy cập vào các cấu hình bảo mật có thẩm quyền, được chính phủ xác nhận đáp ứng các yêu cầu tuân thủ khắt khe nhất.

Sẵn sàng triển khai AL2023 STIG trong môi trường của bạn? Khám phá tài liệu toàn diện của chúng tôi và bắt đầu hành trình hợp lý hóa sự tuân thủ bảo mật của bạn ngay hôm nay. Để tìm hiểu thêm về làm cứng STIG cho các instance EC2 của bạn, hãy tham khảo [Tuân thủ STIG cho instance EC2 của bạn](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-configure-stig.html) và đối với các cài đặt STIG được áp dụng cho các instance EC2 Linux, hãy tham khảo [cài đặt STIG cho các instance EC2 Linux](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-settings.html#ec2-linux-os-stig). Để áp dụng cài đặt STIG cho instance AL 2023 EC2 của bạn, [tải xuống AL2023 DISA STIG](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-stig-downloads.html).
