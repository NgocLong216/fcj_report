---
title: "Đề xuất"
date: "2025-09-22"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

**AWS First Cloud AI Journey – Project Plan (Kế hoạch dự án)**

[Project team] – [University] – [Project Name]

[Date]

**Mục lục**

<span style="text-decoration: underline;">1</span> <span style="text-decoration: underline;">BACKGROUND VÀ ĐỘNG LỰC</span>

<span style="text-decoration: underline;">1.1</span> <span style="text-decoration: underline;">Executive Summary</span>

<span style="text-decoration: underline;">1.2</span> <span style="text-decoration: underline;">PROJECT SUCCESS CRITERIA</span>

<span style="text-decoration: underline;">1.3</span> <span style="text-decoration: underline;">Assumptions</span>

<span style="text-decoration: underline;">2</span> <span style="text-decoration: underline;">SOLUTION ARCHITECTURE / SƠ ĐỒ KIẾN TRÚC</span>

<span style="text-decoration: underline;">2.1</span> <span style="text-decoration: underline;">Technical Architecture Diagram</span>

<span style="text-decoration: underline;">2.2</span> <span style="text-decoration: underline;">Technical Plan</span>

<span style="text-decoration: underline;">2.3</span> <span style="text-decoration: underline;">Project Plan</span>

<span style="text-decoration: underline;">2.4</span> <span style="text-decoration: underline;">Security Considerations</span>

<span style="text-decoration: underline;">3</span> <span style="text-decoration: underline;">ACTIVITIES VÀ DELIVERABLES</span>

<span style="text-decoration: underline;">3.1</span> <span style="text-decoration: underline;">Hoạt động và Giao hàng</span>

<span style="text-decoration: underline;">3.2</span> <span style="text-decoration: underline;">OUT OF SCOPE</span>

<span style="text-decoration: underline;">3.3</span> <span style="text-decoration: underline;">PATH TO PRODUCTION</span>

<span style="text-decoration: underline;">4</span> <span style="text-decoration: underline;">EXPECTED AWS COST BREAKDOWN BY SERVICES</span>

<span style="text-decoration: underline;">5</span> <span style="text-decoration: underline;">ĐỘI NGŨ</span>

<span style="text-decoration: underline;">6</span> <span style="text-decoration: underline;">Resources & Cost Estimates</span>

<span style="text-decoration: underline;">7</span> <span style="text-decoration: underline;">Chấp nhận</span>

# 1 BACKGROUND VÀ ĐỘNG LỰC

## **1.1 Tóm tắt điều hành**

Tổ chức đối mặt với những vấn đề inefficiencies trong đánh giá HR do xử lý dữ liệu thủ công, thiếu tính minh bạch trong các quy trình đánh giá và tracking metrics.

InsightHR cung cấp HR automation thông qua flexible evaluation management, automated scoring. AWS cung cấp serverless scalability, cost efficiency, security cho sensitive data, và rapid deployment.

Custom KPI, automated performance scoring, multi-level dashboards, automated notifications, role-based access (Admin/Manager/Employee), multi-tenant support.

End-to-end delivery bao gồm Well-Architected design, serverless backend (Lambda, DynamoDB, API Gateway), frontend (S3 + CloudFront), authentication/security (Cognito, IAM), KPI/formula builder, notifications (SNS, SES), CI/CD, monitoring, và knowledge transfer.

## **1.2 Tiêu chí thành công của dự án**

Thành công được xác định bằng việc chứng minh một functional MVP chứng minh khả năng của platform trong việc tự động hóa đánh giá HR và cung cấp measurable business value.

1. **Tiêu chí chức năng (Functional Criteria):**

- Authentication với role-based access (Admin/HR, Manager, Employee)

- HR tạo custom KPIs mà không cần hỗ trợ kỹ thuật

- CSV upload kích hoạt automated Lambda scoring

- Dashboard hiển thị individual/team performance với biểu đồ

- SES gửi automated email notifications

- **Tiêu chí kỹ thuật (Technical Criteria):**

- 99.9%+ uptime

- <300ms API latency (95th percentile)

- 95%+ scoring accuracy so với manual calculations

- Zero critical security vulnerabilities

- **Hiệu suất & Chi phí (Performance & Cost):**

- ~$11.53/tháng AWS cost

- End-to-end workflow (upload → score → visualize) hoàn thành trong <5 phút

- **Tác động kinh doanh (Business Impact):**

- Chứng minh 60%+ potential giảm thời gian HR

- Non-technical users vận hành KPI builder độc lập

- **Giao hàng (Delivery):**

- Week 8: MVP (authentication, KPI/formula management, scoring, basic dashboard)

- Week 12: Full features (notifications, advanced dashboard)

## **1.3 Giả định và ràng buộc**

**1. Giả định (Assumptions):**

- AWS cost estimate hiện tại khoảng $11.53/tháng là chính xác cho projected initial load và usage.

- Required data format và mapping logic cho employee performance data có thể được xác định rõ ràng và cung cấp bởi HR team cho automated scoring engine.

- Automated scoring system được trained locally. Technical evaluation files của mỗi team được đánh giá theo criteria của công ty và phải theo format được cung cấp bởi customer.

**2. Ràng buộc (Constraints):**

- Project delivery phải tuân thủ timeline 12 tuần sử dụng Agile Scrum framework.

- Solution phải được xây dựng hoàn toàn trên serverless AWS services để đáp ứng objectives của scalability, cost efficiency, và reduced operational overhead.

- Final production AWS cost phải duy trì quanh target ~$11.53/tháng.

**3. Risks:**

- Data Security/Compliance: Failure để fully understand hoặc implement tất cả customer's specific regulatory control validation requirements có thể ảnh hưởng đến project's ability để meet security objectives.

- Feature Creep: Yêu cầu các features được xác định là "Out of Scope" có thể derail 12-week MVP delivery timeline.

# 2 SOLUTION ARCHITECTURE / SƠ ĐỒ KIẾN TRÚC

## **2.1 Technical Architecture Diagram**

Nền tảng InsightHR được xây dựng trên serverless architecture sử dụng AWS services, cung cấp scalability, cost-effectiveness, và high availability, kiến trúc bao gồm:

1. **Frontend & Content Delivery:**

- Amazon S3: Hosts static website và stores user-uploaded files (CSV). S3 Vector để store vectors (embeddings cho text-data), S3 Standard để store raw documents.

- Amazon CloudFront: Distributes static và dynamic content globally với low latency.

2. **Backend & Compute:**

- AWS Lambda: Executes tất cả business logic, bao gồm authentication, custom scoring.

- Amazon API Gateway: Manages APIs làm communication gateway giữa frontend và backend.

3. **Data Storage:**

- Amazon DynamoDB: Stores structured data như user/employee information, company KPIs, scoring formulas, và performance evaluation results.

4. **Security & Identity:**

- Amazon Cognito: Manages user authentication, registration, và identity workflows.

- AWS IAM: Manages access control và permissions cho AWS services.

- AWS KMS: Encrypts sensitive data trong DynamoDB và S3.

5. **Monitoring & Notifications:**

- Amazon CloudWatch & CloudWatch Logs: Monitors Lambda functions, API Gateway, và database access.

- Amazon SNS: Sends notifications (ví dụ: reminders, result notifications) cho employees.

6. **Lợi ích kiến trúc (Architecture Benefits):**

- Serverless: Không server management và automatic scaling.

- Cost-Effective: Chủ yếu pay-as-you-go services.

- High Availability: Built-in redundancy trên AWS regions.

- Scalable: Có thể xử lý growth từ small teams đến large enterprises.

- Flexible: Dễ dàng modify và extend functionality.

7. **Proposed Architecture Diagram:**

![Diagram](/images/2-Proposal/fix_aws_diagram.drawio.png)

8. **Công cụ được đề xuất cho dự án này (Tools Proposed for This Project):**

- Amazon CloudFront: Cho global content delivery và caching của static và dynamic web content.

- Amazon S3: Để host static web assets và store documents, vector embeddings, và files khác được xử lý bởi system.

- Amazon API Gateway: Để provide secure RESTful interface, hoạt động như communication layer giữa frontend clients và backend services.

- AWS Lambda: Để run backend business logic bao gồm user dashboard, auto scoring, và data management workflows.

- Amazon DynamoDB: Để store application data như user information, HR records, scoring results, và vector metadata với low-latency performance.

- Amazon Cognito: Để manage user authentication, authorization, registration, MFA, và secure access tới APIs và frontend applications.

- AWS Identity and Access Management (IAM): Để define fine-grained access policies và control permissions giữa services và users.

- AWS Key Management Service (KMS): Để manage encryption keys sử dụng cho securing sensitive data stored trong S3, DynamoDB, và logs.

- Amazon ECR: Để store containerized model assets và application dependencies trong secure và version-controlled repository.

- Amazon Simple Email Service (SES): Để send automated email notifications như onboarding alerts và HR communications.

- Amazon Simple Notification Service (SNS): Để publish notifications và trigger downstream processes; integrates với email, SMS, và microservices.

- Amazon CloudWatch & CloudWatch Logs: Cho monitoring performance, logging, tracing, và operational troubleshooting trên Lambda, API Gateway.

## **2.2 Technical Plan**

Đối tác sẽ develop automated deployment scripts sử dụng AWS CloudFormation và Infrastructure as Code (IaC) practices.

Điều này sẽ cho phép quick và repeatable deployments vào AWS accounts. Một số additional configurations như WAF rules trên CloudFront cho enhanced security có thể require approval và sẽ follow standard DevOps change management processes.

Application Feature Implementation:

**1. Authentication & Security Module**

- User Management: Cognito manages user lifecycle Registration, login, password reset workflows

- Access Control: IAM và RBAC enforce role-based permissions Admin/HR, Manager, và Employee access levels

- API Security: API Gateway implements JWT-protected endpoints Token validation trước Lambda processing

**2. Administration Module (HR Panel)**

- KPI Management: HR creates, edits, và deletes custom metrics Examples: Tasks Completed, Code Quality, Customer Satisfaction Definitions stored trong DynamoDB

- Auto scoring bởi employee's technical score cho mỗi team với ML model.

**3. Core User Functions**

- Data Upload & Mapping: Upload performance data files (CSV) vào DynamoDB

- Scoring Engine: Lambda triggered on upload Retrieves active formula từ DynamoDB Calculates employee scores Stores results trong DynamoDB Flow: Upload → Validate → Map → Calculate → Store

- Dashboard: Visualize individual và department performance Line graphs, bar charts, trend analysis

- Notifications: SES sends automated alerts Performance milestones, review reminders, custom triggers

## **2.3 Project Plan**

Đối tác sẽ adopt Agile Scrum framework qua 12 one-week sprints totaling 12-week delivery timeline.

1. **Team Responsibilities**

- Product Owner: Prioritizes backlog (KPIs, formulas, analytics) Final authority on feature acceptance

- Development Team: Implements Cognito authentication Builds admin portal và formula builder Develops scoring engine và dashboard Integrates SNS với SES notifications via Email.

- QA Personnel: Conducts functional, performance, và security testing Facilitates UAT Ensures compliance và quality standards

2. **Communication Cadences**

- Daily Standups (30 phút - 1 giờ): Progress review và blocker identification

- Retrospectives (Hàng tuần, 1 giờ): Process improvement và delivery optimization

- Executive Updates (Hàng tuần): Written reports on progress, risks, KPIs, roadmap Leadership decisions required

3. **Knowledge Transfer**

- Sessions conducted bởi development team covering AWS serverless fundamentals KPI và formula configuration Data workflows và column-mapping Dashboard navigation và analytics System monitoring (CloudWatch, Cognito, DynamoDB)

## **2.4 Security Considerations**

Đối tác sẽ implement AWS security best practices dựa trên Well-Architected Framework, ưu tiên protection của sensitive HR data trong khi ensuring high operational availability. Security implementation covers năm key categories:

**1. Access Control**

- Cognito manages user identities Enforces strong password policies và MFA support

- IAM implements RBAC Admin/HR access Admin Panel và KPI/Formula configurations Employees view only their own performance data

- API Gateway validates JWT tokens Cognito-issued tokens verified trước Lambda processing

**2. Infrastructure Security**

- Serverless architecture reduces attack surface Không OS hoặc server patching required

- Lambda functions communicate via private AWS networks Chỉ necessary endpoints exposed qua API Gateway

**3. Data Protection**

- KMS encrypts data at rest DynamoDB và S3 encrypted Data unusable mà không decryption keys

- TLS/SSL (HTTPS) encrypts data in transit Tất cả frontend-backend communication secured

**4. Detection & Monitoring**

- CloudWatch Logs captures execution details Lambda và API Gateway activity logged Real-time monitoring và anomaly detection enabled

- AWS Config tracks configuration changes Ensures resource compliance với security objectives

**5. Incident Management**

- CloudWatch Alarms trigger automated alerts via SES Failed login threshold breaches Lambda resource anomalies

- Security Hub provides consolidated security view Unified compliance findings trên AWS environment Simplifies incident identification và response

AWS CloudTrail và AWS Config sẽ được configured cho continuous monitoring của activities và compliance status của resources. Khách hàng sẽ share their regulatory control validation requirements làm inputs cho partner để ensure tất cả security objectives được meet.

# 3 ACTIVITIES VÀ DELIVERABLES

## **3.1 Hoạt động và Giao hàng**

**LƯU Ý: Một số Project Phases chồng lên nhau.**

| Project Phase                            | Timeline  | Activities                                                                                                               | Deliverables/Milestones                                                                                                                                                                                                    | Total man-day |
| ---------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Phase 1: Foundation & Scoring Model      | Tuần 1-8  | • Personal infrastructure architecture research • Data generation cho local model training • Scoring model build         | • Finalized personal architecture diagram • Ready dataset cho Local Model training • Scoring Model MVP (Minimum Viable Product)                                                                                            | 80            |
| Phase 2: Project Setup & Dashboard       | Tuần 9-10 | • Project Setup với basic functions: IAM Role, CRUD function, Static web • Web UI Demo • Implement Dashboard • Fix Model | • Basic IAM Roles configured • Operational CRUD functions • Static website deployed (S3/CloudFront) • Web UI Demo completed • Dashboard displaying data implemented                                                        | 40            |
| Phase 3: Absence Mgmt & Notification     | Tuần 11   | • Implement Absent managing • Setup SNS notification system                                                               | • Operational Absence tracking workflow implemented • SNS notification system fully integrated and tested                                                                                                                 | 15            |
| Phase 4: Integration, Testing & Handover | Tuần 12   | • Final Integration • Testing và set up Monitoring                                                                      | • Application components fully integrated • Functional, Performance, và Security Testing completed • Monitoring (CloudWatch) configured và operational • Project Completion Report & Post-implementation support plan delivered | 15            |

## **3.2 OUT OF SCOPE**

1. **AI Enhancements**

- AI-Powered Insights:

  - Khi đủ data available, develop AI models capable của:

  - Identifying performance patterns trên teams và departments

  - Predicting HR risks (ví dụ: turnover likelihood, burnout indicators)

  - Recommending personalized development plans

  - Detecting anomalies trong performance data

  - Suggesting optimal team compositions

- Machine Learning Features:

  - Predictive analytics cho workforce planning

  - Sentiment analysis từ employee feedback

  - Automated skill gap analysis

  - Performance trend forecasting

2. **Public API Development**

- API Ecosystem:

  - Build comprehensive API set cho phép other internal business systems tự động push performance data vào InsightHR.

- Integration Targets:

  - Project management tools (Jira, Asana, Monday.com)

  - CRM systems (Salesforce, HubSpot)

  - Time tracking software (Toggl, Harvest)

  - Communication platforms (Slack, Microsoft Teams)

  - Code repositories (GitHub, GitLab, Bitbucket)

- Benefits:

  - Transform InsightHR thành central HR data processing hub

  - Create synchronized và comprehensive management ecosystem

  - Eliminate manual data entry

  - Real-time performance tracking

3. **Advanced Features**

- Mobile Applications:

  - iOS và Android native apps

  - Push notifications

  - Offline capabilities

  - Mobile-optimized dashboards

  - DynamoDB back up

- Advanced Analytics:

  - Predictive modeling

  - Benchmarking across industries

  - Custom report builder

  - Data export và API cho third-party tools

- Collaboration Features:

  - Peer review systems

  - 360-degree feedback

  - Goal setting và tracking

  - Performance improvement plans

- Compliance & Governance:

  - Audit trails

  - Compliance reporting

  - Data retention policies

  - Advanced access controls

## **3.3 PATH TO PRODUCTION**

Tài liệu này outlines current production architecture và operational status cho InsightHR platform deployment. Platform đang fully live trong ap-southeast-1 (Singapore) region.

1. **Platform Architecture và Access**

- Public URL:

  - [https://insight-hr.io.vn](https://insight-hr.io.vn)

- AWS Region:

  - ap-southeast-1 (Singapore)

- Frontend:

  - React application hosted trên S3 (insighthr-web-app-sg) với CloudFront HTTPS distribution.

- Backend:

  - 8 Lambda function groups accessed via API Gateway REST API.

- Database:

  - DynamoDB tables configured với On-Demand capacity.

    - 6 tables cho mỗi team

    - Employee information table

    - History score table

    - Absent table

    - Account managing tables

- Authentication:

  - Cognito User Pool.

2. **Live Production Features**

- Các core features sau đây đã được successfully deployed và operational:

- Authentication:

  - Full support cho email/password login, password reset workflows.

- User Management:

  - Complete CRUD functionality, bao gồm bulk import và role-based access.

- Employee Management:

  - Full support cho 300+ employees và bulk operations.

- Performance Score Management:

  - Management của 900+ quarterly scores và calendar-based viewing.

- Attendance Management:

  - Processing của 9,300+ records, bao gồm check-in/check-out kiosk functionality và auto-absence marking.

- Performance Dashboard:

  - Live charts, trend analysis, live clock, và CSV export capabilities.

3. **Deployment và Verification Process (ĐưỜng dẫn tới sản xuất)**

- Standard, repeatable deployment workflow ensures rapid và verifiable updates cho production site:

- Build:

  - npm run build creates optimized production asset bundle.

- Test:

  - npm run preview validates built bundle locally trước deployment.

- Deploy:

  - aws s3 sync dist/ s3://insighthr-web-app-sg --region ap-southeast-1 pushes assets tới S3 bucket.

- Invalidate:

  - aws cloudfront create-invalidation --distribution-id E3MHW5VALWTOCI --paths "/\*" clears CloudFront CDN cache.

- Verify:

  - Full feature testing performed trên live public URL.

4. **Remaining Production Enhancements**

- Platform đang trong final phases của enhancement trước full stabilization, với key items planned hoặc in progress:

- Page Integration (In Progress)

- Consolidate tất cả administrative page navigation.

- Verify tất cả features accessible từ main menu.

- Test role-based routing trên tất cả pages.

- Fix bất kỳ integration bugs.

- Polish và Final Deployment (Planned)

- Implement comprehensive error handling và input validation.

- Refine responsive design cho full mobile compatibility.

- Conduct dedicated Security testing (penetration testing, vulnerability scanning).

- Execute Load testing cho scalability validation.

- Develop user documentation và training materials.

- Perform final production hardening procedures.

- Monitoring và Scalability Strategy

- Active Monitoring:

- CloudWatch Logs enabled cho tất cả Lambda functions và API Gateway endpoints, cùng với CloudWatch Metrics cho performance tracking.

- Planned Alarms:

- CloudWatch Alarms và SNS notifications planned cho critical error rates và latency.

- Scalability:

- Achieved via Serverless Architecture (DynamoDB On-Demand, Lambda, CloudFront CDN).

- Disaster Recovery:

- DynamoDB Point-in-Time Recovery và S3 Versioning planned để enabled cho critical data/assets. Lambda code stored trong version control cho rapid redeployment.

# 4 EXPECTED AWS COST BREAKDOWN BY SERVICES

[AWS Monthly Calculator](https://calculator.aws/#/estimate?id=796d503e4edfd5f357ce19c4a9eba51aee8f944c)

| AWS Service                       | Monthly Estimated Cost (USD) |
| --------------------------------- | ---------------------------- |
| AWS Lambda                        | $3.75                        |
| Amazon Simple Email Service (SES) | $2.25                        |
| Amazon DynamoDB                   | $1.52                        |
| Amazon Simple Storage Service     | $0.46                        |
| Amazon CloudWatch                 | $0.80                        |
| Amazon API Gateway                | $0.06                        |
| Amazon CloudFront                 | $0.00                        |
| Amazon Cognito                    | $0.00                        |
| Amazon EventBridge                | $0.00                        |
| Amazon IAM                        | $1.60                        |
| Amazon KMS                        | $1.03                        |
| TOTAL MONTHLY COST                | $11.53                       |
| TOTAL YEARLY COST                 | $138.36                      |

#

# 5 ĐỘI NGŨ

| Tên                      | Công việc                                                           | Vai trò | Email / Thông tin liên hệ        |
| ------------------------ | ------------------------------------------------------------------- | ------- | -------------------------------- |
| Bùi Tấn Phát             | Dashboard, Manage Employee, Support, Content check                  | Leader  | btfat3103@gmail.com              |
| Nguyễn Ngọc Long         | CRUD, Config Network / API Gateway, Test function, Slide            | Member  | nguyenngoclong216@gmail.com      |
| Đặng Nguyễn Minh Duy     | Database, CloudWatch / CloudLogs, Paper, Slide                      | Member  | dangnguyenminhduy11b08@gmail.com |
| Đỗ Đăng Khoa             | Log In/ Registration / Forget Password, UI / UX - Static Web, Paper | Member  | khoado7577@gmail.com             |
| Nguyễn Huỳnh Thiên Quang | Auto Scoring, Notification System, Slide                            | Member  | quangkootenhatvutru@gmail.com    |

# 6 RESOURCES & COST ESTIMATES

| Resource                   | Responsibility                                              | Rate (USD) / Hour |
| -------------------------- | ----------------------------------------------------------- | ----------------- |
| Full-Stack Developers [2]  | React frontend, Python Lambda backend, API integration      | $66               |
| Cloud Engineers [3]        | AWS infrastructure setup, deployment automation, monitoring | $66               |
| Other (Please specify)     | Estimated platform consumption (Lambda, DynamoDB).         |                   |
| Paper and present material |                                                             | $0.01             |

**LƯU Ý: Project Phase durations chồng lên nhau.**

| Project Phase                            | Duration | Man-Days     | Other (Please specify) | Estimated Cost            |
| ---------------------------------------- | -------- | ------------ | ---------------------- | ------------------------- |
| Phase 1: Foundation & Scoring Model      | 8 Tuần   | 80           | -                      | $42,246.40 (80 x $528.08) |
| Phase 2: Project Setup & Dashboard       | 2 Tuần   | 40           | -                      | $21,123.20 (40 x $528.08) |
| Phase 3: Absence Mgmt & Notification     | 1 Tuần   | 15           | -                      | $7,921.20 (15 x $528.08)  |
| Phase 4: Integration, Testing & Handover | 1 Tuần   | 15           | -                      | $7,921.20 (15 x $528.08)  |
| Total Hours                              | 1200 Giờ | 150 Man-Days |                        |                           |
| Total Cost                               | 12 Tuần  |              |                        | $79,212.00                |

**Cost Contribution distribution giữa Partner, Customer, AWS.**

| Party    | Contribution (USD) | % Contribution của Total |
| -------- | ------------------ | ------------------------ |
| Customer | 0                  | 0                        |
| Partner  | 0                  | 0                        |
| AWS      | 200                | 100                      |

#

# 7 CHẤP NHẬN

1. **Project Acceptance Criteria**

- InsightHR platform sẽ được coi là complete và accepted khi những criteria sau được met.

- **Completed Deliverables**

- Tất cả major features implemented và deployed tới production

- Authentication system với Google OAuth

- User và employee management với bulk operations

- Performance score management với calendar view

- Attendance system với auto-absence marking

- Interactive dashboard với live clock

- **Key Metrics Achieved**

- 300+ user accounts

- 300 employee records trên 5 departments

- 900+ performance scores tracked

- 9,300+ attendance records

- AWS monthly cost: ~$11.53

- System uptime: 99.9%+

- Zero critical security vulnerabilities

- **Acceptance Status**

- Current Status: Application deployed trong CloudFront Production URL: https://d2z6tht6rq32uy.cloudfront.net

- **Next Steps**

- Minor bug fixing và feature updates

- Conduct user acceptance testing

- Provide knowledge transfer và training
