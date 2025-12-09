---
title: "Blog 3"
date: ""
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tiết kiệm chi phí điện toán đám mây: 10 mẹo dành cho các tổ chức học thuật

![figure1](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/04/10/AWS-Public-Sector-Blog-Featured-Images-Blog-Header-static-template-Autosaved-13.png)

Khi sử dụng dịch vụ điện toán đám mây, một trong những lợi ích chính là khả năng điều chỉnh tài nguyên theo nhu cầu – và tránh phải mua sắm vượt mức cần thiết. Điều này trái ngược với mô hình truyền thống sử dụng thiết bị tại chỗ (on-premises), nơi tài nguyên thường được cấu hình để đáp ứng mức sử dụng cao nhất dự đoán trước trong suốt vòng đời thiết bị. Khái niệm cốt lõi này của cloud đôi khi bị bỏ qua khi các tổ chức mới chuyển sang môi trường đám mây, và họ vẫn tiếp tục hành xử như thể đang bị ràng buộc trong một hạ tầng cố định.

Đối với các tổ chức giáo dục đang tận dụng dịch vụ điện toán đám mây, điều quan trọng là cần chủ động quản lý và tối ưu hóa chi phí cloud. Mặc dù nội dung dưới đây hướng đến người dùng trong giáo dục đại học, nhiều điểm cũng hữu ích với các đối tượng khác.

Dưới đây là 10 mẹo giúp kiểm soát chi phí cloud khi sử dụng Amazon Web Services (AWS):


## 1. Thiết lập cảnh báo ngân sách AWS

Sử dụng AWS Budgets để thiết lập cảnh báo, đặc biệt với các khoản chi bất thường. Điều này giúp bạn theo dõi sát mức sử dụng và tránh các cú sốc chi phí bất ngờ.

Việc này đặc biệt hữu ích nếu bạn đang tận dụng Free Tier và muốn đảm bảo không bị tính phí sau khi hết hạn.

Hướng dẫn tạo ngân sách có thể tham khảo tại đây.


## 2. Tối ưu hóa kích thước tài nguyên

Xác định các tài nguyên đang sử dụng không hiệu quả, như các instance Amazon EC2, Amazon RDS, hoặc các volume Amazon EBS được cung cấp quá mức cần thiết. Cân nhắc giảm kích thước hoặc chuyển sang các loại instance thay thế, như instance EC2 sử dụng Graviton, để tối ưu chi phí. Người dùng có AWS Support ở cấp Business hoặc Enterprise có thể sử dụng AWS Trusted Advisor để nhận khuyến nghị về tối ưu hóa tài nguyên.

AWS Compute Optimizer cũng là một công cụ hữu ích, giúp đánh giá EC2, nhóm Auto Scaling, EBS volumes, AWS Lambda functions, RDS databases, và dịch vụ Amazon ECS trên AWS Fargate. Sau khi kích hoạt Compute Optimizer, bạn có thể truy cập Compute Optimization Hub trong phần “Billing and Cost Management” của AWS Console để xem khuyến nghị.

Vì nhu cầu tài nguyên thay đổi theo thời gian, việc giám sát liên tục là rất quan trọng.


## 3. Tận dụng EC2 Spot Instances

Với các workload chịu lỗi (fault-tolerant) và dạng batch – rất phổ biến trong điện toán học thuật – EC2 Spot Instances có thể giúp tiết kiệm đến 90% so với giá theo dạng On-Demand.

## 4. Tạm dừng instance ngoài giờ làm việc

Triển khai chính sách auto-scaling để tắt các EC2 instances vào thời gian ngoài giờ và bật lại khi cần. Điều này giúp tiết kiệm chi phí cho các tài nguyên không cần hoạt động 24/7. Một cách khác để thực hiện chiến lược này là sử dụng Instance Scheduler.

## 5. Sử dụng chính sách vòng đời cho Amazon S3

Tối ưu hóa chi phí lưu trữ Amazon S3 bằng cách triển khai lifecycle policies để tự động di chuyển các đối tượng ít được truy cập sang các tầng lưu trữ rẻ hơn, như S3 Glacier Instant Retrieval hoặc S3 Glacier Deep Archive.

Các công cụ như Amazon S3 Storage Lens và Amazon S3 Analytics có thể giúp bạn phân tích mức sử dụng và hỗ trợ việc thiết lập chính sách vòng đời phù hợp.

## 6. Tối ưu hóa chính sách lưu giữ bản sao lưu

Xem xét lại chính sách lưu giữ backup, đặc biệt với các workload không quan trọng hoặc môi trường phi sản xuất (non-production). Việc giảm thời gian giữ backup không cần thiết có thể tiết kiệm chi phí đáng kể.

Các workload trong môi trường production có thể phải tuân theo các yêu cầu lưu trữ theo quy định (ví dụ: 3 hoặc 7 năm). Để đơn giản, có thể thiết lập các workload trong môi trường non-production với cùng thời gian lưu trữ. Tuy nhiên, xét về chi phí, việc giữ lại các bản sao lưu không bao giờ được khôi phục là không cần thiết và không có lý do gì để bảo tồn chúng trong cùng khoảng thời gian như production.


## 7. Cân nhắc sử dụng Amazon S3 Intelligent-Tiering

Amazon S3 Intelligent-Tiering tự động di chuyển đối tượng giữa các tầng truy cập dựa trên mẫu sử dụng, đảm bảo bạn luôn sử dụng tầng lưu trữ có chi phí hiệu quả nhất.

## 8. Xóa các bộ lưu trữ không còn sử dụng

Xác định và xóa các EBS volumes không gắn (unattached), snapshots, hoặc các phiên upload chưa hoàn tất trên S3 không còn cần thiết.

Sử dụng Amazon Data Lifecycle Manager để quản lý các snapshot EBS là một phương pháp thực hành tốt.

## 9. Gộp các tài khoản dưới ít tài khoản thanh toán hơn

Đối với các tổ chức có nhiều tài khoản AWS, nên xem xét việc gộp lại dưới một số lượng tài khoản thanh toán (payer accounts) ít hơn. Việc này có thể mang lại lợi ích như Global Data Egress Waiver cho khách hàng trong giáo dục đại học, cũng như tiết kiệm tài nguyên mạng.

Nếu không đủ điều kiện để sử dụng Global Data Egress Waiver, bạn có thể dùng CloudFront để giảm lượng traffic từ AWS ra Internet đối với các trang web công khai.


## 10. Sử dụng AWS Savings Plans và Reserved Instances

Đối với các workload ổn định, sử dụng dài hạn như EC2, Lambda, Amazon SageMaker AI, và RDS, hãy xem xét sử dụng Savings Plans hoặc Reserved Instances để nhận mức giá chiết khấu trong 1–3 năm. Tại trang Billing and Cost Management trong AWS Console, bạn có thể xem khuyến nghị Savings Plan và Reserved Instances dựa trên workload hiện tại. Nên thực hiện right-sizing trước bước này để khuyến nghị phù hợp với tài nguyên đã tối ưu. Savings Plans và Reserved Instances có thể giúp tiết kiệm đến 72% so với giá On-Demand.

## Bonus #1: Miễn thuế

Nhiều public sector entities đủ điều kiện để được miễn thuế. Thông thường, điều này cần được cấu hình trong billing console cho từng member account. Để biết thêm chi tiết, xem liên kết này.

## Bonus #2: Tài nguyên học tập và hỗ trợ miễn phí

Muốn tìm hiểu về AWS Services? Hãy đăng ký một Skill Builder account. Có cả tùy chọn paid và no cost. Xem video trên AWS Twitch Channel hoặc AWS YouTube Channel. Đọc thêm nội dung trên AWS Blogs.

Cần hỗ trợ? Hãy đặt câu hỏi hoặc xem lại các câu trả lời trước đó trên trang AWS Community site: re:Post. Các câu hỏi được trả lời bởi AWS Specialists, Generative AI automation, và các thành viên khác trong community.

Ngoài ra, đối với những người có support agreements, bạn có thể mở case từ console để nhận general guidance hoặc specific assistance.
Cuối cùng, nếu bạn muốn tìm hiểu thêm về cost optimization, hãy xem AWS Well-Architected Cost Optimization Workshop. Workshop này tập trung vào Cost Optimization pillar và được thiết kế để cung cấp hands-on guidance nhằm giải thích các best practices.

Và tất nhiên, hãy liên hệ với AWS account team của bạn để khám phá thêm các tùy chọn tổ chức workshops cho campus của bạn. Nếu campus của bạn có Enterprise Support agreement, Technical Account Manager được chỉ định của bạn cũng có thể cung cấp guidance.


**Jim Surlow**

Jim là Senior Technical Account Manager (TAM) và Enterprise Support Lead với hơn 35 năm kinh nghiệm trong lĩnh vực IT. Nhóm TAMs của ông hỗ trợ các khách hàng AWS thuộc lĩnh vực Giáo dục Đại học (Higher Education) tại khu vực phía Tây Hoa Kỳ. Ông cũng là thành viên của cả hai cộng đồng kỹ thuật AWS Storage và Education Technical Field Communities.
