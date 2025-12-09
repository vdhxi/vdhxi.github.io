---
title: "Blog 3"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Cách xuất dữ liệu sang Amazon S3 Tables bằng cách sử dụng AWS Step Functions Distributed Map

Các công ty chạy khối lượng công việc serverless thường cần thực hiện các hoạt động trích xuất, chuyển đổi và tải (ETL) trên các tệp dữ liệu được lưu trữ trong các bucket [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/). Mặc dù các phương pháp truyền thống như [AWS Lambda trigger cho Amazon S3](https://docs.aws.amazon.com/lambda/latest/dg/with-s3.html) hoặc [Amazon S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EventNotifications.html) có thể xử lý các hoạt động này, chúng có thể không đáp ứng được khi quy trình làm việc yêu cầu khả năng hiển thị, kiểm soát hoặc sự can thiệp của con người nâng cao. Ví dụ, một số quy trình có thể cần xem xét thủ công các bản ghi bị lỗi hoặc phê duyệt rõ ràng trước khi chuyển sang các giai đoạn tiếp theo. Các giải pháp điều phối tùy chỉnh cho những vấn đề này có thể trở nên phức tạp và dễ xảy ra lỗi.

[AWS Step Functions](https://aws.amazon.com/step-functions/) giải quyết những thách thức này bằng cách cung cấp khả năng quản lý và giám sát quy trình làm việc tích hợp. Tính năng [Step Functions Distributed Map](https://docs.aws.amazon.com/step-functions/latest/dg/state-map-distributed.html) được thiết kế cho các quy trình xử lý dữ liệu song song, thông lượng cao để các công ty có thể xử lý các công việc ETL phức tạp, [xử lý fan-out](https://aws.amazon.com/blogs/aws/new-step-functions-support-for-dynamic-parallelism/) và trực quan hóa dữ liệu ở quy mô lớn. Distributed Map xử lý từng mục dữ liệu như một quy trình làm việc con độc lập, xử lý hàng triệu bản ghi trong khi vẫn duy trì các kiểm soát đồng thời tích hợp, khả năng chịu lỗi và theo dõi tiến độ. Dữ liệu đã xử lý có thể được xuất liền mạch đến nhiều đích khác nhau, bao gồm [Amazon S3 Tables](https://aws.amazon.com/s3/features/tables/) với hỗ trợ Apache Iceberg.

Trong bài viết này, chúng tôi chỉ ra cách sử dụng Step Functions Distributed Map để xử lý các đối tượng Amazon S3 và xuất kết quả sang Amazon S3 Tables, tạo ra một đường ống xử lý dữ liệu có thể mở rộng và dễ bảo trì.

Xem [GitHub repository](https://github.com/aws-samples/sample-exporting-to-amazon-s3-tables-with-aws-step-functions-distributed-map) liên quan để biết hướng dẫn chi tiết về việc triển khai giải pháp này cũng như mã mẫu.

---

## Tổng quan giải pháp

Hãy xem xét một công ty điện tử tiêu dùng thường xuyên tham gia các triển lãm thương mại và hội nghị trong ngành. Trong các sự kiện này, những người tham dự quan tâm điền vào các biểu mẫu đăng ký bằng giấy để yêu cầu demo sản phẩm, nhận bản tin hoặc tham gia các chương trình truy cập sớm. Sau các sự kiện, đội ngũ của công ty quét hàng trăm nghìn biểu mẫu này và tải chúng lên Amazon S3. Thay vì xem xét thủ công từng biểu mẫu, công ty muốn tự động hóa việc trích xuất các chi tiết khách hàng chính như tên, địa chỉ email, địa chỉ gửi thư và các lĩnh vực quan tâm. Họ muốn lưu trữ dữ liệu có cấu trúc này trong S3 Tables với định dạng Apache Iceberg cho các phân tích downstream và nhắm mục tiêu chiến dịch tiếp thị.

Hãy xem cách giải pháp của bài viết này sử dụng Distributed Map để xử lý các tệp PDF song song, trích xuất dữ liệu bằng [Amazon Textract](https://aws.amazon.com/textract/) và ghi đầu ra đã làm sạch trực tiếp vào S3 Tables. Kết quả là quá trình onboard dữ liệu sau sự kiện có thể mở rộng, không máy chủ, như được hiển thị trong hình sau.

![](/static/images/blog-3/image-1.png)

Quy trình xử lý dữ liệu như được hiển thị trong sơ đồ trước bao gồm các bước sau:

1. Người dùng tải các biểu mẫu quan tâm của khách hàng dưới dạng PDF đã quét lên một bucket Amazon S3.
2. Một quy tắc [Amazon EventBridge Scheduler](https://docs.aws.amazon.com/eventbridge/latest/userguide/using-eventbridge-scheduler.html) kích hoạt theo các khoảng thời gian đều đặn, bắt đầu thực thi quy trình làm việc Step Functions.
3. Việc thực thi quy trình làm việc kích hoạt trạng thái Step Functions Distributed Map, liệt kê tất cả các tệp PDF đã tải lên Amazon S3 kể từ lần chạy trước.
4. Distributed Map lặp qua danh sách các đối tượng và chuyển metadata của từng đối tượng ([bucket, key, size, entity tag [ETag]](https://docs.aws.amazon.com/AmazonS3/latest/API/API_Object.html)) cho một thực thi quy trình làm việc con.
5. Đối với mỗi đối tượng, quy trình làm việc con gọi Amazon Textract với bucket và key được cung cấp để trích xuất văn bản thô và các trường liên quan (tên, địa chỉ email, địa chỉ gửi thư, lĩnh vực quan tâm) từ PDF.
6. Quy trình làm việc con gửi dữ liệu đã trích xuất đến [Amazon Data Firehose](https://aws.amazon.com/firehose/), được cấu hình để chuyển tiếp dữ liệu đến S3 Tables.
7. Firehose phân lô dữ liệu đến từ quy trình làm việc con và ghi nó vào S3 Tables theo khoảng thời gian được cấu hình trước mà bạn chọn.

Với dữ liệu hiện đã được cấu trúc và có thể truy cập trong S3 Tables, người dùng có thể dễ dàng phân tích chúng bằng các truy vấn SQL tiêu chuẩn với [Amazon Athena](https://aws.amazon.com/athena/) hoặc trí tuệ doanh nghiệp như [Amazon QuickSight](https://aws.amazon.com/quicksight/).

## Quy trình xử lý dữ liệu

EventBridge Scheduler bắt đầu các quy trình làm việc Step Functions mới theo các khoảng thời gian đều đặn. Dòng thời gian cho lịch trình này rất linh hoạt. Tuy nhiên, khi thiết lập lịch trình của bạn, hãy đảm bảo tần suất phù hợp với khoảng thời gian mà state machine của bạn được cấu hình để tìm kiếm các tệp PDF. Ví dụ: nếu state machine của bạn kiểm tra các tệp PDF từ tuần trước, bạn sẽ muốn lên lịch chạy hàng tuần. Quy trình làm việc Step Functions sau đó thực hiện ba bước sau (lưu ý rằng các bước này là các bước 4, 5, 6 và 7 trong sơ đồ quy trình làm việc trước đó):

1. Trích xuất dữ liệu người dùng liên quan từ các tệp PDF.
2. Gửi dữ liệu người dùng đã trích xuất đến Firehose.
3. Ghi dữ liệu vào S3 Tables ở định dạng bảng Apache Iceberg.

Sơ đồ sau minh họa quy trình làm việc này.

![](/static/images/blog-3/image-2.png)

Hãy xem xét từng bước của quy trình làm việc trước đó chi tiết hơn.

## Trích xuất dữ liệu người dùng liên quan từ tài liệu PDF

Step Functions sử dụng Distributed Map để xử lý các tệp PDF đồng thời trong các quy trình làm việc con song song. Nó chấp nhận đầu vào từ [JSON](https://aws.amazon.com/documentdb/what-is-json/), [JSONL](https://jsonlines.org/), CSV, tệp Parquet, tệp kê khai Amazon S3 được lưu trữ trong Amazon S3 (được sử dụng để chỉ định các tệp cụ thể để xử lý) hoặc [Amazon S3 bucket prefix](https://docs.aws.amazon.com/firehose/latest/dev/dynamic-partitioning-s3bucketprefix.html) (cho phép lặp qua metadata tệp cho tất cả các đối tượng dưới prefix đó). Step Functions tự động xử lý việc song song hóa bằng cách chia nhỏ tập dữ liệu và chạy các quy trình làm việc con cho từng mục, với trường [ItemBatcher](https://docs.aws.amazon.com/step-functions/latest/dg/input-output-itembatcher.html) cho phép nhóm nhiều tệp PDF vào một lần thực thi quy trình làm việc con duy nhất (ví dụ: 10 tệp PDF mỗi lô) để tối ưu hóa hiệu suất và chi phí.

Ảnh chụp màn hình sau của bảng điều khiển Step Functions hiển thị cấu hình cho Distributed Map. Ví dụ: chúng tôi đã cấu hình Distributed Map để xử lý 10 tệp PDF quan tâm của khách hàng trong một quy trình làm việc con duy nhất.

![](/static/images/blog-3/image-3.png)

Hình ảnh sau đây hiển thị một ví dụ về các tệp PDF được quét này, bao gồm thông tin khách hàng mà giải pháp của bài viết này xử lý.

![](/static/images/blog-3/image-4.png)

Mỗi quy trình làm việc con sau đó gọi [Amazon Textract AnalyzeDocument API](https://docs.aws.amazon.com/textract/latest/dg/API_AnalyzeDocument.html) với các truy vấn cụ thể để trích xuất thông tin khách hàng.

```text
{
  "Document": {
    "S3Object": {
      "Bucket": "<input PDFs bucket>",
      "Name": "{% $states.input.Key %}"
    }
  },
  "FeatureTypes": [
    "QUERIES"
  ],
  "QueriesConfig": {
    "Queries": [
      {
        "Alias": "full_name",
        "Text": "What is the customer's name?"
      },
      {
        "Alias": "phone_number",
        "Text": "What is the customer’s phone number?"
      },
      {
        "Alias": "mailing_address",
        "Text": "What is the customer’s mailing address?"
      },
      {
        "Alias": "interest",
        "Text": "What is the customer’s interest?"
      }
    ]
  }
}
```
API phân tích từng tệp PDF được quét và trả về cấu trúc JSON chứa thông tin khách hàng đã trích xuất.

## Gửi dữ liệu người dùng đã trích xuất đến Firehose

Quy trình làm việc con sau đó sử dụng [hành động Firehose PutRecordBatch API](https://docs.aws.amazon.com/firehose/latest/APIReference/API_PutRecordBatch.html) với [tích hợp dịch vụ](https://docs.aws.amazon.com/step-functions/latest/dg/integrate-services.html) để xếp hàng thông tin khách hàng đã trích xuất để xử lý thêm. Yêu cầu hành động PutRecordBatch bao gồm tên luồng Firehose và các bản ghi dữ liệu. Các bản ghi dữ liệu bao gồm một blob dữ liệu từ bước 1 chứa thông tin khách hàng đã trích xuất, như được hiển thị trong ví dụ sau.

```text
{
  "DeliveryStreamName": "put_raw_form_data_100",
  "Records": [
    {
      "Data": "{\"full_name\":\"Anthony Ayala\",\"phone_number\":\"001-384-925-0701\",\"mailing_address\":\"38548 Joshua Wall Suite 974, East Heatherfort, OH 32669\",\"interest\":\"Fitness Trackers\",\"processed_date\":\"2025-05-01\"}"
    },
    {
      "Data": "{\"full_name\":\"Becky Williams\",\"phone_number\":\"+1-283-499-2466\",\"mailing_address\":\"227 King Forge Suite 241, East Nathanland, PR 05687\",\"interest\":\"Al Assistants\",\"processed_date\":\"2025-05-01\"}"
    }
  ]
}
```

## Ghi dữ liệu vào S3 Tables ở định dạng bảng Apache Iceberg

Firehose quản lý hiệu quả việc đệm dữ liệu, chuyển đổi định dạng và phân phối đáng tin cậy đến nhiều đích khác nhau, bao gồm Apache Iceberg, tệp thô trong Amazon S3, [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/), hoặc [bất kỳ đích nào khác được hỗ trợ](https://docs.aws.amazon.com/firehose/latest/dev/create-destination.html). Các bảng Apache Iceberg có thể được tự quản lý trong Amazon S3 hoặc được lưu trữ trong S3 Tables. Mặc dù các bảng Iceberg tự quản lý yêu cầu tối ưu hóa thủ công—chẳng hạn như nén và hết hạn snapshot—S3 Tables tự động tối ưu hóa lưu trữ cho khối lượng công việc phân tích quy mô lớn, cải thiện hiệu suất truy vấn và giảm chi phí lưu trữ.

Firehose đơn giản hóa quá trình truyền dữ liệu bằng cách cấu hình luồng phân phối, chọn nguồn dữ liệu và đặt bảng Iceberg làm đích. Sau khi bạn thiết lập xong, luồng Firehose đã sẵn sàng để phân phối dữ liệu. Dữ liệu được phân phối có thể được truy vấn từ S3 Tables bằng cách sử dụng Athena, như được hiển thị trong ảnh chụp màn hình sau của bảng điều khiển Athena.

![](/static/images/blog-3/image-5.png)

Kết quả truy vấn bao gồm tất cả dữ liệu khách hàng đã xử lý từ các tệp PDF, như được hiển thị trong ảnh chụp màn hình sau.

![](/static/images/blog-3/image-6.png)

Sự tích hợp này thể hiện một giải pháp mạnh mẽ, không cần mã để chuyển đổi các biểu mẫu PDF thô thành dữ liệu có thể truy vấn, phong phú trong bảng Iceberg. Bạn có thể sử dụng dữ liệu này để phân tích thêm.

## Kết luận

Trong bài viết này, chúng tôi đã chỉ ra cách xây dựng một giải pháp có thể mở rộng, không máy chủ để xử lý tài liệu PDF và xuất dữ liệu đã trích xuất sang S3 Tables bằng cách sử dụng Step Functions Distributed Map. Kiến trúc này mang lại một số lợi ích chính như độ tin cậy, hiệu quả chi phí, khả năng hiển thị và khả năng bảo trì. Bằng cách tận dụng các dịch vụ AWS như Step Functions, Amazon Textract, Firehose và S3 Tables, các công ty có thể tự động hóa quy trình xử lý tài liệu của họ trong khi đảm bảo hiệu suất tối ưu và sự xuất sắc trong vận hành. Giải pháp này có thể được điều chỉnh cho nhiều trường hợp sử dụng khác ngoài các biểu mẫu quan tâm của khách hàng, chẳng hạn như xử lý hóa đơn, biểu mẫu đăng ký hoặc bất kỳ kịch bản nào yêu cầu trích xuất dữ liệu có cấu trúc từ tài liệu ở quy mô lớn.

Mặc dù ví dụ này tập trung vào việc xử lý dữ liệu PDF và ghi vào S3 Tables, Distributed Map có thể xử lý nhiều nguồn đầu vào khác nhau bao gồm JSON, JSONL, CSV và tệp Parquet trong Amazon S3; các mục trong bảng [Amazon DynamoDB](https://aws.amazon.com/dynamodb/); kết quả truy vấn Athena; và tất cả các AWS List API được phân trang. Tương tự, thông qua [tích hợp dịch vụ Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/integrate-services.html), bạn có thể ghi kết quả đến nhiều đích như [bảng DynamoDB bằng cách sử dụng tích hợp dịch vụ PutItem](https://docs.aws.amazon.com/step-functions/latest/dg/connect-ddb.html).

Để bắt đầu với giải pháp này, hãy xem [GitHub repository](https://github.com/aws-samples/sample-exporting-to-amazon-s3-tables-with-aws-step-functions-distributed-map) liên quan để biết hướng dẫn triển khai và mã mẫu.
