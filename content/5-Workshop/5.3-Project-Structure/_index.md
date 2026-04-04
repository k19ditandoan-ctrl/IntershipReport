---
title: "Project Structure"
date: 2026-04-03
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Slothub Project Structure

The project is structured as a mono-repository containing 4 main independent microservices. Each service can be developed and scaled individually. Below is an overview of the directories:

```text
Slothub/
├── frontend/
│   ├── src/                 # React components and pages
│   ├── public/              # Static assets
│   ├── package.json         # Node.js dependencies
│   └── .env                 # API Base URLs
├── backend/
│   ├── src/main/java        # Spring Boot Java source code
│   ├── src/main/resources   # application.yml and static assets
│   ├── pom.xml              # Maven dependencies
│   └── .env                 # Database credentials & JWT config
├── AI/
│   ├── main.py              # FastAPI application entrypoint
│   ├── services/            # OpenAI and S3 handling scripts
│   ├── requirements.txt     # Python dependencies
│   └── .env                 # OpenAI API key, S3 Bucket info
├── agent-core/
│   ├── app.py               # LangGraph state definition & Agent logic
│   ├── tools/               # Bedrock Agent tools (RAG, roadmap, quiz)
│   ├── requirements.txt     # Python dependencies
│   └── .env                 # AWS credentials and Local Dev flags
└── docker-compose.yml       # Shared PostgreSQL database with pgAdmin
```

#### Understanding the Components

- `frontend/`: The user interface built with React. It dynamically renders conversational widgets sent back from the agent using a specific protocol (`>>>[UI_WIDGET:TYPE|args]<<<`).
- `backend/`: The heart of logical operations. It handles User and Class hierarchy and issues JWT tokens via OAuth2 resource server architecture.
- `AI/`: The content factory. When teachers upload PDFs, this service analyzes them using OpenAI and generates study materials and questionnaires. The resulting files are safely pushed to AWS S3.
- `agent-core/`: The cognitive center (Slozy AI). Running with LangGraph framework, it processes student queries in real-time. By connecting to the shared database, it retrieves educational context through `pgvector` extension to implement RAG workflows.

In the next section, we will start by initializing our shared infrastructure using Docker and AWS.
