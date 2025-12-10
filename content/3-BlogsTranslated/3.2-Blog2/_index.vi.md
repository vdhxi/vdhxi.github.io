---
title: "Blog 2"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# Tối ưu hóa các workload nhạy cảm với độ trễ bằng thống kê NVMe chi tiết của Amazon EC2

Các instance Amazon Elastic Cloud Compute (Amazon EC2) với bộ lưu trữ NVMe gắn cục bộ có thể cung cấp hiệu năng cần thiết cho các workload đòi hỏi độ trễ cực thấp và thông lượng I/O cao. Các workload hiệu năng cao, từ các ứng dụng giao dịch tần suất cao và cơ sở dữ liệu in-memory đến các công cụ phân tích thời gian thực và suy luận AI/ML, đều cần khả năng theo dõi hiệu năng toàn diện. Các công cụ hệ điều hành như iostat và sar cung cấp những thông tin chi tiết có giá trị ở cấp độ hệ thống, và Amazon CloudWatch cung cấp các phép đo quan trọng về disk IOPs và thông lượng, nhưng các workload hiệu năng cao có thể hưởng lợi từ khả năng hiển thị chi tiết hơn nữa về hiệu năng của instance store.

Đối với các ứng dụng nhạy cảm với độ trễ mà mỗi mili-giây đều quan trọng, các công cụ giám sát hiệu năng nâng cao cung cấp khả năng hiển thị sâu vào các hệ thống lưu trữ, giúp các đội ngũ của bạn có thể theo dõi và phân tích hành vi ở độ chi tiết 1 giây. Thông tin chi tiết này có thể giúp tổ chức của bạn phát hiện nhanh chóng các điểm nghẽn, tinh chỉnh hiệu năng ứng dụng và cung cấp dịch vụ tin cậy.

Trong bài viết này, chúng tôi thảo luận về cách bạn có thể sử dụng thống kê hiệu năng chi tiết của Amazon EC2 cho các volume NVMe instance store, một tập hợp các chỉ số mới cung cấp độ chi tiết theo từng giây, để mang lại khả năng hiển thị thời gian thực vào hiệu năng lưu trữ gắn cục bộ của bạn. Các thống kê này tương tự như thống kê hiệu năng chi tiết của Amazon EBS, mang lại trải nghiệm giám sát nhất quán trên cả hai loại lưu trữ. Bạn có thể truy cập các thống kê này trực tiếp từ các thiết bị NVMe được gắn vào instance Amazon EC2 bằng cách sử dụng nvme-cli hoặc sử dụng CloudWatch agent để giám sát hiệu năng I/O ở cấp độ lưu trữ. Chúng tôi cũng cung cấp các ví dụ về cách sử dụng các thống kê này để xác định các điểm nghẽn hiệu năng.

## Tổng quan tính năng

Các instance dựa trên Amazon EC2 Nitro với bộ lưu trữ instance NVMe gắn cục bộ hiện cung cấp 11 chỉ số toàn diện ở độ chi tiết theo từng giây. Các chỉ số này, tương tự như các chỉ số volume EBS, bao gồm các phép đo độ dài hàng đợi (queue length), IOPS, dữ liệu thông lượng, và biểu đồ phân phối (histogram) độ trễ IO cho bộ lưu trữ instance NVMe gắn cục bộ. Ngoài ra, chúng cũng bao gồm các biểu đồ phân phối độ trễ cụ thể theo kích thước IO để cung cấp thông tin chi tiết hơn nữa về các mẫu hiệu năng của bộ lưu trữ instance NVMe cục bộ. Các chỉ số này được thu thập và trình bày riêng biệt cho từng volume NVMe riêng lẻ có sẵn trên một instance.

Các thống kê được trình bày dưới ba định dạng chính:
1. Các thống kê được trình bày dưới ba định dạng chính:
2. Độ dài hàng đợi thời gian thực, hiển thị giá trị hiện tại tại thời điểm bạn truy vấn
3. Biểu đồ phân phối độ trễ trực quan hóa sự phân bố của các hoạt động IO trên các phạm vi độ trễ khác nhau bằng cách hiển thị cả chế độ xem tích lũy và phân bố cụ thể theo kích thước IO

## Điều kiện tiên quyết

Để truy cập thống kê hiệu năng chi tiết cho bộ lưu trữ instance cục bộ, hãy hoàn thành các bước sau:
1. Khởi chạy một instance Amazon EC2 Nitro mới hoặc sử dụng một instance hiện có, sau đó kết nối với nó bằng SSH hoặc phương thức kết nối ưa thích của bạn.
2. Xác định thiết bị NVMe liên kết với bộ lưu trữ cục bộ để truy vấn thống kê hiệu năng. Ví dụ, bạn có thể chạy lệnh `nvme-cli` trong CLI để xuất ra tất cả các thiết bị NVMe trên instance.


```text
  bash
  $ sudo nvme list.
```


Sau đây là ví dụ đầu ra của lệnh list liệt kê các thiết bị NVMe trên instance và Serial Numbers (SN) của volume (đã được che trong đầu ra bên dưới vì lý do riêng tư). Trong minh họa này, hãy coi rằng bộ lưu trữ cục bộ được ứng dụng của bạn sử dụng là `/dev/nvme1n1`.

![](/images/blog-2/image-1.png)

3. Nếu bạn đang sử dụng Amazon Linux 2023 phiên bản 2023.8.20250915 (hoặc mới hơn) hoặc Amazon Linux 2 2.0.20251014.0 (hoặc mới hơn), bạn có thể chuyển sang Bước 4 vì `nvme-cli` sẽ sử dụng phiên bản mới nhất. Nếu bạn đang sử dụng phiên bản Amazon Linux cũ hơn, hãy cập nhật `nvme-cli` bằng lệnh sau, trong đó `2023.8.20250915` có thể được thay thế bằng phiên bản Amazon Linux 2023 mới nhất:

```text
  bash
  $ sudo dnf upgrade --releasever=2023.8.20250915
```
4. Chạy `nvme-cli`, với các quyền chính xác, và truyền thiết bị như một tham số. Bạn có thể sử dụng `--help` để xem chi tiết về cách sử dụng lệnh:
```text
  bash
  $ sudo nvme amzn stats --help
```
Ví dụ đầu ra:

![](/images/blog-2/image-2.png)

Nếu bạn thích đầu ra ở định dạng JSON, bạn có thể cung cấp tham số `-o json` cho lệnh.

```text
  bash
  $ sudo nvme amzn stats /dev/nvme1n1 -o json
```

Đầu ra sau đây (không có tham số -o json) hiển thị các hoạt động đọc/ghi tích lũy, số byte đọc/ghi, tổng thời gian xử lý (đọc và ghi tính bằng micro giây), và thời lượng (tính bằng micro giây) khi ứng dụng cố gắng vượt quá giới hạn IOPS/thông lượng của instance.

![](/images/blog-2/image-3.png)

Nó cũng hiển thị các biểu đồ phân phối độ trễ I/O đọc/ghi, với mỗi hàng đại diện cho các hoạt động I/O đã hoàn thành trong một khoảng thời gian cụ thể (tính bằng micro giây).

![](/images/blog-2/image-4-1.png)
![](/images/blog-2/image-4-2.png)

Nếu bạn muốn xem các biểu đồ phân phối độ trễ trên 5 dải IO khác nhau: (0, 512 Byte], (512B, 4KiB], (4KiB, 8KiB], (8KiB 32KiB], (32 KiB, MAX], bạn có thể cung cấp tham số `--details` hoặc `-d` cho lệnh:

```text
  bash
  $ sudo nvme amzn stats -d /dev/nvme1n
```

Hình ảnh sau đây là một đoạn trích từ đầu ra của lệnh trên, hiển thị các biểu đồ phân phối độ trễ bổ sung (đọc và ghi) của 5 dải IO khác nhau.

![](/images/blog-2/image-5-1.png)
![](/images/blog-2/image-5-2.png)
![](/images/blog-2/image-5-3.png)
![](/images/blog-2/image-5-4.png)
![](/images/blog-2/image-5-5.png)

Bạn có thể chạy lệnh stats ở độ chi tiết theo từng giây. Bạn cũng có thể viết script để lấy các thống kê theo khoảng thời gian mong muốn (mỗi giây hoặc bất kỳ thời lượng nào khác) với mỗi đầu ra tiếp theo phản ánh tổng số tích lũy cập nhật cho các chỉ số. Tính toán sự khác biệt trong các thống kê qua hai đầu ra cuối cùng cho phép bạn rút ra thông tin chi tiết về hồ sơ lưu trữ instance trong khoảng thời gian đó. Dưới đây là một script mẫu bạn có thể sử dụng để lấy các thống kê ở khoảng thời gian mặc định là 1 giây hoặc ở khoảng thời gian mong muốn của bạn.

```bash
  #!/bin/bash 
  # interval of 1 second 
  INTERVAL=${1:-1} 
  while true; do 
	echo "=== $(date) ===" 
	sudo nvme amzn stats /dev/nvme1 || break 
	echo 
	sleep $INTERVAL 
  done
```

Bạn có thể lưu script này, cấp quyền thực thi và chạy nó ở khoảng thời gian mặc định 1 giây hoặc cung cấp một khoảng thời gian tùy chỉnh khi thực thi script. Ví dụ, nếu bạn đã lưu script là `nvme_stats.sh`, 
bạn có thể sử dụng các lệnh sau để cấp quyền thực thi và chạy để lấy đầu ra ở khoảng thời gian mặc định 1 giây (giả sử bạn đang ở cùng thư mục với nvme_stats.sh).
```text
  chmod +x nvme_stats.sh
  ./nvme_stats.sh
```

Nếu, chẳng hạn, bạn muốn lấy đầu ra mỗi 5 giây, bạn có thể sử dụng lệnh bên dưới (sau khi cấp quyền thực thi cho script)
```text
  ./nvme_stats.sh 5
```

Bạn cũng có thể tích hợp với CloudWatch bằng cách sử dụng CloudWatch agent để thu thập và xuất bản các thống kê này để theo dõi lịch sử, trực quan hóa xu hướng thông qua dashboard, và các cảnh báo dựa trên hiệu năng để tương quan với các chỉ số ứng dụng và thông báo tự động cho các vấn đề hiệu năng.

## Rút ra thông tin chi tiết từ thống kê hiệu năng chi tiết NVMe instance store của Amazon EC2

Tương tự như [thống kê hiệu năng chi tiết của EBS](https://aws.amazon.com/blogs/storage/uncover-new-performance-insights-using-amazon-ebs-detailed-performance-statistics/), bạn có thể sử dụng thống kê NVMe instance store của Amazon EC2 để khắc phục các vấn đề hiệu năng workload khác nhau. Như đã đề cập trong phần trước, 
bạn cũng có thể sử dụng các thống kê chi tiết để xem các biểu đồ phân phối độ trễ I/O nhằm quan sát sự phân tán của độ trễ I/O trong khoảng thời gian đó. Bạn có thể sử dụng các thống kê hoạt động đọc/ghi và thời gian đã sử dụng để tính toán độ trễ trung bình. Các thống kê chi tiết hiển thị độ trễ trung bình ở độ chi tiết theo từng giây.

Hai kịch bản ví dụ tiếp theo minh họa phân tích hiệu năng chính bằng cách sử dụng các thống kê. Trong Kịch bản 1, chúng ta sẽ sử dụng chỉ số **EC2 Instance Local Storage Performance Exceeded (us)** để kiểm tra xem nhu cầu I/O có vượt quá khả năng lưu trữ của instance hay không, giúp định cỡ instance phù hợp cho hiệu năng ứng dụng I/O đầy đủ. 
Trong Kịch bản 2, chúng ta sẽ sử dụng các biểu đồ phân phối cụ thể theo kích thước IO (sử dụng `--details`) để chẩn đoán cách các ghi khối lớn ảnh hưởng đến hiệu năng đọc tiếp theo – một vấn đề thường bị ẩn bởi các số liệu tổng hợp của các công cụ giám sát truyền thống trên tất cả các kích thước IO.

### Kịch bản 1: Xác định khi các ứng dụng vượt quá giới hạn hiệu năng lưu trữ instance

Hiểu liệu nhu cầu I/O của ứng dụng của bạn có vượt quá khả năng của các volume instance store hay không là điều quan trọng để khắc phục sự cố hiệu năng. 
Khi các ứng dụng tạo ra các workload I/O liên tục cố gắng vượt quá giới hạn IOPS và thông lượng của các loại instance Amazon EC2 cụ thể, bạn sẽ gặp phải độ trễ tăng cao và hiệu năng bị suy giảm. 
Chỉ số **EC2 Instance Local Storage Performance Exceeded (us)** giúp xác định các kịch bản này bằng cách hiển thị thời lượng (tính bằng micro giây) khi các workload vượt quá hiệu năng instance được hỗ trợ. Giá trị khác không hoặc số lượng tăng lên giữa các ảnh chụp nhanh (snapshot) cho thấy kích thước hoặc loại instance hiện tại của bạn có thể không cung cấp đủ hiệu năng I/O cho ứng dụng của bạn.

Phần sau đây chỉ ra cách xác định xem một ứng dụng có đang gửi nhiều IOPS hơn mức bộ lưu trữ cục bộ của instance có thể hỗ trợ hay không.

Kịch bản ví dụ: Một ứng dụng trên instance i3en.xlarge hiển thị độ trễ ghi tăng cao >1ms. Bạn muốn xác định xem workload của ứng dụng có đang vượt quá hiệu năng được hỗ trợ của volume NVMe instance hay không.

1. **Chọn thiết bị NVMe Instance Storage bạn muốn phân tích** – Xác định instance bạn muốn phân tích cho ứng dụng đang gặp phải độ trễ tăng cao.
2. **Xác định thiết bị NVMe** – Sử dụng lệnh nvme-cli sau, và xác định thiết bị NVMe liên kết với bộ lưu trữ instance đó.

```bash
  $ sudo nvme list
```

Kịch bản ví dụ: Chúng tôi đã sử dụng lệnh list và xác định /dev/nvme1n1 là thiết bị NVMe liên kết với instance i3en.xlarge đang chạy ứng dụng hiện đang thấy độ trễ ghi tăng cao >1ms 
(trong khi độ trễ đọc là <50us theo điều kiện bình thường), vì vậy bây giờ chúng tôi muốn phân tích nó.

3. **Thu thập thống kê cho thiết bị tại một thời điểm hoặc tại các khoảng thời gian mong muốn** – Thu thập các thống kê hiệu năng chi tiết bằng lệnh nvme-cli hoặc sử dụng script mẫu được cung cấp 
trong phần trước để nắm bắt thống kê tại các khoảng thời gian mong muốn, nếu cần.

```bash
  $ sudo nvme amzn stats /dev/nvme1n1
```

Kịch bản ví dụ: Chúng tôi chọn thu thập thống kê chỉ một lần sau khi nhận thấy độ trễ ghi tăng cao của ứng dụng.

4. Phân tích các thống kê để kiểm tra xem ứng dụng có yêu cầu nhiều hơn hiệu năng được hỗ trợ của bộ lưu trữ instance hay không – Xác nhận sự tồn tại của sự suy giảm độ trễ I/O tổng thể bằng cách so sánh hai bộ biểu đồ phân phối độ trễ I/O đọc/ghi được thực hiện cách nhau một khoảng thời gian. Kịch bản ví dụ: Đầu ra sau đây hiển thị biểu đồ phân phối Read IO của bộ lưu trữ instance cục bộ NVMe được thực hiện cách nhau 40 giây không có vấn đề về độ trễ read IO (vì độ trễ đọc bình thường cho workload này là < 50 us).
   
Chỉ số được ghi lại tại thời điểm T:

![](/images/blog-2/image-6.png)

Chỉ số được ghi lại tại thời điểm T+40s:

![](/images/blog-2/image-7.png)

Đầu ra sau đây hiển thị biểu đồ phân phối Write IO được thực hiện cách nhau 40 giây. Chúng ta có thể nhận thấy rằng nhiều write IO rơi vào phạm vi độ trễ 1ms – 2ms, điều này không được mong đợi cho ứng dụng này.

Chỉ số được ghi lại tại thời điểm T:

![](/images/blog-2/image-8.png)

Chỉ số được ghi lại tại thời điểm T+40s:

![](/images/blog-2/image-9.png)

5. Phân tích chỉ số **EC2 Instance Local Storage Performance Exceeded (us)** hiển thị tổng thời gian (tính bằng micro giây) các yêu cầu IOPS vượt quá giới hạn volume. Lý tưởng nhất, số lượng tăng thêm của chỉ số này giữa hai thời điểm snapshot nên là tối thiểu, vì bất kỳ giá trị nào trên 0 đều chỉ ra rằng workload yêu cầu nhiều IOPS hơn mức volume có thể cung cấp. Kịch bản ví dụ: So sánh các chỉ số cách nhau 40 giây cho thấy rằng trong hơn 34 giây, nhu cầu IOPS của ứng dụng đã vượt qua IOPS 
được hỗ trợ bởi bộ lưu trữ instance cục bộ. Điều này giải thích độ trễ ghi tăng cao: IOPS dư thừa trên mức bộ lưu trữ cơ bản có thể xử lý vật lý sẽ xếp hàng các hoạt động, làm tăng thời gian chờ. Điều này chỉ ra rằng instance i3en.xlarge được chọn để chạy ứng dụng này không thể đáp ứng các yêu cầu hiệu năng của ứng dụng, gợi ý việc nâng cấp lên kích thước instance lớn hơn hoặc đánh giá lại chính loại instance đó.

Chỉ số được ghi lại tại thời điểm T:

![](/images/blog-2/image-10.png)

Chỉ số được ghi lại tại thời điểm T+40s:

![](/images/blog-2/image-11.png)

Điều quan trọng là phải có kích thước instance phù hợp để tránh các điểm nghẽn hiệu năng cho ứng dụng của bạn. Tham khảo [tài liệu về instance Amazon EC2](https://aws.amazon.com/ec2/instance-types/) để biết thêm thông tin về các instance khác nhau và kích thước lưu trữ của chúng.

### Kịch bản 2: Xác định kích thước khối gây ra độ trễ tăng cao trong các ứng dụng của bạn

Nhiều vấn đề hiệu năng lưu trữ phát sinh từ các tương tác phức tạp giữa các hoạt động đọc và ghi với các kích thước I/O khác nhau, mà các công cụ giám sát cấp hệ thống truyền thống như `iostat` hoặc `sar` không thể chẩn đoán hiệu quả do các số liệu tổng hợp của chúng trên tất cả các kích thước I/O. 
Thống kê hiệu năng chi tiết NVMe instance store EC2 giải quyết vấn đề này bằng cách cung cấp các biểu đồ phân phối độ trễ cụ thể theo kích thước I/O thông qua tùy chọn `--details` trong NVMe CLI. 
Các biểu đồ phân phối này hiển thị dữ liệu độ trễ cho các phạm vi kích thước I/O khác nhau: (0, 512 Byte], (512B, 4KiB], (4KiB, 8KiB], (8KiB, 32KiB], (32KiB, MAX], cho phép tương quan chính xác hơn giữa các mẫu workload ứng dụng và các chỉ số độ trễ cụ thể theo kích thước I/O để tối ưu hóa có mục tiêu.

Trong kịch bản ví dụ này, ứng dụng của bạn thực hiện các lần đọc nhỏ (thường <=4KiB, như đọc metadata) theo sau là các lần ghi lớn (>=32KiB) và hiển thị độ trễ đọc cao bất ngờ. Vấn đề phổ biến này xảy ra khi các lần ghi lớn ảnh hưởng đến hiệu năng của các hoạt động đọc tiếp theo, tạo ra hiệu ứng dây chuyền lên hiệu năng I/O tổng thể.

1. **Thu thập độ trễ IO đọc và ghi theo phạm vi kích thước** – Sử dụng NVMe CLI với tùy chọn `--details` để thu thập độ trễ IO đọc và ghi theo phạm vi kích thước:

```bash
    $ sudo nvme amzn stats /dev/nvme1n1 --details
```

2. **Xác nhận sự tồn tại của sự suy giảm độ trễ IO tổng thể** – Trong kịch bản ví dụ, kiểm tra độ trễ IO tổng thể, cả hoạt động đọc (trái) và ghi (phải) đều đang hiển thị độ trễ cao hơn mong đợi.

![](/images/blog-2/image-12-1.png)
![](/images/blog-2/image-12-2.png)

3. **Kiểm tra đầu ra cho các mẫu trên các dải kích thước IO khác nhau** – Phân tích độ trễ theo kích thước hoạt động cho thấy các hoạt động đọc nhỏ (512 byte đến 4K), thường nhanh, đang gặp phải các đợt tăng độ trễ bất ngờ trong khi các lần 
ghi lớn (32K+) hiển thị sự chậm trễ đáng kể. Các lần đọc nhỏ về lý thuyết nên duy trì hiệu năng tốt bất kể các hoạt động I/O khác.

![](/images/blog-2/image-13-1.png)
![](/images/blog-2/image-13-1.png)

Mẫu quan sát được chỉ ra rằng các hoạt động ghi lớn bị ứ đọng tạo ra sự tắc nghẽn toàn hệ thống, ảnh hưởng đến tất cả các hoạt động I/O thuộc mọi loại và kích thước. 
Mặc dù khả năng của hệ thống lưu trữ để xử lý các lần đọc nhỏ một cách hiệu quả, các lần ghi lớn đang xếp hàng làm chậm cả hoạt động đọc và ghi ở cấp độ ứng dụng.

Dựa trên phân tích này, chúng ta có thể thực hiện một số tối ưu hóa có mục tiêu cho ứng dụng, như sử dụng kích thước khối nhỏ hơn cho các hoạt động ghi khi có thể, 
hoặc gộp các lần ghi nhỏ thay vì thực hiện các lần ghi đơn lẻ lớn.

## Dọn dẹp

Nếu bạn đã tạo một instance Amazon EC2 với volume NVMe cho bài tập này, hãy chấm dứt và xóa instance thích hợp để tránh chi phí trong tương lai.

## Kết luận

[Thống kê hiệu năng chi tiết của Amazon EC2 cho instance store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/nvme-detailed-performance-stats.html) volume NVMe cung cấp giám sát hiệu năng lưu trữ thời gian thực, dưới một phút, tương tự như [thống kê hiệu năng chi tiết có sẵn cho các volume Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/nvme-detailed-performance-stats.html). Điều này cung cấp trải nghiệm giám sát nhất quán 
trên cả hai loại lưu trữ, với các biểu đồ phân phối độ trễ dựa trên kích thước IO bổ sung cho bộ lưu trữ instance để tối ưu hóa tốt hơn các mẫu I/O, và khắc phục sự cố hiệu quả hơn.

Để tìm hiểu thêm về các volume NVMe instance store của Amazon EC2, các kỹ thuật tối ưu hóa cho các workload nhạy cảm với độ trễ hoặc các chủ đề liên quan đến Amazon EC2 khác, hãy truy cập [trang tài liệu Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) hoặc khám phá các bài đăng khác trên AWS Storage Blog của chúng tôi về tối ưu hóa hiệu năng.

Chúng tôi rất muốn nghe cách bạn đang sử dụng các thống kê này để nâng cao workload của mình, hoặc nếu bạn có bất kỳ câu hỏi nào, trong phần bình luận bên dưới.
