---
title: "Blog 1"
date: ""
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Clario nâng cao chất lượng quy trình tạo tài liệu thử nghiệm lâm sàng với Amazon Bedrock

Bài viết này có đồng tác giả là Kim Nguyen và Shyam Banuprakash từ Clario.

Clario là nhà cung cấp hàng đầu các giải pháp endpoint data cho ngành công nghiệp thử nghiệm lâm sàng, tạo ra clinical evidence chất lượng cao cho các công ty dược phẩm và khoa học đời sống trong quá trình đưa liệu pháp mới đến với bệnh nhân. Từ khi thành lập hơn 50 năm trước, các giải pháp endpoint data của Clario đã hỗ trợ hơn 26.000 thử nghiệm lâm sàng, góp phần mang lại hơn 700 phê duyệt từ cơ quan quản lý trên hơn 100 quốc gia. Một trong những thách thức chính mà Clario phải đối mặt khi hỗ trợ khách hàng là quy trình tạo tài liệu thử nghiệm lâm sàng tốn rất nhiều thời gian, có thể kéo dài hàng tuần.


## Thách thức kinh doanh

Khi phân tích hình ảnh y tế là một phần của thử nghiệm lâm sàng, Clario chuẩn bị medical imaging charter process document (gọi tắt là Charter), trong đó nêu chi tiết format và yêu cầu cho việc central review hình ảnh thử nghiệm lâm sàng. Dựa trên Charter, nhóm imaging của Clario tạo ra một số tài liệu tiếp theo (như trong hình minh họa), bao gồm business requirement specification (BRS), training slides, và các tài liệu phụ trợ. Nội dung của các tài liệu này phần lớn được trích từ Charter nhưng cần định dạng lại và diễn đạt lại. Quy trình này tốn nhiều thời gian, dễ dẫn đến lỗi thủ công ngoài ý muốn, nguy cơ thông tin không nhất quán hoặc dư thừa, từ đó gây chậm trễ hoặc tác động tiêu cực đến thử nghiệm lâm sàng.

![docflow1](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2025/03/27/docflow1.png)

Nhóm imaging của Clario nhận thấy cần hiện đại hóa quy trình tạo tài liệu và tối ưu hóa workflow end-to-end. Clario đã hợp tác với AWS account team và AWS Generative AI Innovation Center để khám phá cách mà generative AI có thể giúp cải tiến quy trình này.

## Giải pháp

Nhóm AWS đã phối hợp chặt chẽ với Clario để phát triển một prototype solution sử dụng AWS AI services nhằm tự động hóa quy trình tạo BRS. Giải pháp bao gồm các dịch vụ chính sau:

- Amazon Simple Storage Service (Amazon S3): Dịch vụ lưu trữ đối tượng có khả năng mở rộng, được sử dụng để lưu trữ Charter-derived và các tài liệu BRS được sinh ra.

- Amazon OpenSearch Serverless: Cấu hình serverless theo nhu cầu của Amazon OpenSearch Service để dùng làm vector store.

- Amazon Bedrock: Amazon Bedrock là một dịch vụ fully managed cung cấp nhiều lựa chọn foundation models (FMs) hiệu năng cao từ các công ty AI hàng đầu thông qua một API duy nhất, cùng với đầy đủ các khả năng cần thiết để xây dựng ứng dụng generative AI với tính bảo mật, quyền riêng tư và trách nhiệm AI. Với Amazon Bedrock, bạn có thể thử nghiệm và đánh giá các FMs hàng đầu cho từng use case của mình, tùy chỉnh riêng tư với dữ liệu của bạn bằng các kỹ thuật như fine-tuning và Retrieval Augmented Generation (RAG), và xây dựng các agents có thể thực thi tác vụ trên hệ thống và dữ liệu doanh nghiệp của bạn.

Giải pháp được minh họa trong hình sau:

![architecture-2](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2025/03/27/architecture-2.png)

## Kiến trúc

1. Charter-derived documents được xử lý bằng script on-premises trước khi upload.

2. File được gửi đến AWS qua AWS Direct Connect.

3. Script chia nhỏ tài liệu (chunking) và gọi một embedding model để tạo ra document embeddings. Sau đó, embeddings được lưu trữ trong cơ sở dữ liệu vector OpenSearch để ứng dụng của chúng tôi có thể truy xuất. Clario sử dụng Amazon Titan Text Embeddings model được cung cấp bởi Amazon Bedrock. Mỗi chunk sẽ được gọi để sinh ra một embedding.

4. Amazon OpenSearch Serverless được dùng làm vector store lâu dài. Embeddings được lưu trong OpenSearch vector index, hỗ trợ tìm kiếm semantic relevant documents. Clario cũng lưu các attribute của tài liệu gốc và thử nghiệm tương ứng để tăng tính phong phú cho trải nghiệm tìm kiếm.

5. Custom build user interface (UI) là điểm truy cập chính cho người dùng để khởi tạo job sinh tài liệu và tương tác với chat UI. UI được tích hợp với workflow engine để quản lý quy trình.

6. Workflow engine gọi Amazon Bedrock API và điều phối quá trình sinh BRS. Cụ thể:

    - Sử dụng global specification để lưu prompt input cho LLM.

    - Query OpenSearch để tìm Charter liên quan.

    - Loop qua từng business requirement.

    - Gọi Claude 3.7 Sonnet LLM từ Amazon Bedrock để sinh response.

7. Xuất bản tài liệu business requirement specification ra giao diện người dùng, nơi business requirement writer có thể xem xét các câu trả lời để tạo ra tài liệu cuối cùng. Clario sử dụng Claude 3.7 Sonnet từ Amazon Bedrock cho tác vụ question-answering và ứng dụng conversational AI.

8. Các tài liệu cuối cùng được ghi vào Amazon S3 để được sử dụng và xuất bản bởi các document workflows bổ sung sẽ được xây dựng trong tương lai.

9. Một AI chat agent theo nhu cầu giúp khám phá tài liệu và cho phép người dùng trao đổi với một hoặc nhiều tài liệu.

## Lợi ích và kết quả

Bằng cách sử dụng các dịch vụ AWS AI, Clario đã đơn giản hóa đáng kể quy trình phức tạp trong việc tạo BRS. Giải pháp prototype đã chứng minh những lợi ích sau:

- Cải thiện độ chính xác: Sử dụng generative AI giảm thiểu lỗi dịch thuật và sự không nhất quán, giảm nhu cầu chỉnh sửa và hạn chế trễ tiến độ nghiên cứu.

- Khả năng mở rộng và linh hoạt: Kiến trúc serverless của AWS cho phép mở rộng liền mạch khi nhu cầu tăng, trong khi thiết kế modular giúp dễ dàng tích hợp với hệ thống khác của Clario.

- Bảo mật: Chiến lược bảo mật dữ liệu của Clario tập trung vào việc giới hạn toàn bộ thông tin trong hệ sinh thái AWS an toàn bằng cách sử dụng các tính năng bảo mật của Amazon Bedrock. Bằng cách giữ dữ liệu tách biệt trong hạ tầng AWS, Clario giúp đảm bảo khả năng bảo vệ trước các mối đe dọa bên ngoài và truy cập trái phép. Cách tiếp cận này cho phép Clario đáp ứng các yêu cầu tuân thủ và mang lại cho khách hàng sự tin tưởng về tính bảo mật và toàn vẹn của dữ liệu nhạy cảm.

## Bài học rút ra

Việc triển khai thành công giải pháp prototype này đã củng cố giá trị của việc sử dụng các generative AI models cho những ứng dụng chuyên biệt theo lĩnh vực, điển hình như trong ngành khoa học đời sống. Nó cũng nhấn mạnh tầm quan trọng của việc có sự tham gia của các business stakeholders ngay từ đầu và hiểu rõ giá trị kinh doanh cần đạt được. Sau thành công của dự án này, Clario đang tiến hành productionize giải pháp trong mảng Medical Imaging vào năm 2025 nhằm tiếp tục cung cấp các dịch vụ tiên tiến nhất cho khách hàng, với dữ liệu chất lượng cao và các thử nghiệm lâm sàng thành công.

## Kết luận

Sự hợp tác giữa Clario và AWS đã chứng minh tiềm năng của AWS AI/ML services và generative AI models (như Anthropic Claude) trong việc tối ưu hóa quy trình tạo tài liệu cho ngành khoa học đời sống, đặc biệt là các thử nghiệm lâm sàng phức tạp. Với công nghệ này, Clario đã nâng cao và đơn giản hóa quy trình tạo BRS, cải thiện cả độ chính xác lẫn khả năng mở rộng. Khi Clario tiếp tục mở rộng ứng dụng AI/ML trên toàn bộ hoạt động, công ty đang ở vị thế vững chắc để thúc đẩy đổi mới và mang lại kết quả tốt hơn cho khách hàng và bệnh nhân.

---

### Về các tác giả

Kim Nguyen là Giám đốc cấp cao phụ trách Data Science (Sr. Director of Data Science) tại Clario, nơi anh lãnh đạo một nhóm các nhà khoa học dữ liệu trong việc phát triển các giải pháp AI/ML sáng tạo cho ngành chăm sóc sức khỏe và thử nghiệm lâm sàng. Với hơn 10 năm kinh nghiệm trong quản lý và phân tích dữ liệu lâm sàng, Kim đã khẳng định chuyên môn của mình trong việc chuyển đổi dữ liệu phức tạp trong lĩnh vực khoa học đời sống thành insight có thể hành động giúp thúc đẩy kết quả kinh doanh. Sự nghiệp của anh bao gồm các vị trí lãnh đạo tại Clario và Gilead Sciences, nơi anh đi đầu trong các sáng kiến tự động hóa và chuẩn hóa dữ liệu trên nhiều nhóm chức năng. Kim có bằng Thạc sĩ Khoa học Dữ liệu và Kỹ thuật (Master’s in Data Science and Engineering) từ Đại học California, San Diego (UC San Diego) và bằng Cử nhân từ Đại học California, Berkeley, mang lại cho anh nền tảng kỹ thuật vững chắc để phát triển các mô hình dự đoán và chiến lược dựa trên dữ liệu. Hiện làm việc tại San Diego, California, anh tận dụng chuyên môn của mình để thúc đẩy các phương pháp tiên tiến trong lĩnh vực khoa học dữ liệu cho nghiên cứu lâm sàng.

Shyam Banuprakash là Phó Chủ tịch Cấp cao phụ trách Data Science và Delivery (Senior Vice President of Data Science and Delivery) tại Clario, nơi anh lãnh đạo các chương trình phân tích phức tạp và phát triển các giải pháp dữ liệu sáng tạo cho lĩnh vực medical imaging. Với gần 12 năm kinh nghiệm phát triển tại Clario, Shyam đã thể hiện khả năng lãnh đạo xuất sắc trong ra quyết định dựa trên dữ liệu và cải tiến quy trình kinh doanh. Chuyên môn của anh vượt ra ngoài vai trò chính, khi anh còn là Thành viên Hội đồng Tư vấn (Advisory Board Member) cho Modal và Chương trình Customer Experience của UC Irvine. Shyam có bằng Master of Advanced Study in Data Science and Engineering từ UC San Diego, cùng với khóa đào tạo chuyên sâu tại MIT về data science và big data analytics. Sự nghiệp của anh thể hiện sự giao thoa mạnh mẽ giữa chăm sóc sức khỏe, công nghệ và khoa học dữ liệu, giúp anh trở thành một thought leader trong việc tận dụng phân tích dữ liệu để chuyển đổi nghiên cứu lâm sàng và hình ảnh y học.

John O’Donnell là Principal Solutions Architect tại Amazon Web Services (AWS), nơi anh phụ trách tư vấn và thiết kế các giải pháp cloud-based phức tạp cho ngành Healthcare and Life Sciences (HCLS) ở cấp độ CIO. Với hơn 20 năm kinh nghiệm thực tế, anh đã có thành tích vững chắc trong việc mang lại giá trị và đổi mới cho khách hàng HCLS trên toàn cầu. Là một technical leader đáng tin cậy, John đã hợp tác với các nhóm AWS để đi sâu vào thách thức của khách hàng, đề xuất giải pháp, và đảm bảo các quá trình chuyển đổi lên cloud hiệu quả, có thể dự đoán và thành công. Anh đam mê hỗ trợ các khách hàng HCLS đạt được mục tiêu và đẩy nhanh quá trình hiện đại hóa theo hướng cloud-native.

Praveen Haranahalli là Senior Solutions Architect tại Amazon Web Services (AWS), nơi anh cung cấp tư vấn chuyên sâu và thiết kế các giải pháp cloud an toàn, có khả năng mở rộng cho nhiều khách hàng doanh nghiệp khác nhau. Với gần 20 năm kinh nghiệm trong lĩnh vực CNTT, trong đó hơn 10 năm chuyên về Cloud Computing, anh đã chứng minh năng lực trong việc triển khai các cloud transformation mang tính đột phá trên nhiều ngành công nghiệp. Là một cố vấn kỹ thuật đáng tin cậy, Praveen đã hợp tác thành công với khách hàng để xây dựng pipeline DevSecOps, thiết lập các security guardrails toàn diện, và phát triển các giải pháp AI/ML sáng tạo. Anh đam mê giải quyết các thách thức kinh doanh phức tạp thông qua kiến trúc cloud tiên tiến, giúp các tổ chức đạt được chuyển đổi số thành công dựa trên công nghệ trí tuệ nhân tạo và học máy.
