---
title: "Week 6 Worklog"
date: 2026-02-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### OBJECTIVES IN WEEK 6:
- Understand and apply Serverless architecture (AWS Lambda) for automation (Cost Optimization) and Event-driven processing.
- Master the interaction between Lambda, storage services (S3), and NoSQL databases (DynamoDB).
- Master the AWS Command Line Interface (CLI) to manage resources professionally and efficiently.
- Finalize the Solution Architecture and Budget Estimation for the team project.

### TASKS OF WEEK 6:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Team Project Meeting: Define and research solution architecture for the web app** | 09/02/2026 | 09/02/2026 | [Proposal Guide](https://workshop-sample.fcjuni.com/2-proposal/) |
| **Tue** | **- Practice Lab 13: EC2 Cost Optimization with Lambda**<br>+ Introduction<br>+ Preparation Steps<br>* Create VPC<br>* Create Security Group<br>* Create EC2 instance<br>* Incoming Web-hooks slack<br>+ Create Tag for Instance<br>+ Create Role for Lambda<br>+ Create Lambda Function<br>* Function stop instance<br>* Function start instance<br>+ Check results<br>+ Resource Cleanup | 10/02/2026 | 10/02/2026 | [Lab 13 Intro](https://000022.awsstudygroup.com/vi/1-introduce/)<br>[Create Role](http://000022.awsstudygroup.com/vi/4-createroleforlambda/)<br>[Lambda Function](https://000022.awsstudygroup.com/vi/5-createlambdafunction/) |
| **Wed** | **- Practice Lab 14: Serverless - Lambda interaction with S3 and DynamoDB**<br>+ Introduction<br>+ Image Processing and Optimization on AWS<br>* Create Image Processing Lambda Function<br>* Create S3 Bucket<br>* Create IAM Policy for Lambda Function<br>* Test Lambda Function<br>+ Write data to Amazon DynamoDB<br>* Create and Manage Tables in AWS DynamoDB<br>* Create Lambda Function to Write data<br>+ Resource Cleanup | 11/02/2026 | 11/02/2026 | [Lab 14 Intro](https://000078.awsstudygroup.com/vi/1-introduce/)<br>[Resize Function](https://000078.awsstudygroup.com/vi/2-resize-image-function/)<br>[DynamoDB Write](https://000078.awsstudygroup.com/vi/3-write-data-to-dynaomodb/) |
| **Thu** | **- Attend workshop: Data Science on AWS - Unlocking data power with cloud computing**<br>**- Team Project Meeting: Finalize solution architecture, budget estimation for web app** | 12/02/2026 | 12/02/2026 | [AWS Calculator](https://calculator.aws/#/) |
| **Fri** | **- Practice Lab 15: Getting started with AWS CLI**<br>+ Introduction<br>+ Preparation Steps<br>+ Install AWS CLI<br>+ Check resources via CLI<br>+ AWS CLI with Amazon S3<br>+ AWS CLI with Amazon SNS<br>+ AWS CLI with IAM<br>+ AWS CLI with VPC<br>* AWS CLI with VPC<br>* AWS CLI with Internet Gateway<br>+ Create EC2 using AWS CLI<br>+ Troubleshooting<br>+ Resource Cleanup | 13/02/2026 | 13/02/2026 | [Lab 15 Intro](https://000011.awsstudygroup.com/vi/1-introduce/)<br>[Install CLI](https://000011.awsstudygroup.com/vi/3-installcli/)<br>[CLI with EC2](https://000011.awsstudygroup.com/vi/9-ec2/) |

### ACHIEVEMENTS IN WEEK 6:
1. Successfully implemented automated cost-saving solution (Lab 13): Used Lambda to Stop/Start EC2 instances on schedule and integrated Slack notifications.
2. Built a Serverless image processing application (Lab 14): Combined Lambda, S3, and DynamoDB to automatically resize images and store metadata.
3. Completed the detailed Solution Architecture design and Cost Estimation for the final capstone project.
4. Expanded knowledge on Data Science on AWS platform through the specialized workshop.
5. Proficiently used AWS CLI (Lab 15) to manipulate core services (S3, EC2, VPC, IAM) without using the Console interface.