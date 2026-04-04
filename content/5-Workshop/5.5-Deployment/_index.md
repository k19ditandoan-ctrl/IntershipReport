---
title: "Development & Deployment"
date: 2026-04-03
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Running the Microservices Locally

Slothub relies on 4 distributed processes. In a real-world scenario, you would deploy these using container clusters such as AWS ECS (Fargate). For this workshop, we will start them sequentially on your local machine using the created `.env` files. Ensure you have the `.env` settings mentioned in the `report.md`.

##### 1. Start the Backend API (Spring Boot)
The backend manages application logic and connects to the PostgreSQL database.

* Open a terminal inside the `backend/` folder.
* Add your `DB_HOST`, `JWT_SIGNER_KEY`, email configurations, and AWS credentials to `backend/.env`.
* Execute the application:
  ```bash
  # Using Maven wrapper
  ./mvnw spring-boot:run
  ```
The Spring Boot portal will be live on `http://localhost:8080`.

##### 2. Start the AI Content Service (FastAPI)
The AI service manages AWS S3 and OpenAI API prompts.

* Open a terminal inside the `AI/` folder.
* Verify `OPENAI_API_KEY` and AWS configs are loaded in `AI/.env`.
* Create a virtual environment and start the Uvicorn server:
  ```bash
  uvicorn main:app --host 0.0.0.0 --port 8000
  ```
This service handles generative requests on `http://localhost:8000/api/v1`.

##### 3. Start the LangGraph Agent-Core (Slozy)
For tutoring interactions and theory lookup via RAG.

* Open a terminal in the `agent-core/` folder.
* Set `LOCAL_DEV=1` for testing the memory locally rather than forcing an AWS Bedrock invocation.
* Start the agent service. (Make sure you followed Python module requirements like `pip install -r requirements.txt`).

##### 4. Start the Frontend (React Vite)
The unified user portal.

* Navigate to the `frontend/` folder.
* Set `VITE_API_BASE_URL` to the Spring backend URL and `VITE_FAST_API_BASE_URL` to the Python API in `frontend/.env`.
* Install packages and start the UI:
  ```bash
  npm install
  npm run dev
  ```

Visit `http://localhost:5173` locally. Log in, request materials from uploaded PDFs, and interact with the AI chat system to verify that the microservices are integrated perfectly!
