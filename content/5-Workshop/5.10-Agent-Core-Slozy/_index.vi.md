---
title: "Agent-Core & Slozy AI"
date: 2026-04-03
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

#### Tổng quan Agent-Core

**Agent-Core** là thành phần thông minh nhất trong hệ thống Slothub — nơi chứa **Trợ lý Slozy**, một gia sư AI hội thoại được xây dựng trên kiến trúc **LangGraph ReAct Agent** và triển khai trên **AWS Bedrock AgentCore**.

Thay vì trả lời dựa trên kiến thức chung của mô hình ngôn ngữ, Slozy **truy vấn trực tiếp** vào cơ sở dữ liệu giáo trình thông qua cơ chế **RAG (Retrieval-Augmented Generation)** sử dụng **pgvector** trên PostgreSQL, đảm bảo phản hồi chính xác và có nguồn gốc.

#### Kiến trúc LangGraph ReAct Agent

```
                    ┌───────────────────┐
                    │   Nhận câu hỏi    │
                    │   từ học sinh     │
                    └────────┬──────────┘
                             │
                    ┌────────▼──────────┐
                    │    Suy luận       │
                    │  (Reasoning)      │
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
                    │   Tổng hợp &      │
                    │   Trả lời         │
                    └───────────────────┘
```

**ReAct** (Reasoning + Acting) cho phép agent:
1. **Suy luận** (Reason): Phân tích câu hỏi, xác định công cụ phù hợp
2. **Hành động** (Act): Gọi công cụ (tool) để truy xuất dữ liệu
3. **Quan sát** (Observe): Đánh giá kết quả từ công cụ
4. **Lặp lại**: Tiếp tục suy luận nếu cần thêm thông tin
5. **Trả lời**: Tổng hợp câu trả lời cuối cùng

#### Ba Công cụ Tích hợp (Tools)

##### 1. `search_theory_database` — Tìm kiếm Lý thuyết (RAG)

Công cụ cốt lõi sử dụng **pgvector** để thực hiện tìm kiếm vector similarity:

```python
# Mô phỏng logic tìm kiếm
def search_theory_database(query: str) -> list:
    # 1. Chuyển câu hỏi thành vector embedding
    query_vector = openai.Embedding.create(
        input=query,
        model="text-embedding-ada-002"
    )
    
    # 2. Tìm kiếm similarity trên PostgreSQL pgvector
    results = db.execute("""
        SELECT content, title, similarity
        FROM theory_embeddings
        ORDER BY embedding <=> %s::vector
        LIMIT 5
    """, [query_vector])
    
    return results
```

{{% notice info %}}
`pgvector` là extension của PostgreSQL cho phép lưu trữ và truy vấn vector embeddings. Toán tử `<=>` tính khoảng cách cosine giữa hai vector, cho phép tìm nội dung lý thuyết tương tự nhất với câu hỏi của học sinh.
{{% /notice %}}

##### 2. `suggest_roadmap` — Gợi ý Lộ trình Học

Công cụ này gọi API nội bộ (FastAPI) để tạo lộ trình ôn tập phù hợp:

```python
def suggest_roadmap(subject: str, level: str) -> dict:
    # Gọi API FastAPI nội bộ
    response = requests.post(
        "http://localhost:8000/api/v1/roadmap",
        json={"subject": subject, "current_level": level}
    )
    return response.json()
```

##### 3. `suggest_quiz` — Gợi ý Bài Kiểm tra

Tương tự, công cụ này tạo bộ câu hỏi kiểm tra theo chủ đề:

```python
def suggest_quiz(topic: str, difficulty: str) -> dict:
    # Gọi API FastAPI để sinh quiz
    response = requests.post(
        "http://localhost:8000/api/v1/generate-exercises",
        json={"topic": topic, "difficulty": difficulty}
    )
    return response.json()
```

#### Giao thức Widget Protocol

Điểm đặc biệt của Slozy là khả năng trả về **UI widgets** mà frontend có thể render thành các thành phần tương tác:

```
Định dạng widget:
>>>[UI_WIDGET:TYPE|arg1|arg2|...]<<<

Ví dụ:
>>>[UI_WIDGET:ROADMAP|math_12|4_weeks]<<<
>>>[UI_WIDGET:QUIZ|derivatives|medium|5_questions]<<<
>>>[UI_WIDGET:THEORY|chapter_3_section_2]<<<
```

Khi frontend nhận được chuỗi chứa pattern widget này, nó sẽ tự động parse và render thành React component tương ứng (bảng lộ trình, form quiz tương tác, v.v.) thay vì hiển thị text thuần túy.

#### Local Dev vs Production

| Khía cạnh | Local (`LOCAL_DEV=1`) | Production |
|-----------|----------------------|------------|
| **Memory** | `MemorySaver` (RAM) | `AgentCoreMemorySaver` (AWS Bedrock) |
| **Lịch sử chat** | Mất khi restart | Bền vững |
| **LLM Provider** | OpenAI trực tiếp | AWS Bedrock models |
| **Chi phí** | Chỉ OpenAI API | AWS Bedrock + Fargate |

```python
# Lựa chọn checkpointer dựa trên môi trường
import os
from langgraph.checkpoint.memory import MemorySaver

if os.getenv("LOCAL_DEV") == "1":
    checkpointer = MemorySaver()  # RAM - mất dữ liệu khi restart
else:
    from bedrock_agent_core import AgentCoreMemorySaver
    checkpointer = AgentCoreMemorySaver()  # AWS Bedrock - bền vững
```

#### Cấu trúc Mã nguồn Agent-Core

```text
agent-core/
├── app.py              # Định nghĩa LangGraph graph & agent
├── tools/
│   ├── search_theory.py    # Tool tìm kiếm lý thuyết (pgvector RAG)
│   ├── suggest_roadmap.py  # Tool gợi ý lộ trình
│   └── suggest_quiz.py     # Tool gợi ý bài kiểm tra
├── prompts/
│   └── system_prompt.txt   # System prompt cho Slozy
├── requirements.txt    # LangGraph, LangChain, boto3, psycopg2...
└── .env                # Cấu hình môi trường
```

#### Luồng Hội thoại Ví dụ

```
Học sinh: "Em không hiểu phần đạo hàm, anh giải thích cho em được không?"

Slozy (suy luận): 
  → Cần tìm lý thuyết về "đạo hàm"
  → Gọi tool: search_theory_database("đạo hàm")
  
pgvector trả về:
  → Chapter 3: "Đạo hàm của hàm số"
  → Section 3.1: "Định nghĩa đạo hàm"
  → Section 3.2: "Quy tắc tính đạo hàm"

Slozy (trả lời):
  "Đạo hàm là tốc độ thay đổi tức thời của hàm số. 
   Theo giáo trình Chương 3, Mục 3.1:
   - Đạo hàm f'(x) = lim[h→0] (f(x+h) - f(x))/h
   - ...
   
   Em muốn anh gợi ý lộ trình ôn tập không?
   >>>[UI_WIDGET:ROADMAP|calculus|derivatives]<<<"
```

#### Khởi chạy Agent-Core

```bash
# Di chuyển tới thư mục agent-core
cd agent-core/

# Tạo virtual environment (Python 3.10)
python3.10 -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# Cài đặt dependencies
pip install -r requirements.txt

# Chạy agent
python app.py
```

{{% notice warning %}}
Agent-Core sử dụng **Python 3.10** (khác với AI Service dùng Python 3.12) do yêu cầu tương thích của thư viện AWS Bedrock AgentCore SDK. Hãy đảm bảo bạn sử dụng đúng phiên bản Python.
{{% /notice %}}

Phần tiếp theo sẽ tìm hiểu cách **Frontend React** tích hợp với tất cả các microservice phía sau.
