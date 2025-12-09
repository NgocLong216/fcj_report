---
title: "Event 1"
date: ""
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Báo Cáo Tóm Tắt: “AI/ML/GenAI trên AWS”

### Mục Tiêu Sự Kiện

- Hiểu tổng quan về AI trên AWS, từ các dịch vụ ML chuyên biệt đến những tiến bộ mới nhất về Agentic AI và framework giọng nói thời gian thực.

### Diễn Giả

- **Dinh Le Hoang Anh** – Cloud Engineer Trainee

### Những Điểm Nổi Bật

#### Tổng Quan Dịch Vụ AI/ML trên AWS

- ​Amazon SageMaker – Nền tảng ML đầu cuối

    - ​Chuẩn bị và gắn nhãn dữ liệu

    - ​Huấn luyện, tinh chỉnh và triển khai mô hình

    - ​Tích hợp khả năng MLOps

- ​Demo Trực Tiếp: Trình diễn SageMaker Studio

#### Generative AI với Amazon Bedrock

- Mô hình nền tảng: Claude, Llama, Titan – so sánh & hướng dẫn chọn lựa

- ​Prompt Engineering: Kỹ thuật, Chain-of-Thought reasoning, Few-shot learning

- ​Retrieval-Augmented Generation (RAG): Kiến trúc & tích hợp Knowledge Base

- ​Bedrock Agents: Workflow nhiều bước và tích hợp công cụ

- ​Guardrails: An toàn và lọc nội dung

- ​Demo Trực Tiếp: Xây dựng chatbot Generative AI sử dụng Bedrock

### Những Bài Học Chính

- "Chasm" là Thực: Khoảng cách giữa việc tạo demo AI thú vị (POC) và agent sẵn sàng triển khai sản xuất là rất lớn. Các vấn đề như độ trễ, bảo mật và quản trị "hallucination" cần được giải quyết bằng các nền tảng mạnh mẽ như Bedrock AgentCore.

- Chuyên Môn Hóa vượt Trội hơn Tổng Quát: Đối với các nhiệm vụ cụ thể (như tìm lỗi trong máy móc hoặc phân tích cảm xúc khách hàng), sử dụng dịch vụ chuyên biệt như Lookout hoặc Comprehend thường hiệu quả hơn việc xây dựng mô hình tùy chỉnh từ đầu.

- Agent Đa phương thức là Tương Lai: Các framework như Pipecat cho phép phát triển các trợ lý có khả năng nhìn và nghe theo thời gian thực, vượt ra ngoài giao diện chỉ văn bản.

### Ứng Dụng vào Công Việc

- Ước Tính Chi Phí: Khi đề xuất giải pháp AI, cần tính đến các mô hình giá cụ thể (ví dụ: Personalize tính phí theo giờ huấn luyện và inference, trong khi Comprehend tính theo số ký tự).

- Lựa Chọn Công Cụ: Sử dụng LangChain hoặc CrewAI để thử nghiệm nhanh các agent, nhưng cân nhắc Bedrock AgentCore cho bảo mật và quản trị cấp doanh nghiệp khi triển khai sản xuất.

- Phát Hiện Dị Thường: Đánh giá Amazon Lookout cho việc giám sát vận hành nội bộ để tự động hóa phát hiện lỗi.

#### Một vài ảnh sự kiện

![1](/images/4-Eventparticipated/1.jpg)
![2](/images/4-Eventparticipated/2.jpg)
![3](/images/4-Eventparticipated/3.jpg)
![4](/images/4-Eventparticipated/4.jpg)
