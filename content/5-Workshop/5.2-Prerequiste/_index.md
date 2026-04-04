---
title: "Prerequisites"
date: 2026-04-03
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Prerequisites

To set up the Slothub microservice architecture locally, you will need the following tools and accounts:

#### 1. Developer Environment
- **Java Development Kit (JDK) 17**: Required to build and run the Spring Boot backend service.
- **Node.js (v18 or higher) and npm**: Necessary for running the React/TypeScript/Vite frontend.
- **Python (3.10 to 3.12)**: Used for both the FastAPI AI Service (3.12 recommended) and the LangGraph Agent-Core (3.10 recommended).
- **Docker & Docker Compose**: The easiest way to run the shared PostgreSQL database with the `pgvector` extension locally. 
- **Git**: To clone and manage the codebase.

#### 2. Cloud Accounts & API Keys
Because Slothub's AI components leverage cloud language models and storage options, you need:
- **AWS Account**:
  - An **S3 Bucket** (e.g., in `ap-southeast-1`) for storing uploaded PDF files and generated contents.
  - Access keys (`AWS_ACCESS_KEY`, `AWS_SECRET_KEY`) with permissions to read/write to S3 and invoke AWS Bedrock operations.
- **OpenAI API Key**: Required by the FastAPI service for embeddings and automated content generation tasks.

#### 3. IDE / Editors
- **Visual Studio Code** or **IntelliJ IDEA**: For backend and frontend development.
- **pgAdmin** or **DBeaver**: For visualizing database records, included in the docker-compose template.

Once you have these tools installed and API keys generated, you're ready to proceed to the project structure and deployment steps.
