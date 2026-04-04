---
title: "Workshop"
date: 2026-04-03
weight: 5
chapter: false
pre: " <b> 5. </b> "
alwaysopen: true
---
# Slothub — Building an AI-Powered Learning & Classroom Management Platform

#### Overview

**Slothub** is an innovative online learning platform integrating multi-layered AI to deliver a deeply personalized educational experience. Built with a microservice architecture, the project leverages modern development frameworks and AWS cloud services to provide a scalable, intelligent solution for both teachers and students.

In this workshop, you will learn how to:
- Set up a local development environment using Docker Compose for PostgreSQL
- Understand a microservice architecture (React, Spring Boot, FastAPI, Bedrock AgentCore)
- Configure necessary AWS services including S3 for file storage and Bedrock for AI capabilities
- Run backend services, AI engines, and the React frontend locally
- Experience the end-to-end flow of an AI-powered educational application

The project demonstrates modern software architecture patterns using:
- **Comprehensive Backend** — Java 17 + Spring Boot 3.5 for robust REST API endpoints, authentication (JWT/OAuth2), and classroom management
- **Generative AI Services** — Python 3.12 + FastAPI for automated exercise generation, learning roadmaps, and document processing (via OpenAI & AWS S3)
- **Agentic AI Tutor (Slozy)** — LangGraph ReAct Agent deployed on AWS Bedrock AgentCore for conversational, RAG-based tutoring with pgvector
- **Modern Frontend** — React 18 with TypeScript, Vite, and TailwindCSS
- **Containerized Database** — PostgreSQL with pgvector extension deployed via Docker Compose

#### Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Project Structure](5.3-Project-Structure/)
4. [Infrastructure Setup](5.4-Infrastructure-Setup/)
5. [Development & Deployment](5.5-Deployment/)
6. [Cleanup](5.6-Cleanup/)
7. [Environment Configuration](5.7-Environment-Config/)
8. [Backend Spring Boot](5.8-Backend-Deep-Dive/)
9. [AI Service (FastAPI)](5.9-AI-Service-Deep-Dive/)
10. [Agent-Core & Slozy AI](5.10-Agent-Core-Slozy/)
11. [Frontend React](5.11-Frontend-Integration/)
12. [AWS Cloud Deployment](5.12-AWS-Cloud-Deployment/)
