---
title: "Cleanup"
date: 2026-04-03
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Project Cleanup and Teardown

If you deployed the application locally and simply want to free up device resources or reset the database cleanly, follow these cleanup steps:

##### 1. Clean Local App Instances
Navigate to the terminals where you ran React, Spring Boot, FastAPI, and Agent-Core independently and press `Ctrl+C` to terminate the isolated instances.

##### 2. Teardown Docker Compose Database
Move to the directory where your `docker-compose.yml` is located.
To simply stop the containers (preserving data inside named volumes):
```bash
docker-compose stop
```
If you wish to wipe the PostgreSQL database entirely (including user accounts and RAG vectors):
```bash
docker-compose down -v
```

##### 3. Cloud Storage (AWS S3)
To ensure no extra charges arise from forgotten files:
1. Log into your **AWS Management Console**.
2. Go to the **S3** Dashboard and click on your bucket (e.g., `Slothub-upload-2026`).
3. Click "Empty bucket" to delete all stored PDFs and images.
4. (Optional) Select the bucket and click "Delete" to permanently terminate the storage container.

##### 4. AWS Bedrock Agent (If Deployed)
If you disabled `LOCAL_DEV=1` and pushed the Agent setup directly to **AWS Bedrock AgentCore**:
1. Open the Bedrock console.
2. Select your provisioned agent alias.
3. Delete the alias and subsequently delete the deployed agent to prevent recurring costs mapped to your free tier.

By adhering to these cleanup routines after a workshop, you safeguard against unforeseen expenses from unused, persistent resources in AWS.
