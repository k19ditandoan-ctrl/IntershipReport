---
title: "Week 10 Worklog"
date: 2026-03-15
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### OBJECTIVES IN WEEK 10:
- Research and design the Backend architecture supporting Hybrid Search (combining keyword and semantic search) for the project.
- Master comprehensive Serverless architecture: From event processing (S3 triggers), storage (DynamoDB) to API building (API Gateway).
- Build an automated CI/CD pipeline for Serverless applications using AWS CodePipeline.
- Practice in-depth Serverless application Monitoring and Tracing with CloudWatch and X-Ray.
- Expand community connections and learn about Agentic AI.

### TASKS OF WEEK 10:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Team Project Meeting: Backend Development - Hybrid Search Engine (Text search + semantic search):**<br>- Research best practices and papers on hybrid search engines<br>- Design preliminary hybrid search engine architecture | 16/03/2026 | 16/03/2026 | [Paper](https://arxiv.org/pdf/2408.09236)<br>[Medium Article](https://medium.com/tech-learnings/hybrid-search-in-search-engines-bridging-the-gap-between-keywords-and-context-e8c5f6cabd6c)<br>[Meilisearch](https://www.meilisearch.com/blog/hybrid-search)<br>[Google Vertex AI](https://docs.cloud.google.com/vertex-ai/docs/vector-search/about-hybrid-search) |
| **Tue** | **- Practice Lab 22: Serverless - Lambda interaction with S3 and DynamoDB**<br>+ Introduction<br>+ Image Processing and Optimization on AWS<br>* Create Image Processing Lambda Function<br>* Create S3 Bucket<br>* Create IAM Policy for Lambda Function<br>* Test Lambda Function<br>+ Write data to Amazon DynamoDB<br>* Create and Manage Tables in AWS DynamoDB<br>* Create Lambda Function to Write data<br>+ Resource Cleanup | 17/03/2026 | 17/03/2026 | [Lab 22 Intro](https://000078.awsstudygroup.com/vi/1-introduce/)<br>[Resize Function](https://000078.awsstudygroup.com/vi/2-resize-image-function/)<br>[DynamoDB Write](https://000078.awsstudygroup.com/vi/3-write-data-to-dynaomodb/) |
| **Wed** | **- Practice Lab 23: Serverless - Guide to writing Front-end calling API Gateway**<br>+ Introduction to API Gateway / DynamoDB<br>+ Deploy front-end<br>+ Deploy Lambda function<br>* Create table in DynamoDB<br>* Deploy Lambda function<br>Lambda function writes data<br>Lambda function reads data<br>Lambda function deletes data<br>+ Setup API Gateway<br>* Create methods<br>* Configure and enable CORS<br>+ Test API with Postman<br>+ Test API with front-end<br>+ Resource Cleanup | 18/03/2026 | 18/03/2026 | [Lab 23 Intro](https://000079.awsstudygroup.com/vi/1-introduction/)<br>[Deploy Frontend](https://000079.awsstudygroup.com/vi/2-front-end-deployment/)<br>[API Gateway](https://000079.awsstudygroup.com/vi/4-config-api-gw/)<br>[Postman Test](https://000079.awsstudygroup.com/vi/5-test-api-by-postman/) |
| **Thu** | **- Team Project Meeting: Backend Development - Hybrid Search Engine (Text search + semantic search):**<br>- Run and test hybrid search engine with collected data<br>- Finalize hybrid search engine architecture | 19/03/2026 | 19/03/2026 | [Supabase AI](https://supabase.com/docs/guides/ai/hybrid-search)<br>[MongoDB Hybrid](https://www.mongodb.com/resources/products/capabilities/hybrid-search)<br>[AWS OpenSearch](https://aws.amazon.com/vi/blogs/big-data/hybrid-search-with-amazon-opensearch-service/)<br>[Amazon Bedrock](https://aws.amazon.com/vi/blogs/machine-learning/amazon-bedrock-knowledge-bases-now-supports-hybrid-search/) |
| **Fri** | **- Practice Lab 24: Serverless - CI/CD with CodePipeline**<br>+ Preparation<br>+ Build SAM pipeline<br>* Create Git repository<br>* Create SAM pipeline<br>+ Build front-end pipeline<br>* Create Git repository<br>* Create pipeline<br>+ Test web operation<br>+ Cleanup<br>**- Practice Lab 25: Serverless - Monitoring Serverless applications with CloudWatch and X-Ray**<br>+ Preparation<br>+ Monitor with CloudWatch<br>* Debug with CloudWatch Logs<br>* Create custom metrics<br>* Create alarms with CloudWatch Alarm<br>+ Trace with X-ray<br>+ Cleanup | 20/03/2026 | 20/03/2026 | [Lab 24 Intro](https://000084.awsstudygroup.com/vi/1-preparation/)<br>[SAM Pipeline](https://000084.awsstudygroup.com/vi/2-build-sam-pipeline/)<br>[Lab 25 Intro](https://000085.awsstudygroup.com/vi/1-preparation/)<br>[CloudWatch](https://000085.awsstudygroup.com/vi/2-cloudwatch-monitor/)<br>[X-Ray](https://000085.awsstudygroup.com/vi/3-x-ray-trace/) |
| **Sat** | **- Attend Event: AWS Community Day Vietnam** | 21/03/2026 | 21/03/2026 | [Event Info](https://aws-community-day-vietnam-2025.awsstudygroup.com/) |

### ACHIEVEMENTS IN WEEK 10:
1. Successfully designed and tested the Hybrid Search Engine architecture, leveraging both traditional keyword search and vector (Semantic) search.
2. Built a complete Serverless Backend workflow: Automated image processing with S3 Triggers and NoSQL data management with DynamoDB.
3. Successfully deployed a Full-stack Serverless App: Connected Frontend to Backend via API Gateway and Lambda, effectively handling CORS issues.
4. Established an automated DevOps process (CI/CD) for Serverless applications, enabling rapid and error-free deployment of Code and Frontend.
5. Enhanced system operational capability by setting up Monitoring Dashboards (CloudWatch) and Request Tracing (X-Ray) for effective debugging.