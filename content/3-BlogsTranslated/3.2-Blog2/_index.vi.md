---
title: "Blog 2"
date: ""
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# ChurnIQ AI-ssistant của Cleeng: Phân tích người đăng ký được hỗ trợ bởi Amazon Bedrock

*Bài viết này có đồng tác giả là Jakub Abramczyk, Nhà khoa học dữ liệu, Sebastian Boruch, Quản lý sản phẩm ChurnIQ và Kirstin White, Quản lý tiếp thị tăng trưởng từ Cleeng.*

Trong thị trường phát trực tuyến (D2C – Direct-to-Consumer) cạnh tranh khốc liệt, việc hiểu rõ hành vi người đăng ký là điều thiết yếu để tăng mức độ tương tác, tối ưu hóa nội dung và giảm tỷ lệ người dùng rời bỏ (churn). Theo Forbes, chi phí để có được khách hàng mới cao hơn gấp 5–7 lần so với việc giữ chân khách hàng hiện tại. Do đó, việc giữ chân khách hàng là điều cốt lõi đối với các doanh nghiệp đăng ký kỹ thuật số trong lĩnh vực truyền thông trực tuyến, thể thao, học trực tuyến, chăm sóc sức khỏe và podcasting. Thành công phụ thuộc vào việc phân tích hiệu quả chiến dịch, xác định khách hàng có nguy cơ rời bỏ và đưa ra các quyết định dựa trên dữ liệu nhằm duy trì lợi thế cạnh tranh và tối đa hóa doanh thu.
Truyền thống, việc trích xuất các thông tin chi tiết từ dữ liệu người đăng ký đòi hỏi đội ngũ nhà phân tích dữ liệu và các nhóm Business Intelligence (BI) chuyên môn cao. Sự phụ thuộc này thường gây ra các điểm nghẽn, làm chậm trễ phản ứng kịp thời trước các rủi ro churn. Việc mở rộng quyền truy cập dữ liệu xu hướng người đăng ký thông qua một trợ lý AI sinh ngữ là cách mà đối tác Amazon Web Services (AWS) – Cleeng – giải quyết thách thức này.

Cleeng đã xây dựng ChurnIQ AI-ssistant, được vận hành bởi Amazon Bedrock. Giải pháp AI sinh ngữ này cho phép các nhóm sử dụng các truy vấn bằng ngôn ngữ tự nhiên để phân tích dữ liệu người đăng ký phức tạp, loại bỏ nhu cầu về chuyên môn phân tích sâu. Người dùng có thể tạo các biểu đồ dữ liệu và khám phá xu hướng ngay lập tức, trao quyền cho các nhóm marketing, sản phẩm và giữ chân khách hàng thông qua khả năng phân tích tự phục vụ.
Chúng ta sẽ khám phá cách Cleeng xây dựng ChurnIQ AI-ssistant bằng cách sử dụng các dịch vụ AWS (bao gồm Amazon Bedrock, AWS Lambda và Amazon DynamoDB) để chuyển đổi dữ liệu thuê bao phức tạp thành các insight có thể hành động, giúp ra quyết định nhanh hơn và hiệu quả hơn.

## Giới thiệu về ChurnIQ AI-ssistant

![figure1](https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2025/03/26/ChurnIQ_AI-ssistant-image.png)

*Hình 1: Ảnh chụp giao diện của ChurnIQ AI-ssistant.*

ChurnIQ AI-ssistant là một thành phần mới sử dụng AI sinh ngữ trong ChurnIQ – sản phẩm phân tích nằm trong giải pháp Subscriber Retention Management® của Cleeng. Giải pháp này hợp nhất toàn bộ trải nghiệm người đăng ký trên nền tảng web và ứng dụng di động, giúp các công ty D2C đơn giản hóa quản lý đăng ký và tối ưu hóa giá trị vòng đời khách hàng.

Để giúp các nhóm nền tảng giảm thiểu tình trạng người dùng hủy đăng ký, ChurnIQ AI-ssistant cung cấp các truy vấn được định nghĩa sẵn cho các câu hỏi thường gặp, khả năng tùy chỉnh biểu đồ dễ dàng và tích hợp liền mạch với ChurnIQ Studio. Nền tảng này mang đến cái nhìn toàn diện về toàn bộ vòng đời của người đăng ký — từ đăng ký mới, chuyển đổi dùng thử, đến gia hạn và hủy đăng ký.

Các chỉ số quan trọng bao gồm khối lượng giao dịch, doanh thu theo gói ưu đãi và quốc gia, tỷ lệ khách hàng hủy đăng ký, giá trị vòng đời khách hàng (customer lifetime value), thay đổi gói đăng ký và kênh thu hút người dùng. Những chỉ số này giúp doanh nghiệp hiểu rõ xu hướng hiệu suất nền tảng, xu hướng doanh thu và hành vi của người dùng.

Để tạo biểu đồ, người dùng chỉ cần nhập câu hỏi của mình vào giao diện chatbot của ChurnIQ AI-ssistant và sẽ nhận được câu trả lời nhanh chóng, chính xác kèm theo biểu đồ dữ liệu trực quan. Những phản hồi và biểu đồ này cung cấp insight về hành vi người đăng ký, tỷ lệ hủy đăng ký và doanh thu. Sau đó, ChurnIQ AI-ssistant phân tích dữ liệu để phát hiện các xu hướng đáng lo ngại và kích hoạt các nhóm liên quan tiến hành phân tích sâu hơn nhằm khắc phục vấn đề.

Ngoài khả năng tự nhập câu hỏi, công cụ còn có các truy vấn định sẵn phổ biến như:

- Nguyên nhân chính dẫn đến churn là gì?

- Có bao nhiêu khách hàng đã hủy đăng ký trong tuần này?

- Tỷ lệ churn của người đăng ký gói hàng tháng là bao nhiêu?

- Có bao nhiêu khách hàng quay lại trong số người đăng ký mới?

- Tỷ lệ phần trăm đăng ký mới đến từ khách hàng quay lại là bao nhiêu?

## Kiến trúc AWS

![figure2](https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2025/03/25/ChurnIQ-Image-2-1.png)

*Hình 2: Kiến trúc AWS của ChurnIQ AI-ssistant do Cleeng phát triển.*

ChurnIQ AI-ssistant sử dụng các dịch vụ AWS như Amazon Bedrock – một dịch vụ được quản lý toàn phần cung cấp nhiều foundation models (FMs) hàng đầu cùng các khả năng cần thiết để xây dựng ứng dụng AI sinh ngữ.

Dưới đây là luồng xử lý của một truy vấn từ người dùng:

1. Người dùng mở ChurnIQ AI-ssistant và nhập truy vấn ngôn ngữ tự nhiên, ví dụ: “Cho tôi xem phân tích người dùng đã hủy đăng ký theo quốc gia.”


1. Truy vấn được gửi đến một Amazon API Gateway endpoint, từ đó gọi một AWS Lambda function.


1. Lambda kiểm tra Amazon DynamoDB để xem phản hồi cho truy vấn đó đã tồn tại hay chưa. Các prompt được cache trong DynamoDB trong 6 giờ để tăng tốc phản hồi và giảm chi phí cho các truy vấn lặp lại.


1. Nếu chưa có phản hồi, Lambda tiếp tục phân tích truy vấn và gọi Amazon Bedrock API với prompt đó.


1. Amazon Bedrock, sử dụng mô hình nền tảng Anthropic’s Claude, xử lý truy vấn và kiểm tra theo thiết lập Amazon Bedrock Guardrails để đảm bảo chỉ phản hồi các truy vấn liên quan đến chức năng của ChurnIQ. Amazon Bedrock tạo ra schema cần thiết để truy vấn các nguồn dữ liệu liên quan trong ChurnIQ bằng cách sử dụng prompt engineering được lập trình sẵn để tự động chọn cột và bộ lọc phù hợp.


1. ChurnIQ AI-ssistant hiển thị dashboard cho người dùng xem. Người dùng có thể tùy chỉnh biểu đồ bằng cách thay đổi bộ lọc, chỉ số, và các chiều dữ liệu. Người dùng cũng có thể lưu biểu đồ vào thư mục cá nhân.


1. Cuối cùng, người dùng có thể đưa phản hồi tích cực hoặc tiêu cực ngay trong giao diện AI-ssistant. Phản hồi này được gửi qua API Gateway, được phân tích bởi Lambda và lưu vào bảng DynamoDB. Thông tin phản hồi giúp nhóm sản phẩm Cleeng tinh chỉnh prompt và cải tiến chức năng.


## Kết quả và lợi ích

Cleeng chọn Amazon Bedrock nhờ khả năng cấu hình dễ dàng và tích hợp đơn giản với Amazon API Gateway, AWS Lambda, và Amazon DynamoDB. Sự tích hợp này giúp tăng tốc quá trình phát triển ChurnIQ AI-ssistant. Ngoài ra, Amazon Bedrock playgrounds cho phép so sánh các mô hình và phản hồi khác nhau, từ đó chọn ra mô hình tốt nhất một cách nhanh chóng.

Khi thử nghiệm nội bộ với khách hàng trước khi ra mắt, các lợi ích nổi bật bao gồm:


- Câu trả lời chính xác và tức thì cho các câu hỏi quan trọng về hành vi người đăng ký, tỷ lệ churn, và xu hướng doanh thu.


- Thông tin phân tích có thể hành động về chiến dịch thành công nhất và các phân khúc khách hàng có rủi ro cao.


- Gợi ý ý tưởng chiến dịch mới dựa trên hành vi người đăng ký để cải thiện sự hài lòng và lòng trung thành.


- Giảm tải công việc cho đội ngũ phân tích dữ liệu và BI, giúp họ tập trung vào các nhiệm vụ có giá trị cao hơn.


## Kết luận

Chúng tôi đã trình bày cách Cleeng tận dụng Amazon Bedrock để tích hợp ChurnIQ AI-ssistant, giúp các nền tảng đăng ký kỹ thuật số cải thiện khả năng phân tích dự đoán. Các insight hợp nhất này có thể chủ động giảm churn và tối ưu hóa customer lifetime value.

Tìm hiểu thêm về Cleeng’s ChurnIQ solution và AI-ssistant bằng cách xem interactive demo hoặc liên hệ với Sales Team. của họ.

Khám phá thêm các AWS Partners khác hoặc liên hệ với AWS Representative để tìm hiểu cách chúng tôi có thể giúp accelerate your business.

## Đọc thêm

- Bắt đầu với Amazon Bedrock


- Hướng dẫn phân tích dữ liệu khách hàng trên AWS


- AWS Media & Entertainment: Trực tiếp đến người tiêu dùng & phát trực tuyến

**Jason O'Malley**

Jason O’Malley là Sr. Partner Solutions Architect tại AWS, hỗ trợ các partners trong việc thiết kế media, communications, và technology industry solutions. Trước khi gia nhập AWS, Jason đã có 13 năm làm việc trong media and entertainment industry tại các công ty như Conan O’Brien’s Team Coco, WarnerMedia, và Media.Monks. Jason bắt đầu sự nghiệp trong television production và post-production trước khi xây dựng các media workloads on AWS. Khi không tạo ra các solutions cho partners và customers, Jason thường cùng vợ và con trai tham gia các chuyến phiêu lưu hoặc đọc sách về sustainability.

**Claudio Medeiros**

Claudio Medeiros là Principal Solutions Architect tại AWS với hơn 14 năm kinh nghiệm hỗ trợ các media và telecom companies đổi mới và xây dựng next-generation video platforms.

**Maggie Osude**

Maggie Osude là Solutions Architect tại AWS, hỗ trợ các enterprises trong việc tối ưu hóa và mở rộng cloud infrastructure. Cô thúc đẩy innovation trong media workflows, AI/ML, và cloud efficiency, giúp khách hàng xây dựng các scalable, high-performing solutions.
