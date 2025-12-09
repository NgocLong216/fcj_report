---
title: "Event 2"
date: ""
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “DepOps on AWS”

### Event Objectives

- To master the AWS DevOps toolkit, focusing on shifting from manual operations to automated "Infrastructure as Code," understanding container orchestration, and implementing self-healing observability.

### Speakers

- **Truong Quang Tinh** – AWS Communit Builder, Platform Engineer - Tymex
- **Kha Van**
- **Tran Vi**
- **Long Quy Nghiem**

### Key Highlights

#### DevOps Mindset

- ​Recap of AI/ML session

- ​DevOps culture and principles

- ​Benefits and key metrics (DORA, MTTR, deployment frequency)

#### AWS DevOps Services – CI/CD Pipeline

- ​Source Control: AWS CodeCommit, Git strategies (GitFlow, Trunk-based)

- ​Build & Test: CodeBuild configuration, testing pipelines

- ​Deployment: CodeDeploy with Blue/Green, Canary, and Rolling updates

- ​Orchestration: CodePipeline automation

- ​Demo: Full CI/CD pipeline walkthrough

#### Infrastructure as Code (IaC)

- AWS CloudFormation: Templates, stacks, and drift detection

- ​AWS CDK (Cloud Development Kit): Constructs, reusable patterns, and language support

- ​Demo: Deploying with CloudFormation and CDK

- ​Discussion: Choosing between IaC tools

#### Container Services on AWS

- ​Docker Fundamentals: Microservices and containerization

- ​Amazon ECR: Image storage, scanning, lifecycle policies

- ​Amazon ECS & EKS: Deployment strategies, scaling, and orchestration

- ​AWS App Runner: Simplified container deployment

- ​Demo & Case Study: Microservices deployment comparison

#### Monitoring & Observability

- ​CloudWatch: Metrics, logs, alarms, and dashboards

- ​AWS X-Ray: Distributed tracing and performance insights

- ​Demo: Full-stack observability setup

- ​Best Practices: Alerting, dashboards, and on-call processes

#### DevOps Best Practices & Case Studies

- ​Deployment strategies: Feature flags, A/B testing

- ​Automated testing and CI/CD integration

- ​Incident management and postmortems

- ​Case Studies: Startups and enterprise DevOps transformations

### Key Takeaways

- Observability is Active, Not Passive: Modern monitoring isn't just looking at dashboards; it's about configuring CloudWatch to act (restart servers, scale out) when thresholds are breached.

- The "L1" vs. "L3" Trade-off: When using CDK, you have a choice between granular control (L1 Constructs mapping 1:1 to CloudFormation) or high-level abstraction (L3 patterns). Understanding this layer helps in debugging.

- Testing Strategy Shift: For microservices, unit tests aren't enough. We must explicitly test for "Connection Failures" and "API Contracts" to prevent cascading failures.

### Applying to Work

- Self-Healing Infrastructure: Review our current alarms. Can we attach a Lambda function to any of them to automatically fix the issue (e.g., clear a cache) instead of waking up an engineer?

- rototyping: For the next internal tool or MVP, use App Runner instead of EC2/ECS to reduce setup time to near zero.

- Standardization: Adopt CDK with TypeScript for our infrastructure to allow developers to read/write infra definitions in a language they already know.

#### Some event photos

![1](/images/4-Eventparticipated/5.jpg)
![2](/images/4-Eventparticipated/6.jpg)