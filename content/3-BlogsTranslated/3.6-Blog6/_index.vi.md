---
title: "Blog 6"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.6. </b> "
---

# Công bố AWS Well-Architected Generative AI Lens được cập nhật

Chúng tôi vui mừng thông báo bản cập nhật cho [AWS Well-Architected Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html). Bản cập nhật này có một số phần mới của Well-Architected Generative AI Lens, bao gồm các thực tiễn tốt nhất mới, hướng dẫn kịch bản nâng cao và các lời mở đầu được cải thiện về AI có trách nhiệm, kiến trúc dữ liệu và quy trình làm việc agentic.

AWS Well-Architected Framework cung cấp các thực tiễn kiến trúc tốt nhất để thiết kế và vận hành các workload [generative AI](https://aws.amazon.com/generative-ai/) trên AWS. Generative AI Lens sử dụng Well-Architected Framework để phác thảo các bước thực hiện đánh giá Well-Architected Framework cho các workload generative AI của bạn.

![](/images/blog-6/image-1.png)

Generative AI Lens cung cấp một cách tiếp cận nhất quán cho khách hàng để đánh giá các kiến trúc sử dụng các mô hình ngôn ngữ lớn (LLM) để đạt được các mục tiêu kinh doanh của họ. Lens này giải quyết các cân nhắc chung liên quan đến lựa chọn mô hình, kỹ thuật prompt, tùy chỉnh mô hình, tích hợp workload và cải tiến liên tục. Loại trừ cụ thể khỏi Generative AI Lens là các thực tiễn tốt nhất liên quan đến đào tạo mô hình và các kỹ thuật tùy chỉnh mô hình nâng cao. Chúng tôi xác định các thực tiễn tốt nhất giúp bạn kiến trúc các ứng dụng và workload dựa trên đám mây của mình theo các nguyên tắc thiết kế AWS Well-Architected được thu thập từ việc hỗ trợ hàng nghìn triển khai của khách hàng.

Generative AI Lens tham gia vào bộ sưu tập các Well-Architected lens được xuất bản dưới [AWS Well-Architected Lenses](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&awsm.page-wa-lens-whitepapers=1&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc). Để biết thêm thông tin về chính lens này, hãy xem [bài đăng thông báo ra mắt](https://aws.amazon.com/blogs/architecture/announcing-the-aws-well-architected-generative-ai-lens/).

## Có gì thay đổi trong Generative AI Lens được cập nhật?

Generative AI Lens được cập nhật kết hợp một số bổ sung mới để khách hàng xem xét. Những bổ sung này giữ cho lens bắt kịp với lĩnh vực generative AI đang phát triển nhanh chóng, giúp khách hàng cập nhật các thực tiễn kiến trúc tốt nhất.

### Hướng dẫn Amazon SageMaker HyperPod

Lens được cập nhật có hướng dẫn bổ sung cho người dùng [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/). SageMaker HyperPod là một dịch vụ lưu trữ và đào tạo mô hình có khả năng phục hồi cao mà bạn có thể sử dụng để điều phối các quy trình làm việc generative AI phức tạp, chạy lâu dài trên đám mây. Các quy trình làm việc này có thể là đào tạo trước mô hình nền tảng hoặc phục vụ suy luận mô hình ở quy mô lớn.

Chúng tôi rất vui mừng được thông báo hướng dẫn bổ sung cho khách hàng sử dụng SageMaker HyperPod trong Generative AI Lens. Hướng dẫn này được tích hợp vào các thực tiễn tốt nhất hiện có, mở rộng hướng dẫn cho các dịch vụ được bao gồm để bao gồm các khả năng của SageMaker. Hướng dẫn này tham gia vào hướng dẫn hiện có về [Amazon Bedrock](https://aws.amazon.com/bedrock/), [Amazon Q Business](https://aws.amazon.com/q/business/), [Amazon Q Developer](https://aws.amazon.com/q/developer/), và [Amazon SageMaker AI](https://aws.amazon.com/sagemaker/ai/).

### Lời mở đầu về Responsible AI
Lời mở đầu về AI có trách nhiệm được cập nhật hiện bao gồm một cuộc thảo luận chi tiết về tám khía cạnh cốt lõi của [AI có trách nhiệm](https://aws.amazon.com/ai/responsible-ai/) như được mô tả bởi AWS. Khách hàng hiện có thể tìm hiểu thêm về tám khía cạnh của các hệ thống AI được phát triển có trách nhiệm trực tiếp trong lens. Đây là bài đọc bắt buộc đối với khách hàng trong tất cả các giai đoạn của hành trình generative AI của họ.

### Lời mở đầu về kiến trúc dữ liệu
Lời mở đầu về kiến trúc dữ liệu được cập nhật xem xét các cân nhắc chiến lược liên quan đến kiến trúc dữ liệu hiện đại hỗ trợ các workload generative AI. Phần này cung cấp cho khách hàng cái nhìn về các quyết định và cân nhắc cấp cao cần thiết để kiến trúc một hệ thống dữ liệu phục vụ các workload generative AI.

### Lời mở đầu về Agentic AI
Mới đối với generative AI lens là lời mở đầu về agentic AI. Các hệ thống agentic, mặc dù về mặt kỹ thuật được phân loại là một tập hợp con của điện toán phân tán, đóng một vai trò quan trọng trong các workload generative AI hiện đại. Lời mở đầu này giới thiệu cho khách hàng một mẫu các mô hình kiến trúc phổ biến trong các hệ thống agentic được hỗ trợ bởi các mô hình nền tảng.

### Các kịch bản
Generative AI Lens hiện bao gồm tám kịch bản kiến trúc. Các kịch bản này bao gồm một loạt các ứng dụng kinh doanh được hỗ trợ bởi generative AI phổ biến, bao gồm các trung tâm cuộc gọi tự động, đồng nghiệp ảo cho nhân viên tri thức và các hệ thống dịch vụ generative AI đa thuê bao (multi-tenant). Phần kịch bản cung cấp hướng dẫn cụ thể để áp dụng các công nghệ generative AI cho các vấn đề kinh doanh phổ biến. Hình ảnh sau đây là một ví dụ về một trong những kịch bản mới hiện được bao gồm trong Generative AI Lens.

![](/images/blog-6/image-2.png)

## Ai nên sử dụng Generative AI Lens?
Generative AI Lens hữu ích cho nhiều vai trò. Các nhà lãnh đạo doanh nghiệp có thể sử dụng lens này để có được sự đánh giá rộng hơn về việc triển khai end-to-end và lợi ích của generative AI. Các nhà khoa học dữ liệu và kỹ sư có thể đọc lens này để hiểu cách sử dụng, bảo mật và thu được thông tin chi tiết từ dữ liệu của họ ở quy mô lớn. Các nhà lãnh đạo rủi ro và tuân thủ có thể hiểu cách generative AI được triển khai có trách nhiệm bằng cách cung cấp sự tuân thủ các yêu cầu quy định và quản trị.

## Các bước tiếp theo
[Well-Architected Generative AI Lens](https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html) được cập nhật hiện đã có sẵn. Sử dụng lens như một khuôn khổ để xác minh rằng các workload generative AI của bạn được kiến trúc với sự xuất sắc trong vận hành, bảo mật, độ tin cậy, hiệu quả hiệu năng, tối ưu hóa chi phí và tính bền vững trong tâm trí.

Nếu bạn cần hỗ trợ về việc triển khai hoặc đánh giá các workload generative AI của mình, vui lòng liên hệ với Kiến trúc sư Giải pháp AWS hoặc Đại diện Tài khoản của bạn.

Đặc biệt cảm ơn tất cả mọi người trong các cộng đồng Kiến trúc Giải pháp AWS, Dịch vụ Chuyên nghiệp AWS và Machine Learning đã đóng góp cho Generative AI Lens được cập nhật. Những đóng góp này bao gồm các quan điểm, chuyên môn, nền tảng và kinh nghiệm đa dạng trong việc phát triển AWS Well-Architected Generative AI Lens mới.

Để đọc thêm, hãy tham khảo [AWS Well-Architected Framework và các sách trắng về trụ cột](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc), hoặc sử dụng [AWS Well-Architected Machine Learning Lens](https://docs.aws.amazon.com/wellarchitected/latest/machine-learning-lens/machine-learning-lens.html) và lens tùy chỉnh của nó có thể truy cập từ AWS Well-Architected Tool.
