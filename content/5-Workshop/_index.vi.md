---
title: "Workshop"
date: 2026-04-03
weight: 5
chapter: false
pre: " <b> 5. </b> "
alwaysopen: true
---
# Slothub — Xây dựng Nền tảng Học tập & Quản lý Lớp học Thông minh với AI

#### Tổng quan

**Slothub** là một nền tảng học trực tuyến sáng tạo, tích hợp AI đa tầng để mang đến trải nghiệm giáo dục cá nhân hóa sâu sắc và thông minh. Được xây dựng với kiến trúc microservice, dự án tận dụng các framework phát triển hiện đại và dịch vụ đám mây AWS để cung cấp một giải pháp thông minh, có khả năng mở rộng cho cả giáo viên và học sinh.

Trong workshop này, bạn sẽ học cách:
- Thiết lập môi trường phát triển cục bộ sử dụng Docker Compose cho PostgreSQL
- Hiểu về kiến trúc microservice (React, Spring Boot, FastAPI, Bedrock AgentCore)
- Cấu hình các dịch vụ AWS cần thiết như S3 để lưu trữ file và Bedrock cho AI
- Chạy các dịch vụ backend, AI và frontend React trên local
- Trải nghiệm luồng hoạt động từ đầu đến cuối của một ứng dụng giáo dục hỗ trợ bởi AI

Dự án thể hiện các mẫu kiến trúc phần mềm hiện đại sử dụng:
- **Backend Toàn diện** — Java 17 + Spring Boot 3.5 cho REST API mạnh mẽ, xác thực (JWT/OAuth2), và quản lý lớp học
- **Dịch vụ Generative AI** — Python 3.12 + FastAPI để tự động tạo bài tập, lộ trình học, và xử lý tài liệu (qua OpenAI & AWS S3)
- **Gia sư AI Slozy** — LangGraph ReAct Agent triển khai trên AWS Bedrock AgentCore cho hội thoại RAG-tutoring với pgvector
- **Frontend Hiện đại** — React 18 với TypeScript, Vite và TailwindCSS
- **Cơ sở dữ liệu Container hóa** — PostgreSQL với pgvector extension được triển khai qua Docker Compose

#### Nội dung

1. [Tổng quan về Workshop](5.1-Workshop-overview/)
2. [Yêu cầu tiên quyết](5.2-Prerequiste/)
3. [Cấu trúc dự án](5.3-Project-Structure/)
4. [Thiết lập hạ tầng](5.4-Infrastructure-Setup/)
5. [Phát triển & Triển khai](5.5-Deployment/)
6. [Dọn dẹp](5.6-Cleanup/)
7. [Cấu hình Biến Môi trường](5.7-Environment-Config/)
8. [Backend Spring Boot](5.8-Backend-Deep-Dive/)
9. [Dịch vụ AI (FastAPI)](5.9-AI-Service-Deep-Dive/)
10. [Agent-Core & Slozy AI](5.10-Agent-Core-Slozy/)
11. [Frontend React](5.11-Frontend-Integration/)
12. [Triển khai AWS Cloud](5.12-AWS-Cloud-Deployment/)
