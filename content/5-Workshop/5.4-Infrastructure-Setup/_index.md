---
title: "Infrastructure Setup"
date: 2026-04-03
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Local Database Setup

Because the project services communicate interchangeably with a single PostgreSQL database (with vector support for AI searches), we bundle it into a local container for quick deployment rather than managing a complex cloud database during development.

1. Navigate to the root directory where `docker-compose.yml` resides.
2. Ensure Docker Desktop is running.
3. Open your terminal and run:

    ```bash
    docker-compose up -d
    ```

4. Confirm that both PostgreSQL (`:5432`) and pgAdmin (`:5050`) containers are running.
5. You can visit `http://localhost:5050` (Using `admin@Slothub.com` / `admin`) to visualize your tables once the backend initializes them.

#### Cloud Storage Setup (AWS S3)

To handle document uploads (like PDF files) used for generating quizzes and roadmaps, we need an AWS S3 bucket.

1. Log into your **AWS Management Console**.
2. Search and open the **S3** service.
3. Click "Create bucket".
4. Enter a globally unique bucket name (e.g., `Slothub-upload-2026`).
5. Choose a region (e.g., `ap-southeast-1`).
6. Uncheck "Block all public access" if you intend to serve these files directly to the web application, and acknowledge the warning. Alternatively, keep it blocked and rely on Signed URLs.
7. Click "Create bucket".
8. Ensure you obtain the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` for an IAM user who has `AmazonS3FullAccess`. Save these securely.

#### Configuration Check

By setting up both the PostgreSQL connection and securing the AWS S3 credentials, the basic infrastructure requirements for Slothub have been established. Proceed to the next section to start and test the individual microservices.
