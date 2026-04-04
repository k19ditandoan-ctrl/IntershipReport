---
title: "Agent-Core & Slozy AI"
date: 2026-04-03
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

#### Agent-Core Overview

**Agent-Core** is the most intelligent component of the Slothub ecosystem — home to **Slozy Assistant**, a conversational AI tutor built on the **LangGraph ReAct Agent** architecture and deployed on **AWS Bedrock AgentCore**.

Rather than answering based on the language model's general knowledge, Slozy **queries directly** into the curriculum database through **RAG (Retrieval-Augmented Generation)** using **pgvector** on PostgreSQL, ensuring accurate and sourced responses.

#### LangGraph ReAct Agent Architecture

```
                    ┌───────────────────┐
                    │  Receive student  │
                    │     question      │
                    └────────┬──────────┘
                             │
                    ┌────────▼──────────┐
                    │    Reasoning      │
                    │                   │
                    └────────┬──────────┘
                             │
                 ┌───────────┼───────────┐
                 │           │           │
        ┌────────▼──┐ ┌─────▼─────┐ ┌──▼─────────┐
        │search_    │ │suggest_   │ │suggest_    │
        │theory_    │ │roadmap    │ │quiz        │
        │database   │ │           │ │            │
        └────────┬──┘ └─────┬─────┘ └──┬─────────┘
                 │           │           │
                 └───────────┼───────────┘
                             │
                    ┌────────▼──────────┐
                    │   Synthesize &    │
                    │     Respond       │
                    └───────────────────┘
```

**ReAct** (Reasoning + Acting) enables the agent to:
1. **Reason**: Analyze the question, determine the appropriate tool
2. **Act**: Call the tool to retrieve data
3. **Observe**: Evaluate results from the tool
4. **Iterate**: Continue reasoning if more information is needed
5. **Respond**: Synthesize a final answer

#### Three Integrated Tools

##### 1. `search_theory_database` — Theory Search (RAG)

The core tool uses **pgvector** for vector similarity search:

```python
# Simplified search logic
def search_theory_database(query: str) -> list:
    # 1. Convert question to vector embedding
    query_vector = openai.Embedding.create(
        input=query,
        model="text-embedding-ada-002"
    )
    
    # 2. Similarity search on PostgreSQL pgvector
    results = db.execute("""
        SELECT content, title, similarity
        FROM theory_embeddings
        ORDER BY embedding <=> %s::vector
        LIMIT 5
    """, [query_vector])
    
    return results
```

{{% notice info %}}
`pgvector` is a PostgreSQL extension that enables vector embedding storage and querying. The `<=>` operator computes cosine distance between two vectors, finding the most similar theoretical content to the student's question.
{{% /notice %}}

##### 2. `suggest_roadmap` — Learning Roadmap Suggestions

This tool calls the internal FastAPI API to generate appropriate study roadmaps:

```python
def suggest_roadmap(subject: str, level: str) -> dict:
    # Call internal FastAPI API
    response = requests.post(
        "http://localhost:8000/api/v1/roadmap",
        json={"subject": subject, "current_level": level}
    )
    return response.json()
```

##### 3. `suggest_quiz` — Quiz Suggestions

Similarly, this tool generates quiz question sets by topic:

```python
def suggest_quiz(topic: str, difficulty: str) -> dict:
    # Call FastAPI to generate quiz
    response = requests.post(
        "http://localhost:8000/api/v1/generate-exercises",
        json={"topic": topic, "difficulty": difficulty}
    )
    return response.json()
```

#### Widget Protocol

A distinctive feature of Slozy is its ability to return **UI widgets** that the frontend can render as interactive components:

```
Widget format:
>>>[UI_WIDGET:TYPE|arg1|arg2|...]<<<

Examples:
>>>[UI_WIDGET:ROADMAP|math_12|4_weeks]<<<
>>>[UI_WIDGET:QUIZ|derivatives|medium|5_questions]<<<
>>>[UI_WIDGET:THEORY|chapter_3_section_2]<<<
```

When the frontend receives a string containing this widget pattern, it automatically parses and renders the corresponding React component (roadmap table, interactive quiz form, etc.) instead of displaying plain text.

#### Local Dev vs Production

| Aspect | Local (`LOCAL_DEV=1`) | Production |
|--------|----------------------|------------|
| **Memory** | `MemorySaver` (RAM) | `AgentCoreMemorySaver` (AWS Bedrock) |
| **Chat history** | Lost on restart | Persistent |
| **LLM Provider** | Direct OpenAI | AWS Bedrock models |
| **Cost** | OpenAI API only | AWS Bedrock + Fargate |

```python
# Checkpointer selection based on environment
import os
from langgraph.checkpoint.memory import MemorySaver

if os.getenv("LOCAL_DEV") == "1":
    checkpointer = MemorySaver()  # RAM - data lost on restart
else:
    from bedrock_agent_core import AgentCoreMemorySaver
    checkpointer = AgentCoreMemorySaver()  # AWS Bedrock - persistent
```

#### Agent-Core Source Structure

```text
agent-core/
├── app.py              # LangGraph graph & agent definition
├── tools/
│   ├── search_theory.py    # Theory search tool (pgvector RAG)
│   ├── suggest_roadmap.py  # Roadmap suggestion tool
│   └── suggest_quiz.py     # Quiz suggestion tool
├── prompts/
│   └── system_prompt.txt   # System prompt for Slozy
├── requirements.txt    # LangGraph, LangChain, boto3, psycopg2...
└── .env                # Environment configuration
```

#### Example Conversation Flow

```
Student: "I don't understand derivatives, can you explain?"

Slozy (reasoning): 
  → Need to find theory about "derivatives"
  → Calling tool: search_theory_database("derivatives")
  
pgvector returns:
  → Chapter 3: "Derivatives of Functions"
  → Section 3.1: "Definition of Derivatives"
  → Section 3.2: "Rules for Computing Derivatives"

Slozy (response):
  "A derivative is the instantaneous rate of change of a function.
   According to Chapter 3, Section 3.1 of your curriculum:
   - The derivative f'(x) = lim[h→0] (f(x+h) - f(x))/h
   - ...
   
   Would you like me to suggest a study roadmap?
   >>>[UI_WIDGET:ROADMAP|calculus|derivatives]<<<"
```

#### Running Agent-Core

```bash
# Navigate to agent-core directory
cd agent-core/

# Create virtual environment (Python 3.10)
python3.10 -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt

# Run the agent
python app.py
```

{{% notice warning %}}
Agent-Core uses **Python 3.10** (unlike the AI Service which uses Python 3.12) due to compatibility requirements of the AWS Bedrock AgentCore SDK. Ensure you are using the correct Python version.
{{% /notice %}}

The next section explains how the **React Frontend** integrates with all the backend microservices.
