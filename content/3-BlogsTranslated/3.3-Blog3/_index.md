---
title: "Blog 3"
date: ""
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Cloud cost savings: 10 tips for academic institutions

![figure1](https://d2908q01vomqb2.cloudfront.net/9e6a55b6b4563e652a23be9d623ca5055c356940/2025/04/10/AWS-Public-Sector-Blog-Featured-Images-Blog-Header-static-template-Autosaved-13.png)

When using cloud services, one of the key benefits is the ability to match resources to demand – and avoid purchasing resources above what is needed. This is in contrast to the traditional model of purchasing equipment on-premises, where resources are typically sized for anticipated peak usage across the lifespan of the equipment. This fundamental concept of the cloud can sometimes be overlooked when organizations first migrate to the cloud, and they end up behaving as if they are still locked into a fixed infrastructure model.

For academic institutions leveraging cloud services, it is important to proactively manage and optimize cloud costs. Though the following content is geared toward higher education users, many of the points below are helpful to others:

Here are 10 tips to help control cloud costs using Amazon Web Services (AWS):

## 1. Set up AWS budget alerts

Utilize AWS Budgets to set up alerts, especially for anomalous spending. This will help you stay on top of usage and avoid unexpected cost spikes.

This is especially helpful if you are taking advantage of services on the Free Tier and you want to ensure that you aren’t surprised upon expiry.

Guidance on how to create a budget can be found here.

## 2. Right-size resources

Identify underutilized resources, such as over-provisioned Amazon Elastic Cloud Compute (Amazon EC2) instances, Amazon Relational Database Service (Amazon RDS) instances, or Amazon Elastic Block Store (Amazon EBS) volumes. Consider downsizing these resources or exploring alternative instance types like Graviton-based EC2 instances to optimize costs. For those enrolled in Business or Enterprise levels of AWS Support, AWS Trusted Advisor can provide recommendations for right-sizing.

AWS Compute Optimizer is also a tool that can be used to evaluate EC2 instances, Amazon EC2 Auto Scaling groups, EBS volumes, AWS Lambda functions, RDS databases, and Amazon Elastic Container Service (Amazon ECS) services on AWS Fargate. After enrolling in Compute Optimizer, one can then get recommendations from Compute Optimization Hub found on the “Billing and Cost Management” page within your AWS Console.

As resources change over time, ongoing monitoring is important.

## 3. Leverage EC2 Spot Instances

For fault-tolerant, batch-oriented workloads common in academic computing, EC2 Spot Instances can provide significant cost savings of up to 90% compared to on-demand pricing.

## 4. Pause instances after hours

Implement auto-scaling policies to shut down EC2 instances during non-business hours, and then restart them when needed. This can help reduce costs for resources that are not needed 24/7. Another method to accomplish this strategy is to implement Instance Scheduler.

## 5. Utilize Amazon Simple Storage Service (Amazon S3) lifecycle policies

Optimize your S3 storage costs by implementing lifecycle policies to automatically move lesser-used objects to cheaper storage tiers, such as Amazon S3 Glacier Instant Retrieval or S3 Glacier Deep Archive.

Amazon S3 Storage Lens and Amazon S3 Analytics are tools that can be used to analyze usage of S3 objects and can be helpful with creating lifecycle policies for your S3 storage objects. 

## 6. Right-size backup retention policies

Review your backup retention policies, especially for non-critical or non-production workloads. Reducing unnecessary backup retention can lead to cost savings.

Production workloads may have regulatory retention requirements (e.g., 3 or 7 years). For simplicity purposes, it may be easiest to have non-production workloads with the exact same retention, but from a cost point of view, it would be excessive to retain backups that will never be restored and no reason to preserve them for the same duration.

## 7. Consider Amazon S3 Intelligent-Tiering

Amazon S3 Intelligent-Tiering automatically moves objects between access tiers based on usage patterns, ensuring you’re always using the most cost-effective storage tier.

## 8. Delete orphaned storage

Identify and delete any unattached EBS volumes, snapshots, or incomplete S3 uploads that are no longer needed. See the associated links which will point to the different methods.

Using Amazon Data Lifecycle Manager to manage EBS snapshot volumes is a best practice.

## 9. Aggregate accounts under fewer payer accounts

For institutions with multiple AWS accounts, consider consolidating them under fewer payer accounts. This can unlock benefits like the Global Data Egress Waiver for higher education customers, as well as potential network resource savings.

For those who cannot take advantage of the Global Data Egress Waiver, consider using CloudFront to reduce network traffic out to the Internet from publicly facing web pages.

## 10. Utilize AWS Savings Plans and Reserved Instances

For consistent, long-term usage of resources like EC2, Lambda, Amazon Sagemaker AI, and RDS consider Savings Plans or Reserved Instances to lock in discounted pricing for 1-3 years. From the menus on the “Billing and Cost Management” page within the AWS Console, there are Savings Plan and Reservation recommendations based on your workloads. One will want to proceed with right-sizing before this step, so that the recommendations can be based on one’s adjusted workloads. Savings Plans and Reserved Instances can provide up to 72% discounts compared to On-Demand pricing.

## Bonus #1: Tax Exemption

Many public sector entities qualify for tax exemption. Typically, this needs to be configured on the billing console for each of one’s member accounts. For more details, see this link.

## Bonus #2: No cost education and support resources

Want to learn about AWS Services? Sign up for a Skill Builder account. There are paid and no cost options. Watch videos on the AWS Twitch Channel or the AWS YouTube Channel. Read additional content on AWS Blogs.

Need Support? Ask a question or explore prior answers on the AWS Community site: re:Post. Questions are answered by AWS Specialists, Generative AI automation, and other members of the community.

Additionally, for those with support agreements, one can open a case from their console to get general guidance or specific assistance.

Finally, if you want to learn more about cost optimization, see the AWS Well-Architected Cost Optimization Workshop. This workshop focuses on the Cost Optimization pillar and is designed to provide hands-on guidance to explain best practices.

And of course, check with your AWS account team to further explore options to run workshops for your campus. If your campus has an Enterprise Support agreement, your assigned Technical Account Manager can provide guidance as well.

**Jim Surlow**

Jim is a senior technical account manager (TAM) and enterprise support lead with over 35 years of IT experience. His team of TAMs support Higher Education AWS customers in the western United States. He also a member of both the AWS Storage and Education Technical Field Communities.