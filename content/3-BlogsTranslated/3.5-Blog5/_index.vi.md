---
title: "Blog 5"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.5. </b> "
---

# Kiến tạo sự xuất sắc của AI: AWS ra mắt ba Well-Architected Lenses tại re:Invent 2025

Tại [re:Invent 2025](https://reinvent.awsevents.com/?trk=03c58d4a-be5e-48b5-a705-eb2be9b88efa&sc_channel=em), chúng tôi giới thiệu một lens mới và hai bản cập nhật quan trọng cho [AWS Well-Architected Lenses](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&awsm.page-wa-lens-whitepapers=1&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) tập trung đặc biệt vào các workload AI: Responsible AI Lens, Machine Learning (ML) Lens, và Generative AI Lens. Cùng với nhau, các lens này cung cấp hướng dẫn toàn diện cho các tổ chức ở các giai đoạn khác nhau trong hành trình AI của họ, cho dù bạn mới bắt đầu thử nghiệm với machine learning hay đã triển khai các ứng dụng AI phức tạp ở quy mô lớn.

[AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html?refid=cr_card) cung cấp các thực tiễn kiến trúc tốt nhất để thiết kế và vận hành các workload tin cậy, an toàn, hiệu quả về hiệu năng, tối ưu hóa chi phí và bền vững trên đám mây.

## Responsible AI Lens: Nhúng niềm tin vào các hệ thống AI

[Responsible AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/responsible-ai-lens/responsible-ai-lens.html) cung cấp một cách tiếp cận có cấu trúc cho các nhà phát triển để đánh giá và theo dõi các workload AI của họ dựa trên các thực tiễn tốt nhất đã được thiết lập, xác định các lỗ hổng tiềm ẩn trong việc triển khai AI của họ và nhận hướng dẫn khả thi để cải thiện chất lượng và sự phù hợp của hệ thống AI với các nguyên tắc AI có trách nhiệm. Bằng cách sử dụng Responsible AI Lens, bạn có thể đưa ra các quyết định sáng suốt cân bằng giữa các yêu cầu kinh doanh và kỹ thuật, đẩy nhanh con đường từ thử nghiệm AI đến các giải pháp sẵn sàng cho sản xuất.

Những điểm chính từ Responsible AI Lens:
- **Mọi hệ thống AI đều có cân nhắc về Responsible AI**: Cho dù được thiết kế có chủ ý hay không, các hệ thống AI vốn dĩ mang theo những tác động về Responsible AI cần được quản lý tích cực thay vì phó mặc cho may rủi.
- **Các hệ thống AI có thể được sử dụng ngoài mục đích ban đầu và có thể có những tác động không mong muốn**: Các ứng dụng thường được sử dụng theo những cách mà các nhà phát triển không lường trước được, và do bản chất xác suất của chúng, các hệ thống AI có thể tạo ra các kết quả bất ngờ ngay cả trong các trường hợp sử dụng đã định, khiến các quyết định Responsible AI mạnh mẽ trở nên cần thiết ngay từ đầu.
- **Responsible AI là yếu tố thúc đẩy đổi mới và niềm tin**: Thay vì là một sự ràng buộc, các thực tiễn Responsible AI có thể thúc đẩy đổi mới bằng cách chủ động xây dựng niềm tin của các bên liên quan và khách hàng và giảm thiểu rủi ro downstream.

Responsible AI Lens đóng vai trò là hướng dẫn nền tảng cho các hoạt động phát triển AI, cung cấp các hướng dẫn quan trọng thông báo cho cả việc triển khai Machine Learning Lens và Generative AI Lens.

## Machine Learning Lens: Nền tảng cho các workload ML

[Machine Learning Lens](https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html) cung cấp cho bạn một bộ các thực tiễn tốt nhất không phụ thuộc vào đám mây đã được thiết lập dưới dạng các trụ cột Well-Architected Framework cho từng giai đoạn vòng đời machine learning (ML). Machine Learning Lens được cập nhật cung cấp một cách tiếp cận nhất quán để thiết kế, xây dựng và vận hành các workload machine learning trên AWS. Nó giải quyết toàn bộ các workload ML, từ học có giám sát và không giám sát truyền thống đến các ứng dụng AI hiện đại.

Machine Learning Lens được cập nhật kết hợp các khả năng AWS ML mới nhất (đã phát triển kể từ khi được giới thiệu vào năm 2023). Có gì mới trong ML Lens được cập nhật:
- Các quy trình làm việc cộng tác dữ liệu và AI được nâng cao thông qua Amazon SageMaker Unified Studio.
- Phát triển được hỗ trợ bởi AI để tạo mã và nâng cao năng suất.
- Cơ sở hạ tầng đào tạo phân tán để phát triển và tinh chỉnh mô hình nền tảng với Amazon SageMaker HyperPod.
- Các khả năng tùy chỉnh mô hình như chưng cất kiến thức và tinh chỉnh các ứng dụng cụ thể theo miền bằng cách sử dụng Amazon Bedrock với Kiro và Amazon Q Developer.
- Phát triển ML không cần mã (no-code) sử dụng Amazon SageMaker Canvas với tích hợp Amazon Q.
- Phát hiện thiên kiến được cải thiện với các chỉ số công bằng nâng cao và các khả năng Responsible AI trong Amazon SageMaker Clarify.
- Tạo bảng điều khiển tự động cho thông tin chi tiết về kinh doanh thông qua Amazon Quick Sight.
- Kiến trúc suy luận mô-đun để triển khai mô hình linh hoạt với Inference Components.
- Khả năng quan sát nâng cao với các khả năng gỡ lỗi và giám sát được cải thiện trong suốt vòng đời ML.
- Tối ưu hóa chi phí nâng cao cho quản lý tài nguyên thông qua Amazon SageMaker Training Plans, Savings Plans, và hỗ trợ Spot Instance.

Bạn có thể sử dụng ML Lens bất kể bạn đang ở đâu trên hành trình đám mây của mình. Bạn có thể chọn áp dụng hướng dẫn này trong quá trình thiết kế các workload ML của mình hoặc sau khi các workload của bạn đã đi vào sản xuất như một phần của quy trình cải tiến liên tục. Những cải tiến này được hỗ trợ bởi các dịch vụ AWS chính bao gồm Amazon SageMaker Unified Studio, Amazon Q, Amazon SageMaker HyperPod, và Amazon Bedrock.

## Generative AI Lens: Hướng dẫn chuyên biệt cho các mô hình nền tảng

[Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html?did=wp_card&trk=wp_card) cung cấp một cách tiếp cận nhất quán cho khách hàng để đánh giá các kiến trúc sử dụng các mô hình ngôn ngữ lớn (LLM) để đạt được các mục tiêu kinh doanh của họ. Lens này giải quyết các cân nhắc chung liên quan đến lựa chọn mô hình, kỹ thuật prompt, tùy chỉnh mô hình, tích hợp workload và cải tiến liên tục. Chúng tôi xác định các thực tiễn tốt nhất giúp bạn kiến trúc các ứng dụng và workload dựa trên đám mây của mình theo các nguyên tắc thiết kế AWS Well-Architected được thu thập từ việc hỗ trợ hàng nghìn triển khai của khách hàng. Trong khi Machine Learning (ML) Lens bao gồm phạm vi rộng lớn của các workload ML, Generative AI Lens tập trung cụ thể vào các mô hình nền tảng và các ứng dụng generative AI. Generative AI Lens cung cấp các thực tiễn kiến trúc tốt nhất để thiết kế và vận hành các workload generative AI trên AWS.

Generative AI Lens được cập nhật bao gồm một số bổ sung mới:
- Hướng dẫn Amazon SageMaker HyperPod để điều phối các quy trình làm việc generative AI phức tạp, chạy lâu dài bao gồm các khả năng dịch vụ bổ sung.
- Lời mở đầu về Responsible AI được nâng cao với thảo luận chi tiết về tám khía cạnh cốt lõi của Responsible AI như được mô tả bởi AWS.
- Lời mở đầu về kiến trúc dữ liệu được cập nhật với các cân nhắc chiến lược cần thiết để kiến trúc một hệ thống dữ liệu cho các workload generative AI.
- Lời mở đầu về agentic AI mới giới thiệu các mô hình kiến trúc cho các hệ thống agentic.
- Tám kịch bản kiến trúc bao gồm các ứng dụng kinh doanh được hỗ trợ bởi generative AI phổ biến như trung tâm cuộc gọi tự động, đồng nghiệp ảo cho nhân viên tri thức và các hệ thống dịch vụ generative AI đa thuê bao (multi-tenant).

Generative AI Lens xây dựng dựa trên nền tảng được thiết lập bởi ML Lens, cung cấp hướng dẫn chuyên biệt cho những thách thức và cơ hội độc đáo được trình bày bởi các mô hình nền tảng và các ứng dụng generative AI.

## Chiến lược triển khai cho hướng dẫn Well-Architected AI/ML: Một cách tiếp cận thống nhất

Các lens mới – Responsible AI Lens, Machine Learning Lens, và Generative AI Lens – làm việc cùng nhau để cung cấp hướng dẫn toàn diện cho phát triển AI. Responsible AI Lens hướng dẫn phát triển AI an toàn, công bằng và bảo mật. Nó giúp cân bằng nhu cầu kinh doanh với các yêu cầu kỹ thuật, hợp lý hóa quá trình chuyển đổi từ thử nghiệm sang sản xuất. Machine Learning Lens hướng dẫn các tổ chức đánh giá các workload trên cả các phương pháp tiếp cận AI hiện đại và machine learning truyền thống. Các cập nhật gần đây tập trung vào các lĩnh vực chính bao gồm các quy trình làm việc cộng tác dữ liệu và AI được nâng cao, các khả năng phát triển được hỗ trợ bởi AI, cung cấp cơ sở hạ tầng quy mô lớn và triển khai mô hình có thể tùy chỉnh. Generative AI Lens giúp khách hàng đánh giá các kiến trúc dựa trên mô hình ngôn ngữ lớn (LLM) và các cập nhật của nó bao gồm hướng dẫn cho người dùng Amazon SageMaker HyperPod, thông tin chi tiết mới về agentic AI và các kịch bản kiến trúc được cập nhật.

## Các bước tiếp theo là gì?

Việc ra mắt các lens mới này tại re:Invent 2025 giúp các tổ chức xây dựng các hệ thống AI có trách nhiệm, đáng tin cậy, mạnh mẽ và hiệu quả. Bằng cách cung cấp hướng dẫn toàn diện trên toàn bộ phạm vi của các workload AI, AWS hỗ trợ các tổ chức đẩy nhanh các sáng kiến AI của họ trong khi vẫn duy trì các tiêu chuẩn cao nhất về AI có trách nhiệm và sự xuất sắc về kỹ thuật.

Tìm hiểu thêm về AWS Well-Architected Framework và triển khai hướng dẫn thực tiễn tốt nhất được cung cấp bằng cách sử dụng [GitHub repository](https://github.com/aws-samples/sample-well-architected-custom-lens). Các lens này là các công cụ thực tế được thiết kế để giúp bạn xây dựng các hệ thống AI mang lại giá trị kinh doanh thực sự trong khi vẫn duy trì các tiêu chuẩn cao nhất về đạo đức, bảo mật và sự xuất sắc trong vận hành.

Để đọc thêm, hãy tham khảo [AWS Well-Architected Framework và các sách trắng về trụ cột](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc), hoặc liên hệ với Kiến trúc sư Giải pháp AWS hoặc Đại diện Tài khoản của bạn để được hỗ trợ triển khai các lens này trong tổ chức của bạn.
