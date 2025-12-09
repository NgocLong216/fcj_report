---
title: "Event 1"
date: ""
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# Summary Report: “​AI/ML/GenAI on AWS”

### Event Objectives

- To understand the landscape of AI on AWS, ranging from specialized ML services to the latest advancements in Agentic AI and real-time voice frameworks.

### Speakers

- **Dinh Le Hoang Anh** – Cloud Engineer Trainee

### Key Highlights

#### AWS AI/ML Services Overview

- ​Amazon SageMaker – End-to-end ML platform

    - ​Data preparation and labeling

    - ​Model training, tuning, and deployment

    - ​Integrated MLOps capabilities

- ​Live Demo: SageMaker Studio walkthrough

#### Generative AI with Amazon Bedrock

- Foundation Models: Claude, Llama, Titan – comparison & selection guide

- ​Prompt Engineering: Techniques, Chain-of-Thought reasoning, Few-shot learning

- ​Retrieval-Augmented Generation (RAG): Architecture & Knowledge Base integration

- ​Bedrock Agents: Multi-step workflows and tool integrations

- ​Guardrails: Safety and content filtering

- ​Live Demo: Building a Generative AI chatbot using Bedrock

### Key Takeaways

- The "Chasm" is Real: There is a significant gap between building a cool AI demo (POC) and a production-ready agent. Issues like latency, security, and "hallucination" governance must be addressed using robust platforms like Bedrock AgentCore.

- Specialization over Generalization: For specific tasks (like finding defects in machinery or analyzing customer sentiment), using specialized services like Lookout or Comprehend is often more efficient than building custom models from scratch.

- Multimodal Agents are the Future: Frameworks like Pipecat allow developers to build assistants that can see and hear in real-time, moving beyond text-only interfaces.

### Applying to Work

- Cost Estimation: When proposing AI solutions, we must account for specific pricing models (e.g., Personalize charges by training hour and inference, while Comprehend charges by character).

- Tool Selection: Use LangChain or CrewAI for rapid prototyping of agents, but consider Bedrock AgentCore for enterprise-grade security and governance when moving to production.

- Anomaly Detection: Evaluate Amazon Lookout for internal operations monitoring to automate defect detection.

#### Some event photos

![1](/images/4-Eventparticipated/1.jpg)
![2](/images/4-Eventparticipated/2.jpg)
![3](/images/4-Eventparticipated/3.jpg)
![4](/images/4-Eventparticipated/4.jpg)