---
title: "Backend Spring Boot"
date: 2026-04-03
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

#### Backend Overview

Slothub's backend is built on **Java 17 + Spring Boot 3.5**, serving as the central hub for educational business logic and the primary API layer that the frontend communicates with. The service runs on port `8080` and connects directly to the PostgreSQL database (`EDU_CARE`).

#### Core Domain Models

The system is designed around clearly hierarchical educational business entities:

##### User Management
```
User (Base)
├── Teacher
└── Student
```
- **User**: Root entity containing authentication info (email, hashed password, roles).
- **Teacher**: Extends User, can create classes, assign work, and manage timetables.
- **Student**: Extends User, joins classes, submits assignments, and accesses materials.

##### Classroom Management
| Entity | Role |
|--------|------|
| `Classroom` | Class information (name, code, homeroom teacher) |
| `ClassMember` | Student–class relationship |
| `Timetable` | Class schedule |
| `Attendance` | Daily attendance records |

##### Assignment Management
| Entity | Role |
|--------|------|
| `Assignment` | Assigned work (description, deadline, attachments) |
| `Submission` | Student submissions |
| `Question` | Individual questions |
| `QuestionBank` | Question bank organized by subject/topic |

##### Hierarchical Content System
```
Book
└── Chapter
    └── Section
        └── Subsection
            └── Lesson
```

This 5-tier hierarchical content system enables structured curriculum organization, serving as the foundation for the AI agent's accurate theory retrieval via RAG.

##### AI & Interaction Support
| Entity | Role |
|--------|------|
| `AIChatSession` | Chat sessions with Slozy AI tutor |
| `Roadmap` | AI-generated study roadmaps |

#### Authentication & Authorization

Slothub uses **JWT (JSON Web Token)** combined with **Spring OAuth2 Resource Server** for API security:

```
Authentication Flow:
1. Client sends POST /auth/login with email + password
2. Backend verifies credentials, generates JWT token
3. JWT is signed using JWT_SIGNER_KEY (HMAC-SHA256)
4. Client stores token in localStorage
5. Each API request includes header: Authorization: Bearer <token>
6. Spring Security intercepts and verifies JWT automatically
```

##### Key Security Features

- **Token Blacklist**: On logout, the token is added to a blacklist for immediate invalidation, preventing unauthorized use of unexpired tokens.
- **Email Password Reset**: The system sends password reset links via **Gmail SMTP** when users forget their passwords.
- **Session Expiration**: The frontend listens for `Slothub:session-expired` events (triggered by HTTP 401 responses) to automatically log out the user.

#### Backend Source Code Structure

```text
backend/src/main/java/
├── config/           # Spring Security, CORS, JWT filter configuration
├── controller/       # REST Controllers (Classroom, User, Assignment...)
├── dto/              # Data Transfer Objects (request/response)
├── entity/           # JPA Entities (mapped directly to PostgreSQL tables)
├── exception/        # Centralized exception handling (GlobalExceptionHandler)
├── mapper/           # MapStruct mappers (Entity ↔ DTO)
├── repository/       # Spring Data JPA Repositories
└── service/          # Business Logic Layer
```

#### Key API Endpoints

| Group | Endpoint | Method | Description |
|-------|----------|--------|-------------|
| Auth | `/auth/login` | POST | Login, receive JWT token |
| Auth | `/auth/logout` | POST | Logout, blacklist token |
| Auth | `/auth/reset-password` | POST | Send password reset email |
| User | `/api/users` | GET/POST | User CRUD operations |
| Classroom | `/api/classrooms` | GET/POST | Classroom management |
| Assignment | `/api/assignments` | GET/POST | Assignment creation and management |
| Submission | `/api/submissions` | GET/POST | Submission and grading |
| Timetable | `/api/timetables` | GET/POST | Schedule management |
| Attendance | `/api/attendance` | GET/POST | Attendance tracking |

#### Building & Running the Backend

```bash
# Navigate to the backend directory
cd backend/

# Install dependencies and build
./mvnw clean install -DskipTests

# Run the application
./mvnw spring-boot:run
```

{{% notice info %}}
The backend automatically creates the database schema (DDL) on first startup via the `spring.jpa.hibernate.ddl-auto` configuration in `application.yml`. Ensure the PostgreSQL container is running before starting Spring Boot.
{{% /notice %}}

The next section dives deep into the AI Service (FastAPI) — where automated educational content generation and cloud AI interactions take place.
