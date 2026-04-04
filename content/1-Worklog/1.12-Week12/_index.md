---
title: "Week 12 Worklog"
date: 2026-03-29
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### OBJECTIVES IN WEEK 12:
- Migrate the RAG system from development to AWS infrastructure using native services (RDS PostgreSQL + pgvector, Amazon Bedrock).
- Apply Infrastructure as Code (IaC) with Terraform to deploy RAG infrastructure automatically and consistently.
- Master Cost and Governance skills through advanced IAM Policies (Region limits, Instance Type limits).
- Setup comprehensive monitoring: Network layer (VPC Flow Logs), Application layer (Grafana), and AWS Service layer (CloudWatch).

### TASKS OF WEEK 12:

| Day | Task | Start Date | End Date | References |
|:---:|---|:---:|:---:|---|
| **Mon** | **- Team Project Meeting: Backend Development - RAG system (combined hybrid search engine and LLM):**<br>**- Research best practices for AWS services serving RAG system**<br>**- Proceed to migrate RAG system to AWS** | 30/03/2026 | 30/03/2026 | [RDS PostgreSQL](https://aws.amazon.com/vi/rds/postgresql/)<br>[pgvector](https://github.com/pgvector/pgvector)<br>[Postgres Full Text](https://www.postgresql.org/docs/current/textsearch.html)<br>[Claude 3.5 Haiku](https://aws.amazon.com/vi/about-aws/whats-new/2024/11/anthropics-claude-3-5-haiku-model-amazon-bedrock/)<br>[Claude 3.5 Sonnet](https://aws.amazon.com/vi/about-aws/whats-new/2024/06/anthropic-claude-3-5-sonnet-model-bedrock/) |
| **Tue** | **- Practice Lab 30: Cost and Resource Governance with IAM on AWS**<br>+ Preparation<br>* Create IAM Group<br>* Create IAM user<br>+ Limit by Region<br>* Create limit policy<br>* Attach policy to group<br>* Check policy effectiveness<br>+ Limit by EC2 family<br>* Create limit policy<br>* Attach policy to group<br>* Check policy effectiveness<br>+ Limit by instance size<br>* Update limit policy<br>* Check policy effectiveness<br>+ Limit by EBS volume<br>* Create limit policy<br>* Attach policy to group<br>* Check policy effectiveness<br>+ Resource Cleanup | 31/03/2026 | 31/03/2026 | [Lab 30 Intro](https://000064.awsstudygroup.com/vi/1-preparation/)<br>[Limit Region](https://000064.awsstudygroup.com/vi/2-limit-region/)<br>[Limit Family](https://000064.awsstudygroup.com/vi/3-limit-family/)<br>[Limit Size](https://000064.awsstudygroup.com/vi/4-limit-size/) |
| **Wed** | **- Practice Lab 31: Monitor Network Infrastructure with VPC Flow Logs**<br>+ Introduction<br>+ Preparation Steps<br>+ Enable VPC Flow Logs<br>+ Monitor Network Infrastructure<br>+ Resource Cleanup<br>**- Practice Lab 32: Getting Started with Grafana on AWS**<br>+ Introduction<br>+ Preparation Steps<br>* Create VPC and subnet<br>* Create Security Group<br>* Create EC2 Instance<br>* Create IAM User<br>* Create IAM Role<br>* Attach IAM Role<br>+ Install Grafana<br>+ Monitor with Grafana<br>+ Resource Cleanup | 01/04/2026 | 01/04/2026 | [Lab 31 Intro](https://000074.awsstudygroup.com/vi/1-introduce/)<br>[VPC Flow Logs](https://000074.awsstudygroup.com/vi/4-enablevpcflowlogs/)<br>[Lab 32 Intro](https://000029.awsstudygroup.com/vi/1-introduce/)<br>[Install Grafana](https://000029.awsstudygroup.com/vi/3-installgrafana/) |
| **Thu** | **- Team Project Meeting: Backend Development - RAG system (combined hybrid search engine and LLM):**<br>**- Complete RAG system migration to AWS with Infrastructure as Code using Terraform** | 02/04/2026 | 02/04/2026 | [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)<br>[Terraform CI/CD AWS](https://docs.aws.amazon.com/whitepapers/latest/cicd_for_5g_networks_on_aws/terraform.html)<br>[Terraform Tutorial](https://www.youtube.com/watch?v=wAwVOFf0Xq4) |
| **Fri** | **- Practice Lab 33: AWS CloudWatch Workshop**<br>+ Introduction<br>+ Preparation Steps<br>+ CloudWatch Metric<br>* Viewing Metrics<br>* Search expressions<br>* Math expressions<br>* Dynamic Labels<br>+ CloudWatch Logs<br>* CloudWatch Logs<br>* CloudWatch Logs Insights<br>* CloudWatch Metric Filter<br>+ CloudWatch Alarms<br>+ CloudWatch Dashboards<br>+ Resource Cleanup | 03/04/2026 | 03/04/2026 | [Lab 33 Intro](https://000036.awsstudygroup.com/vi/1-introduce/)<br>[Metrics](https://000036.awsstudygroup.com/vi/3-cloudwatchmetric/)<br>[Logs](https://000036.awsstudygroup.com/vi/4-cloudwatchlogs/)<br>[Alarms](https://000036.awsstudygroup.com/vi/5-cloudwatchalarm/) |

### ACHIEVEMENTS IN WEEK 12:
1. Successfully migrated the RAG system to AWS, utilizing RDS PostgreSQL (pgvector) as the Vector Database and Amazon Bedrock (Claude Models) as the LLM.
2. Automated RAG Backend infrastructure deployment using Terraform, ensuring consistency and scalability.
3. Established strict IAM policies to control resource creation, prevent budget overruns (Cost Control), and ensure security.
4. Built a multi-layer monitoring system: Tracking network traffic with VPC Flow Logs and visualizing Application Metrics on Grafana/CloudWatch Dashboards.