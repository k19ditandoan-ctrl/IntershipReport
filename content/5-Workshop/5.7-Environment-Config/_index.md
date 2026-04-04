---
title: "Environment Configuration"
date: 2026-04-03
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

#### Environment Variables Overview

Slothub's microservice architecture requires each service to be configured via separate `.env` files. Proper environment variable management is key to ensuring smooth inter-service communication and secure cloud integration.

{{% notice warning %}}
**Never** commit `.env` files to your Git repository. Ensure `.env` is listed in `.gitignore` to protect sensitive information such as API keys and database credentials.
{{% /notice %}}

#### 1. Frontend (`frontend/.env`)

The React frontend needs to know the addresses of both backend APIs:

```env
# Spring Boot Backend API URL
VITE_API_BASE_URL=http://localhost:8080/api

# FastAPI AI Service URL
VITE_FAST_API_BASE_URL=http://localhost:8000/api/v1
```

| Variable | Description | Default |
|----------|-------------|---------|
| `VITE_API_BASE_URL` | Main REST API endpoint (Spring Boot) | `http://localhost:8080/api` |
| `VITE_FAST_API_BASE_URL` | AI Service endpoint (FastAPI) | `http://localhost:8000/api/v1` |

{{% notice tip %}}
The `VITE_` prefix is mandatory for Vite to inject variables into the client-side JavaScript bundle. Variables without this prefix won't be accessible in the React source code.
{{% /notice %}}

#### 2. Backend (`backend/.env`)

The Spring Boot backend requires PostgreSQL connection, JWT configuration, and email settings:

```env
# Database Connection
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# JWT Authentication
JWT_SIGNER_KEY=your_256bit_secret_key_here

# AWS Credentials (for file uploads)
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Gmail SMTP (for password reset functionality)
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_app_password
```

| Variable | Description | Notes |
|----------|-------------|-------|
| `DB_HOST` | PostgreSQL host address | `localhost` when using Docker Compose |
| `DB_NAME` | Database name | Default is `EDU_CARE` |
| `DB_USERNAME` | Database user | Typically `postgres` |
| `DB_PASSWORD` | Database password | Set in `docker-compose.yml` |
| `JWT_SIGNER_KEY` | Secret key for signing JWT tokens | Use a random 256-bit string |
| `AWS_ACCESS_KEY` | AWS IAM Access Key | Requires S3 permissions |
| `AWS_SECRET_KEY` | AWS IAM Secret Key | Keep strictly confidential |
| `MAIL_USERNAME` | Gmail SMTP account | Used for sending password reset emails |
| `MAIL_PASSWORD` | Gmail App Password | Generate from Google Account → App Passwords |

#### 3. AI Service (`AI/.env`)

The FastAPI service requires direct DB access, OpenAI API, and AWS S3:

```env
# Database (direct connection via psycopg2)
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# AWS S3 Configuration
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_REGION=ap-southeast-1
AWS_BUCKET_NAME=Slothub-upload-2026

# OpenAI API
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

{{% notice info %}}
The AI service connects **directly** to PostgreSQL via the `psycopg2` library without an ORM. It automatically runs database migrations (creating tables if needed) on each startup.
{{% /notice %}}

#### 4. Agent-Core (`agent-core/.env`)

The Agent-Core (Slozy AI Tutor) needs AWS credentials and the local dev mode flag:

```env
# Database
DB_HOST=localhost
DB_NAME=EDU_CARE
DB_USERNAME=postgres
DB_PASSWORD=your_password

# AWS Credentials
AWS_ACCESS_KEY=AKIAxxxxxxxxxxxxxxxx
AWS_SECRET_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
AWS_REGION=ap-southeast-1
AWS_BUCKET_NAME=Slothub-upload-2026

# OpenAI (shared embedding model)
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

# Local Development Mode
LOCAL_DEV=1
```

| Variable | Description | Values |
|----------|-------------|--------|
| `LOCAL_DEV` | When set to `1`, agent uses `MemorySaver` (RAM) instead of `AgentCoreMemorySaver` (AWS Bedrock) | `1` for local, unset or `0` for production |

{{% notice warning %}}
When `LOCAL_DEV=1`, conversation history is **lost** on agent restart. In production, disable this flag to use `AgentCoreMemorySaver` for persistent storage via AWS Bedrock.
{{% /notice %}}

#### Configuration Checklist

After setting up `.env` files for all 4 services, verify with this checklist:

- [ ] `frontend/.env` — Both URL endpoints are pointing to correct ports
- [ ] `backend/.env` — DB connection works, JWT key is set
- [ ] `AI/.env` — OpenAI key is valid, S3 bucket exists
- [ ] `agent-core/.env` — `LOCAL_DEV=1` for testing, AWS credentials ready

Next, we will dive deep into the Spring Boot backend architecture and its core domain models.
