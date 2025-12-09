---
title: "Event 2"
date: ""
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo Cáo Tóm Tắt: “DevOps trên AWS”

### Mục Tiêu Sự Kiện

- Nắm vững bộ công cụ AWS DevOps, tập trung vào việc chuyển từ vận hành thủ công sang tự động hóa "Infrastructure as Code," hiểu về điều phối container, và triển khai quan sát tự hồi phục (self-healing observability).

### Diễn Giả

- **Truong Quang Tinh** – AWS Community Builder, Platform Engineer - Tymex  
- **Kha Van**  
- **Tran Vi**  
- **Long Quy Nghiem**

### Những Điểm Nổi Bật

#### Tư Duy DevOps

- ​Tổng kết phiên AI/ML trước

- ​Văn hóa và nguyên tắc DevOps

- ​Lợi ích và các chỉ số chính (DORA, MTTR, tần suất triển khai)

#### Dịch Vụ DevOps trên AWS – CI/CD Pipeline

- ​Quản lý mã nguồn: AWS CodeCommit, chiến lược Git (GitFlow, Trunk-based)

- ​Build & Test: Cấu hình CodeBuild, pipeline kiểm thử

- ​Triển khai: CodeDeploy với Blue/Green, Canary và Rolling updates

- ​Điều phối: Tự động hóa với CodePipeline

- ​Demo: Trình diễn toàn bộ CI/CD pipeline

#### Infrastructure as Code (IaC)

- AWS CloudFormation: Template, stack và phát hiện drift

- ​AWS CDK (Cloud Development Kit): Constructs, pattern tái sử dụng, hỗ trợ đa ngôn ngữ

- ​Demo: Triển khai với CloudFormation và CDK

- ​Thảo luận: Lựa chọn giữa các công cụ IaC

#### Dịch Vụ Container trên AWS

- ​Docker Fundamentals: Microservices và containerization

- ​Amazon ECR: Lưu trữ image, quét bảo mật, lifecycle policies

- ​Amazon ECS & EKS: Chiến lược triển khai, scaling, điều phối

- ​AWS App Runner: Triển khai container đơn giản

- ​Demo & Case Study: So sánh triển khai microservices

#### Giám sát & Observability

- ​CloudWatch: Metrics, logs, alarms và dashboards

- ​AWS X-Ray: Distributed tracing và insight hiệu năng

- ​Demo: Thiết lập observability toàn stack

- ​Best Practices: Cảnh báo, dashboards và quy trình on-call

#### Best Practices & Case Studies DevOps

- ​Chiến lược triển khai: Feature flags, A/B testing

- ​Tích hợp CI/CD và kiểm thử tự động

- ​Quản lý sự cố và postmortems

- ​Case Studies: Chuyển đổi DevOps của startup và doanh nghiệp lớn

### Những Bài Học Chính

- Observability là chủ động, không thụ động: Giám sát hiện đại không chỉ là nhìn vào dashboard; mà còn là cấu hình CloudWatch để hành động (khởi động lại server, scale out) khi vượt ngưỡng.

- Trade-off "L1" vs "L3": Khi dùng CDK, bạn có thể chọn giữa granular control (L1 Constructs 1:1 với CloudFormation) hoặc abstraction cao (L3 patterns). Hiểu lớp này giúp debug dễ hơn.

- Thay đổi chiến lược kiểm thử: Với microservices, unit test không đủ. Cần kiểm thử rõ ràng "Connection Failures" và "API Contracts" để tránh lỗi lan truyền.

### Ứng Dụng vào Công Việc

- Self-Healing Infrastructure: Xem xét các cảnh báo hiện tại. Có thể gắn Lambda function để tự động khắc phục vấn đề (ví dụ: clear cache) thay vì phải can thiệp thủ công?

- Prototyping: Với tool nội bộ hoặc MVP tiếp theo, sử dụng App Runner thay vì EC2/ECS để giảm thời gian setup gần như bằng 0.

- Chuẩn hóa: Áp dụng CDK với TypeScript cho cơ sở hạ tầng, giúp developer đọc/viết định nghĩa infra bằng ngôn ngữ họ đã quen.

#### Một vài ảnh từ sự kiện

![1](/images/4-Eventparticipated/5.jpg)
![2](/images/4-Eventparticipated/6.jpg)