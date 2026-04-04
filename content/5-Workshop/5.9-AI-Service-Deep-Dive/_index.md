---
title: "AI Service (FastAPI)"
date: 2026-04-03
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

#### AI Service Overview

Slothub's AI Service is built using **Python 3.12 + FastAPI**, functioning as an automated educational content factory. The service runs on port `8000` and handles three primary tasks: **exercise generation**, **learning roadmap creation**, and **document management**.

#### Service Architecture

```text
AI/
├── main.py                # FastAPI entrypoint - route definitions
├── services/
│   ├── openai_service.py  # OpenAI integration (embedding + generation)
│   ├── s3_service.py      # AWS S3 file upload/download
│   ├── document_service.py# PDF document processing
│   └── roadmap_service.py # Learning roadmap generation logic
├── models/                # Pydantic models for request/response
├── requirements.txt       # Python dependencies
└── .env                   # Environment configuration
```

#### Key Features

##### 1. Automated Exercise Generation from PDFs

When a teacher uploads a PDF document, the following pipeline executes:

```
1. Teacher uploads PDF via Frontend
2. Frontend sends file to FastAPI endpoint
3. FastAPI stores file on AWS S3 (bucket: Slothub-upload-2026)
4. Text content is extracted from PDF
5. Content is sent to OpenAI API for analysis
6. OpenAI generates exercises/questions based on content
7. Results are returned to Frontend for display
```

{{% notice tip %}}
Files are stored in a structured manner on S3 (region `ap-southeast-1`), using naming conventions based on classroom and subject for easy management.
{{% /notice %}}

##### 2. Learning Roadmap Generation

The `/roadmap` endpoint analyzes a student's current knowledge and generates a personalized study roadmap:

```python
# Example roadmap creation flow
POST /api/v1/roadmap
{
    "subject": "Math Grade 12",
    "current_level": "intermediate",
    "target": "final exam",
    "weeks_available": 4
}

# Response: Detailed weekly roadmap
{
    "roadmap": [
        {"week": 1, "topics": ["Derivatives", "Extrema"], "exercises": 15},
        {"week": 2, "topics": ["Basic Integration"], "exercises": 20},
        ...
    ]
}
```

##### 3. Chat Proxy to Slozy Agent

FastAPI acts as an **intermediary proxy** for chat messages, forwarding them from the frontend to the Agent-Core (Slozy AI):

```
Frontend → FastAPI (proxy) → Agent-Core (Slozy)
                                ↓
                          AWS Bedrock AgentCore
                                ↓
                       PostgreSQL pgvector (RAG)
```

#### OpenAI API Integration

The service uses the **OpenAI API** for two main purposes:

| Function | Model | Description |
|----------|-------|-------------|
| **Embedding** | `text-embedding-ada-002` | Convert text to vectors for pgvector storage |
| **Generation** | `gpt-4` / `gpt-3.5-turbo` | Generate educational content (exercises, roadmaps, summaries) |

```python
# Example OpenAI call for exercise generation
import openai

response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": "You are an educational assistant..."},
        {"role": "user", "content": f"Create 5 multiple-choice questions from: {content}"}
    ]
)
```

#### AWS S3 Integration

All uploaded files are pushed to the **AWS S3** bucket `Slothub-upload-2026`:

```python
import boto3

s3_client = boto3.client(
    's3',
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY'),
    aws_secret_access_key=os.getenv('AWS_SECRET_KEY'),
    region_name='ap-southeast-1'
)

# Upload file
s3_client.upload_fileobj(
    file_obj,
    'Slothub-upload-2026',
    f'classrooms/{classroom_id}/{filename}'
)
```

#### Direct Database Connection

Unlike the backend (which uses JPA/Hibernate), the AI service connects **directly** to PostgreSQL via `psycopg2`:

```python
import psycopg2

conn = psycopg2.connect(
    host=os.getenv('DB_HOST'),
    dbname=os.getenv('DB_NAME'),
    user=os.getenv('DB_USERNAME'),
    password=os.getenv('DB_PASSWORD')
)
```

{{% notice warning %}}
The AI service **automatically runs migrations** on startup — creating its own tables if they don't exist (e.g., tables for embedding vectors). This is an intentional design allowing the service to be deployed independently.
{{% /notice %}}

#### AI Service API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/generate-exercises` | POST | Generate exercises from uploaded documents |
| `/api/v1/roadmap` | POST | Create personalized study roadmap |
| `/api/v1/upload` | POST | Upload file to S3 |
| `/api/v1/chat/proxy` | POST | Forward chat messages to Slozy |
| `/api/v1/subjects` | GET | List of subjects |
| `/api/v1/books/{id}/content` | GET | Retrieve book/curriculum content |

#### Running the AI Service

```bash
# Navigate to the AI directory
cd AI/

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt

# Start the server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

{{% notice info %}}
The `--reload` flag enables hot-reload when source code changes during development. Remove this flag in production environments.
{{% /notice %}}

The next section explores the **Agent-Core (Slozy)** — the intelligence behind the AI tutor, powered by LangGraph ReAct Agent and AWS Bedrock AgentCore.
