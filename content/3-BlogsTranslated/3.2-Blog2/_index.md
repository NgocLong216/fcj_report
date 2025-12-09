---
title: "Blog 2"
date: ""
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Cleeng’s ChurnIQ AI-ssistant: Subscriber Analytics Powered by Amazon Bedrock

This blog is co-authored by Jakub Abramczyk, Data Scientist, Sebastian Boruch, ChurnIQ Product Manager, and Kirstin White, Growth Marketing Manager from Cleeng.

In the competitive direct-to-consumer (D2C) streaming market, understanding subscriber behavior is essential for increasing engagement, optimizing content, and reducing customer churn. According to Forbes, acquiring new customers costs 5-7 times more than retaining existing ones. Customer retention is crucial for digital subscription businesses across streaming media, sports, e-learning, wellness, and podcasting. Success depends on analyzing campaign effectiveness, identifying at-risk customers, and making data-driven decisions to maintain competitiveness and maximize revenue.

Traditionally, extracting insights from subscriber data has required specialized data analysts and business intelligence (BI) teams. This dependency frequently creates bottlenecks, delaying critical time-sensitive responses to potential churn risks. Expanding access to subscriber trend data with a generative AI-based assistant is how Amazon Web Services (AWS) Partner Cleeng addresses this challenge.

Cleeng has built ChurnIQ AI-ssistant, powered by Amazon Bedrock. This generative AI solution enables teams to analyze complex subscriber data through natural language prompts, eliminating the dependency for deep analytical expertise. Users can generate data visualizations and uncover trends instantly, empowering marketing, product, and retention teams with self-service analytics capabilities.

We’ll explore how Cleeng built the ChurnIQ AI-ssistant using AWS services (including Amazon Bedrock, AWS Lambda, and Amazon DynamoDB) to transform complex subscriber data into actionable insights for faster, more effective decision-making.

## About ChurnIQ AI-ssistant

![figure1](https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2025/03/26/ChurnIQ_AI-ssistant-image.png)

*Figure 1: A screenshot of ChurnIQ AI-ssistant interface.*

The ChurnIQ AI-ssistant is a new, generative AI-based component of ChurnIQ, the analytics product within Cleeng’s Subscriber Retention Management® solution. Cleeng’s solution unifies the entire subscriber experience across web and mobile apps from a single platform, empowering D2C companies to simplify subscription management and maximize customer lifetime value.

To help platform teams combat user subscriber churn, ChurnIQ AI-ssistant features predefined queries for common questions, easy chart customization, and seamless integration with ChurnIQ Studio. The platform provides comprehensive insights across the entire subscriber lifecycle, from sign-ups and trial conversions to renewals and churn.

Important metrics include transaction volume, revenue by offer and country, customer churn rates, customer lifetime value, subscription changes, and acquisition channels. These metrics help companies understand trends in platform performance, revenue trends, and audience behavior.

To generate a chart, users simply enter their question to the ChurnIQ AI-ssistant chatbot interface and are returned quick and accurate answers with visual data charts. These responses and charts give insights about subscriber behavior, churn rates, and revenue. ChurnIQ AI-ssistant then analyzes the data to spot concerning trends, and activates the necessary teams to dive deeper to remediate issues.

Besides allowing the user to choose their own question, the tool also includes predefined common queries related to user churn, such as:

- What are the primary reasons for customer churn?

- How many customers canceled their subscriptions this week?

- What’s the churn rate among subscribers on the monthly plan?

- What is the number of returning customers among our new subscribers?

- What percentage of new subscriptions come from returning customers?

## AWS architecture overview

![figure2](https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2025/03/25/ChurnIQ-Image-2-1.png)

*Figure 2: The AWS architecture of Cleeng’s ChurnIQ AI-ssistant.*

ChurnIQ AI-ssistant leverages AWS services like Amazon Bedrock, a fully managed service that offers a choice of industry leading foundation models (FMs) along with a broad set of capabilities needed to build generative AI applications.

Here is a walkthrough of the underlying AWS services used and the flow of the user’s prompt:

1. An end-user opens the ChurnIQ AI-assistant and asks a natural language query about the data, such as, “Give me a breakdown of churned subscribers by country.”

1. The request is sent to an Amazon API Gateway endpoint that invokes an AWS Lambda function.

1. The AWS Lambda function queries an Amazon DynamoDB table to check if the response for the model already exists. Prompts are cached within DynamoDB for six hours before being overwritten; enabling faster responses and reduced cost to run an identical inference request.

1. For a response that does not already exist, an AWS Lambda function parses the requests, and calls the Amazon Bedrock API with the prompt.

1. Amazon Bedrock, running Anthropic’s Claude foundation model, interprets the natural request and evaluates against Amazon Bedrock Guardrails settings to prevent the chatbot from responding to requests not related to ChurnIQ functionality. Amazon Bedrock generates the necessary schema to query the relevant data stores within ChurnIQ by leveraging pre-programmed prompt engineering to automatically select the relevant columns and filters for the requested data.

1. The ChurnIQ AI-ssistant assembles the dashboard for the user to review. The user can customize the chart by modifying filters, metrics, and dimensions. The user can optionally save the chart into their personal folder for later reference.

1. Finally, within the AI-ssistant interface, the end-user is presented with the ability to indicate positive or negative feedback on the response. That feedback request is passed through an Amazon API Gateway endpoint, parsed by a Lambda function, and then written to a DynamoDB table. The feedback enables the Cleeng product team to implement additional refinements to the prompt tuning and functionality over time.

## Outcomes and benefits

The Cleeng team chose Amazon Bedrock due to the ease of configuration and straightforward integration between Amazon API Gateway, AWS Lambda, and Amazon DynamoDB. This integration streamlined the development process for the ChurnIQ AI-ssistant. Additionally, the ability to utilize the Amazon Bedrock playgrounds to compare different models and responses accelerated the process of selecting the best model for the job.

ChurnIQ AI-ssistant was privately evaluated with customers prior to launch, and the following benefits were observed:

- Instant, accurate answers to critical questions about subscriber behavior, churn rates, and revenue trends.

- Actionable insights on the most successful campaigns and highest-risk customer segments.

- Discoverable campaign ideas based on subscriber behavior to inform opportunities to improve satisfaction and loyalty.

- Reduced data analyst and BI team backlog, enabling these teams to focus on high-value tasks.

## Conclusion

We showcased how Cleeng utilized Amazon Bedrock to integrate their ChurnIQ AI-ssistant to provide digital subscription platforms improved predictive analytics. These unified insights can proactively reduce churn and optimize customer lifetime value.

Learn more about Cleeng’s ChurnIQ solution and the AI-ssistant by view an interactive demo or contact their Sales Team.

Check out more AWS Partners or contact an AWS Representative to know how we can help accelerate your business.

## Further reading

- Getting started with Amazon Bedrock

- Guidance for Customer Data Analytics on AWS

- AWS Media & Entertainment Direct-to-Consumer & Streaming

**Jason O'Malley**

Jason O’Malley is a Sr. Partner Solutions Architect at AWS supporting partners architecting media, communications, and technology industry solutions. Before joining AWS, Jason spent 13 years in the media and entertainment industry at companies including Conan O’Brien’s Team Coco, WarnerMedia, and Media.Monks. Jason started his career in television production and post-production before building media workloads on AWS. When Jason isn’t creating solutions for partners and customers, he can be found adventuring with his wife and son, or reading about sustainability.

**Claudio Medeiros**

Claudio Medeiros is a Principal Solutions Architect at AWS with over 14 years of experience helping media and telecom companies innovate and build next-generation video platforms.

**Maggie Osude**

Maggie Osude is a Solutions Architect at AWS, helping enterprises optimize and scale their cloud infrastructure. She drives innovation in media workflows, AI/ML, and cloud efficiency, enabling customers to build scalable, high-performing solutions.