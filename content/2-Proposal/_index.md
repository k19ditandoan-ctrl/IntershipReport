---
title: "Proposal"
date: "2026-04-03"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Slothub - Agentic Learning & Management Platform
*(Optimizing teaching and learning through class management, AI-driven content, and personalized tutoring)*

---

## 1. Executive Summary

**Slothub** is a comprehensive web-based ecosystem designed for teachers, students, and administrators to synchronize educational activities on a single platform. The platform manages classroom lifecycles, timetables, attendance, and assignments, while integrating a **Multi-layered AI architecture** (Slozy AI Tutor) to provide personalized learning roadmaps and RAG-based knowledge retrieval.

Our team of 5 IT students is developing Slothub using a modern **microservice architecture** deployed on **AWS (ap-southeast-1)** with a **Multi-AZ design** for high availability. The system integrates a **React/TypeScript frontend**, a **Spring Boot backend**, a **FastAPI AI service**, and **AWS Bedrock AgentCore** for the agentic tutor.

The goal is to reduce administrative burdens for educators while empowering students with guided, self-paced learning tools, leveraged by scalable AWS services such as Fargate, RDS PostgreSQL, and S3.

---

## 2. Problem Statement

### What is the Problem?

- **Fragmented Tools**: Teachers must navigate multiple disconnected platforms (gradebooks, chat apps, files) for data management, leading to inefficiency.
- **Lack of Personalization**: Traditional e-learning offers a "one-size-fits-all" approach that fails to adapt to individual student knowledge gaps and learning paces.
- **Administrative Overload**: educators spend significant time on repetitive tasks like manual exercise creation and content compilation.
- **Static Interactions**: Existing solutions lack intelligent conversational interfaces capable of providing contextual guidance outside of classroom hours.

### The Solution

Slothub centralizes educational data and workflows on a unified stack:
- **Unified Management**: Spring Boot API and RDS PostgreSQL for core operational data.
- **AI-Generated Content**: Dedicated containerized AI services calling **OpenAI & AWS Bedrock** for automated material generation stored on **S3**.
- **Agentic Tutoring**: **Slozy AI Tutor** (powered by Bedrock AgentCore) provides step-by-step guidance using **RAG (Retrieval-Augmented Generation)** from theory databases instead of generating hallucinatory content.
- **High Availability**: Multi-AZ deployment for both database and application layers via **ALB** and **Fargate**.

### Benefits and ROI

- **Centralization**: All study tracks, classroom management, and assignments on one platform.
- **Personalized Learning**: Adaptive roadmaps, quizzes, and AI tutoring based on curriculum context.
- **Scalability**: Containerized microservices allowing independent scaling via ECS Fargate.
- **Operational Reliability**: Multi-AZ RDS and Fargate with monitoring via **CloudWatch** and security from **GuardDuty**.
- **Cost Control**: Optimized resource usage via Serverless execution (Fargate, Bedrock) and caching strategies.

---

## 3. Solution Architecture

### Overview

User Access → **Amazon Cognito (Auth)** → **WAF & ALB** → **ECS Fargate (Backend / AI Services)** → **RDS PostgreSQL (Multi-AZ)** & **S3 (Documents)**. The AI Assistant interacts with **Amazon Bedrock AgentCore** for intelligent tutoring logic.

![Slothub Architecture](/images/2-Proposal/Achitecture-Page-1.drawio.svg)

### AWS Services Used

| Service | Function |
|---------|----------|
| **Amazon Cognito** | User authentication and authorization |
| **Amazon Route 53** | Domain routing and DNS management |
| **AWS WAF** | Web application firewall for threat protection |
| **AWS Amplify** | Frontend hosting and management |
| **AWS Certificate Manager** | SSL/TLS certificate management |
| **Amazon VPC + IGW** | Private networking with controlled internet access |
| **Application Load Balancer** | Traffic distribution to container services |
| **Amazon ECS on Fargate** | Serverless execution for Backend (Spring Boot) and AI (FastAPI) |
| **Amazon ECR** | Docker image repository for microservices |
| **Amazon RDS (PostgreSQL)** | Relational database with Multi-AZ Primary/Standby |
| **Amazon S3** | Storage for documents, assignments, and uploads |
| **Amazon Bedrock (AgentCore)** | AI Tutor agent and generative language models |
| **Amazon CloudWatch** | Resource monitoring and logging |
| **Amazon GuardDuty** | Intelligent threat detection |

---

## 4. Technical Implementation

### Implementation Phases

| Phase | Description | Suggested Duration |
|-------|-------------|--------------------|
| 1 | Infrastructure setup (VPC, ALB, Fargate, RDS Multi-AZ, S3, Cognito), IaC/CI basics | 2-3 weeks |
| 2 | RDS Schema design, Spring Boot API development, and Cognito integration | 3-4 weeks |
| 3 | AI Service (FastAPI) deployment, S3 document pipeline, Bedrock connectivity | 2-3 weeks |
| 4 | AgentCore (Slozy) implementation, tool binding to PostgreSQL and AI API | 2 weeks |
| 5 | Frontend production build, Amplify deployment, WAF/ACM/Route 53 configuration | 2 weeks |
| 6 | Load testing, CloudWatch observation, and cost/security tuning (GuardDuty) | 1-2 weeks |

### Technical Requirements

- **Client**: Modern web browsers (Responsive interface).
- **Backend**: Java 17, Spring Boot 3.x, Spring Security (OAuth2/JWT).
- **AI Services**: Python 3.x, FastAPI, AWS SDK (Boto3) for S3 and Bedrock.
- **Agent Core**: LangGraph/LangChain, Bedrock AgentCore SDK.
- **CI/CD**: GitHub Actions for Docker build, ECR push, and ECS update.

---

## 5. Timeline & Milestones

| Milestone | Activity |
|-----------|----------|
| Preparation | Finalize ERD/API contracts, User Roles, and Data Policies |
| Core Development | Classrooms, Assignments, Timetable, and Attendance modules |
| AI Integration | FastAPI + S3 + Bedrock; Slozy AI Assistant |
| Deployment | Production setup with ECR, Fargate, ALB, Amplify, and WAF |
| Operation | Monitoring, RDS backups, and security auditing |

---

## 6. Budget Estimation

### Resource Investment Time

Total investment for the 5-member team contributing 20 hours/week over three phases:
- **Phase 1: Platform Setup**: 200 hours
- **Phase 2: Core Features**: 200 hours
- **Phase 3: Completion & Deployment**: 200 hours
- **Total Estimated Time**: **600 hours**

### Cloud Infrastructure Costs

- **Hedged Costs**: Utilizing the **AWS Free Tier** and credits package ($200) for development and initial deployment.
- **Primary Items**: Monitoring costs for RDS Multi-AZ, Fargate tasks, and Bedrock token usage via CloudWatch.
- **Optimization**: Rightsizing Fargate resources and implementing Bedrock caching.

---

## 7. Risk Assessment

| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Data Sync Issues (Backend/AI) | High | Medium | API contracts, idempotent uploads, handled transactions |
| Bedrock Cost Overrun | High | Medium | Quota limits, result caching, optimized prompts |
| RDS Failover Latency | Medium | Low | Multi-AZ deployment, automated health checks |
| Security Breaches (API/S3) | High | Medium | IAM least privilege, WAF, Encryption at rest, GuardDuty |
| AI Output Quality | Medium | Medium | Prompt engineering, curriculum-restricted knowledge base |

---

## 8. Expected Outcomes

### Success Criteria

- **Functional MVP**: Successfully manage classrooms, assignments, and AI-driven tutoring for the pilot group.
- **Full Infrastructure**: Secure deployment on AWS using ECS Fargate, RDS Multi-AZ, and Cognito.
- **Performance**: Acceptance latency for teacher/student interactions (monitored via CloudWatch).
- **AI Accuracy**: Slozy AI Tutor successfully retrieves valid theory via RAG for >90% of curriculum queries.
- **Budget Control**: Operates within the $200 AWS credit budget.

### Long-term Value

- **Extended Content**: Automated Question Bank expansion and AI analytics for student progress.
- **Scalability**: Mobile application support and organization-wide multi-tenancy.
- **Efficiency**: Transitioning from administrative management to AI-augmented teaching.

---

## 9. References

- [AWS Pricing Calculator](https://calculator.aws/)
- Amazon Bedrock AgentCore and Amazon ECS Fargate Documents
- Project repository: `frontend`, `backend`, `AI`, `agent-core` folders.
