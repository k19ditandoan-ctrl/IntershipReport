---
title : "Introduction"
date: 2026-04-03
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### About Slothub (Slothub)

**Slothub (Slothub)** is an intelligent online learning and management platform designed to unify the teaching and learning experience. It replaces disconnected tools (gradebooks, chat groups, assignment forms) with an all-in-one ecosystem enhanced by Artificial Intelligence. 

The platform leverages powerful technologies including:
- **AWS Bedrock AgentCore** - Powering **Slozy Assistant**, a conversational AI tutor that uses LangGraph ReAct Agent architecture and RAG (Retrieval-Augmented Generation) against a PostgreSQL pgvector database to ensure accurate, curriculum-based answers.
- **OpenAI API** - For automated document parsing and generative content (exercises, learning roadmaps).
- **Amazon S3** - For secure, structured storage of uploaded course materials (PDF documents) and generated assets.
- **Java Spring Boot** - Providing a robust REST API backend for core educational domain logic (classrooms, users, assignments, timetables).

#### Workshop Overview

In this workshop, you will learn how to initialize, configure, and locally deploy Slothub's microservice architecture:

- **Frontend (`frontend/`)**: React 18, TypeScript, Vite, Tailwind CSS. This component handles the user interface and dynamically renders AI output widgets.
- **Backend (`backend/`)**: Spring Boot 3.5, Java 17. Handles user authentication (JWT/OAuth2), data management, and the core educational domains.
- **AI Service (`AI/`)**: Python 3.12, FastAPI. Responsible for automated content generation, S3 file uploading, and proxying requests to the AI model.
- **Agent-Core (`agent-core/`)**: Python 3.10, LangGraph. The brain behind the Slozy AI Assistant, running locally with `MemorySaver` for testing or AWS Bedrock for production.
- **Database**: PostgreSQL with pgvector extension running easily via **Docker Compose**.

#### Architecture Overview

The Slothub platform follows a microservice/Agentic AI approach:

1. **User Interaction**: Users access the React frontend.
2. **Core Logic**: Frontend calls the Spring Boot API for authentication and classroom data.
3. **AI Workloads**: Frontend/Backend delegates content generation requests to the FastAPI Python service which calls OpenAI APIs and interact with AWS S3.
4. **Intelligent Tutoring**: The chat component interacts with the Agent-Core (Slozy) to perform RAG over PostgreSQL pgvector context.
5. **Data Layer**: All services share a unified PostgreSQL database managed via Docker Compose.

![Slothub Architecture](/images/2-Proposal/Achitecture-Page-1.drawio.svg)
