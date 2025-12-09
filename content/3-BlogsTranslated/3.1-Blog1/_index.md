---
title: "Blog 1"
date: ""
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Clario enhances the quality of the clinical trial documentation process with Amazon Bedrock

*This post is co-written with Kim Nguyen and Shyam Banuprakash from Clario.*

Clario is a leading provider of endpoint data solutions to the clinical trials industry, generating high-quality clinical evidence for life sciences companies seeking to bring new therapies to patients. Since Clario’s founding more than 50 years ago, the company’s endpoint data solutions have supported clinical trials more than 26,000 times with over 700 regulatory approvals across more than 100 countries. One of the critical challenges Clario faces when supporting its clients is the time-consuming process of generating documentation for clinical trials, which can take weeks.

## The business challenge

When medical imaging analysis is part of a clinical trial it is supporting, Clario prepares a medical imaging charter process document that outlines the format and requirements of the central review of clinical trial images (the Charter). Based on the Charter, Clario’s imaging team creates several subsequent documents (as shown in the following figure), including the business requirement specification (BRS), training slides, and ancillary documents. The content of these documents is largely derived from the Charter, with significant reformatting and rephrasing required. This process is time-consuming, can be subject to inadvertent manual error, and carries the risk of inconsistent or redundant information, which can delay or otherwise negatively impact the clinical trial.

![docflow1](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2025/03/27/docflow1.png)

Clario’s imaging team recognized the need to modernize the document generation process and streamline the processes used to create end-to-end document workflows. Clario engaged with their AWS account team and AWS Generative AI Innovation Center to explore how generative AI could help streamline the process.

## The solution

The AWS team worked closely with Clario to develop a prototype solution that uses AWS AI services to automate the BRS generation process. The solution involves the following key services:

- Amazon Simple Storage Service (Amazon S3): A scalable object storage service used to store the charter-derived and generated BRS documents.

- Amazon OpenSearch Serverless: An on-demand serverless configuration for Amazon OpenSearch Service used as a vector store.

- Amazon Bedrock: Amazon Bedrock is a fully managed service that offers a choice of high-performing foundation models (FMs) from leading AI companies through a single API, along with a broad set of capabilities you need to build generative AI applications with security, privacy, and responsible AI. Using Amazon Bedrock, you can experiment with and evaluate top FMs for your use case, privately customize them with your data using techniques such as fine-tuning and Retrieval Augmented Generation (RAG) and build agents that execute tasks using your enterprise systems and data sources.

The solution is shown in the following figure:

![architecture-2](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2025/03/27/architecture-2.png)

## Architecture walkthrough

1. Charter-derived documents are processed in an on-premises script in preparation for uploading.

2. Files are sent to AWS using AWS Direct Connect.

3. The script chunks the documents and calls an embedding model to produce the document embeddings. It then stores the embeddings in an OpenSearch vector database for retrieval by our application. Clario uses an Amazon Titan Text Embeddings model offered by Amazon Bedrock. Each chunk is called to produce an embedding.

4. Amazon OpenSearch Serverlessis used as the durable vector store. Document chunk embeddings are stored in an OpenSearch vector index, which enables the application to search for the most semantically relevant documents. Clario also stores attributes for the source document and associated trial to allow for a richer search experience.

5. A custom build user interface is the primary access point for users to access the system, initiate generation jobs, and interact with a chat UI. The UI is integrated with the workflow engine that manages the orchestration process.

6. The workflow engine calls the Amazon Bedrock API and orchestrates the business requirement specification document generation process. The engine:

    - Uses a global specification that stores the prompts to be used as input when calling the large language model.

    - Queries OpenSearch for the relevant Imaging charter.

    - Loops through every business requirement.

    - Calls the Claude 3.7 Sonnet large language model from Amazon Bedrock to generate responses.

7. Outputs the business requirement specification document to the user interface, where a business requirement writer can review the answers to produce a final document. Clario uses Claude 3.7 Sonnet from Amazon Bedrock for the question-answering and the conversational AI application.

8. The final documents are written to Amazon S3 to be consumed and published by additional document workflows that will be built in the future.

9. An as-needed AI chat agent to allow document-based discovery and enable users to converse with one or more documents.

## Benefits and results

By using AWS AI services, Clario has streamlined the complicated BRS generation process significantly. The prototype solution demonstrated the following benefits:

- **Improved accuracy**: The use of generative AI models minimized the risk of translation errors and inconsistencies, reducing the need for rework and study delays.

- **Scalability and flexibility**: The serverless architecture provided by AWS services allows the solution to scale seamlessly as demand increases, while the modular design enables straightforward integration with other Clario systems.

- **Security**: Clario’s data security strategy revolves around confining all its information within the secure AWS ecosystem using the security features of Amazon Bedrock. By keeping data isolated within the AWS infrastructure, Clario helps ensure protection against external threats and unauthorized access. This approach enables Clario to meet compliance requirements and provide clients with confidence in the confidentiality and integrity of their sensitive data.

## Lessons learned

The successful implementation of this prototype solution reinforced the value of using generative AI models for domain-specific applications like those prevalent in the life sciences industry. It also highlighted the importance of involving business stakeholders early in the process and having a clear understanding of the business value to be realized. Following the success of this project, Clario is working to productionize the solution in their Medical Imaging business during 2025 to continue offering state-of-the-art services to its customers for best quality data and successful clinical trials.

## Conclusion

The collaboration between Clario and AWS demonstrated the potential of AWS AI and machine learning (AI/ML) services and generative AI models, such as Anthropic’s Claude, to streamline document generation processes in the life sciences industry and, specifically, for complicated clinical trial processes. By using these technologies, Clario was able to enhance and streamline the BRS generation process significantly, improving accuracy and scalability. As Clario continues to adopt AI/ML across its operations, the company is well-positioned to drive innovation and deliver better outcomes for its partners and patients.

---

### About the Authors

**Kim Nguyen** serves as the Sr Director of Data Science at Clario, where he leads a team of data scientists in developing innovative AI/ML solutions for the healthcare and clinical trials industry. With over a decade of experience in clinical data management and analytics, Kim has established himself as an expert in transforming complex life sciences data into actionable insights that drive business outcomes. His career journey includes leadership roles at Clario and Gilead Sciences, where he consistently pioneered data automation and standardization initiatives across multiple functional teams. Kim holds a Master’s degree in Data Science and Engineering from UC San Diego and a Bachelor’s degree from the University of California, Berkeley, providing him with the technical foundation to excel in developing predictive models and data-driven strategies. Based in San Diego, California, he leverages his expertise to drive forward-thinking approaches to data science in the clinical research space.

**Shyam Banuprakash** serves as the Senior Vice President of Data Science and Delivery at Clario, where he leads complex analytics programs and develops innovative data solutions for the medical imaging sector. With nearly 12 years of progressive experience at Clario, he has demonstrated exceptional leadership in data-driven decision making and business process improvement. His expertise extends beyond his primary role, as he contributes his knowledge as an Advisory Board Member for both Modal and UC Irvine’s Customer Experience Program. Shyam holds a Master of Advanced Study in Data Science and Engineering from UC San Diego, complemented by specialized training from MIT in data science and big data analytics. His career exemplifies the powerful intersection of healthcare, technology, and data science, positioning him as a thought leader in leveraging analytics to transform clinical research and medical imaging.

**John O’Donnell** is a Principal Solutions Architect at Amazon Web Services (AWS) where he provides CIO-level engagement and design for complex cloud-based solutions in the healthcare and life sciences (HCLS) industry. With over 20 years of hands-on experience, he has a proven track record of delivering value and innovation to HCLS customers across the globe. As a trusted technical leader, he has partnered with AWS teams to dive deep into customer challenges, propose outcomes, and ensure high-value, predictable, and successful cloud transformations. John is passionate about helping HCLS customers achieve their goals and accelerate their cloud native modernization efforts.

**Praveen Haranahalli** is a Senior Solutions Architect at Amazon Web Services (AWS) where he provides expert guidance and architects secure, scalable cloud solutions for diverse enterprise customers. With nearly two decades of IT experience, including over ten years specializing in Cloud Computing, he has a proven track record of delivering transformative cloud implementations across multiple industries. As a trusted technical advisor, Praveen has successfully partnered with customers to implement robust DevSecOps pipelines, establish comprehensive security guardrails, and develop innovative AI/ML solutions. Praveen is passionate about solving complex business challenges through cutting-edge cloud architectures and helping organizations achieve successful digital transformations powered by artificial intelligence and machine learning technologies.