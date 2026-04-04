---
title: "Frontend React"
date: 2026-04-03
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

#### Tổng quan Frontend

Frontend của Slothub được xây dựng bằng **React 18 + TypeScript + Vite + TailwindCSS**, cung cấp giao diện người dùng SPA (Single Page Application) hiện đại, responsive và đa ngôn ngữ (Việt/Anh). Ứng dụng chạy trên cổng `5173` trong môi trường phát triển.

#### Tích hợp API

Frontend giao tiếp với hai backend service thông qua module `api.ts` trung tâm:

```typescript
// api.ts - Cấu hình API client
const BACKEND_URL = import.meta.env.VITE_API_BASE_URL;     // Spring Boot :8080
const AI_URL = import.meta.env.VITE_FAST_API_BASE_URL;     // FastAPI :8000

// Interceptor tự động gắn JWT token
axios.interceptors.request.use((config) => {
    const token = localStorage.getItem('access_token');
    if (token) {
        config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
});
```

| Biến môi trường | Service đích | Cổng mặc định |
|-----------------|-------------|----------------|
| `VITE_API_BASE_URL` | Spring Boot Backend (REST API chính) | `8080` |
| `VITE_FAST_API_BASE_URL` | FastAPI AI Service | `8000` |

#### Quản lý Xác thực (AuthContext)

Frontend sử dụng **React Context API** để quản lý trạng thái xác thực xuyên suốt ứng dụng:

```typescript
// AuthContext.tsx - Quản lý trạng thái xác thực
interface AuthState {
    user: User | null;
    token: string | null;
    isAuthenticated: boolean;
}

const AuthContext = createContext<AuthContextType>(defaultValue);

export function AuthProvider({ children }: Props) {
    const [auth, setAuth] = useState<AuthState>({
        user: null,
        token: localStorage.getItem('access_token'),
        isAuthenticated: false,
    });

    // Tự động đăng xuất khi session hết hạn
    useEffect(() => {
        const handleExpired = () => {
            logout();
            navigate('/login');
        };
        
        window.addEventListener('Slothub:session-expired', handleExpired);
        return () => window.removeEventListener('Slothub:session-expired', handleExpired);
    }, []);
    
    // ...
}
```

##### Luồng Xác thực

```
1. Người dùng nhập email + password tại /login
2. Frontend gửi POST /auth/login tới Spring Boot
3. Nhận JWT token từ response
4. Lưu token vào localStorage
5. Cập nhật AuthContext → isAuthenticated = true
6. Redirect tới Dashboard
```

##### Xử lý Session Expired

Khi bất kỳ API request nào trả về **HTTP 401 (Unauthorized)**, axios interceptor sẽ:

```typescript
// Interceptor xử lý 401
axios.interceptors.response.use(
    (response) => response,
    (error) => {
        if (error.response?.status === 401) {
            // Phát sự kiện custom để AuthContext bắt
            window.dispatchEvent(
                new CustomEvent('Slothub:session-expired')
            );
        }
        return Promise.reject(error);
    }
);
```

{{% notice info %}}
Cơ chế sự kiện `Slothub:session-expired` tách biệt logic xử lý 401 khỏi các component cụ thể, cho phép bất kỳ component nào trong ứng dụng đều có thể phản ứng với session expired mà không cần prop drilling.
{{% /notice %}}

#### Render Widget từ AI Agent

Tính năng đặc biệt nhất của frontend Slothub là khả năng **tự động render UI widgets** từ phản hồi của Slozy AI:

```typescript
// WidgetRenderer.tsx - Parse và render AI widgets
function parseWidgets(text: string): (string | Widget)[] {
    const WIDGET_REGEX = />>>\[UI_WIDGET:(\w+)\|([^\]]*)\]<<</g;
    const parts: (string | Widget)[] = [];
    
    let match;
    while ((match = WIDGET_REGEX.exec(text)) !== null) {
        const type = match[1];   // ROADMAP, QUIZ, THEORY...
        const args = match[2].split('|');
        parts.push({ type, args });
    }
    
    return parts;
}

// Render component tương ứng
function WidgetRenderer({ widget }: { widget: Widget }) {
    switch (widget.type) {
        case 'ROADMAP':
            return <RoadmapWidget subject={widget.args[0]} />;
        case 'QUIZ':
            return <QuizWidget topic={widget.args[0]} difficulty={widget.args[1]} />;
        case 'THEORY':
            return <TheoryCard reference={widget.args[0]} />;
        default:
            return <span>{widget.raw}</span>;
    }
}
```

##### Ví dụ Widget được Render

| Widget Type | Hiển thị | Mô tả |
|-------------|----------|--------|
| `ROADMAP` | Bảng lộ trình theo tuần | Timeline ôn tập với checkbox |
| `QUIZ` | Form trắc nghiệm | Câu hỏi + đáp án tương tác |
| `THEORY` | Card lý thuyết | Nội dung trích từ giáo trình |

#### Các Trang chính (Pages)

| Trang | Route | Mô tả |
|-------|-------|--------|
| Đăng nhập | `/login` | Form xác thực  |
| Dashboard | `/dashboard` | Tổng quan lớp học, thống kê |
| Lớp học | `/classrooms/:id` | Chi tiết lớp, thành viên |
| Bài tập | `/assignments` | Danh sách bài giao/nộp |
| Thời khóa biểu | `/timetable` | Lịch học theo tuần |
| Điểm danh | `/attendance` | Bảng điểm danh |
| Tài liệu | `/materials` | Thư viện sách, upload PDF |
| Chat AI | `/chat` | Giao diện hội thoại với Slozy |
| Lộ trình | `/roadmap` | Lộ trình ôn tập AI-generated |
| Cài đặt | `/settings` | Thông tin tài khoản |

#### Cấu trúc Mã nguồn Frontend

```text
frontend/src/
├── api/
│   └── api.ts               # Axios instance & interceptors
├── components/
│   ├── layout/               # Header, Sidebar, Footer
│   ├── classroom/            # Classroom-related components
│   ├── assignment/           # Assignment forms & lists
│   ├── chat/                 # Chat UI & widget renderer
│   └── common/               # Buttons, Inputs, Modals
├── contexts/
│   └── AuthContext.tsx        # Authentication state management
├── pages/
│   ├── LoginPage.tsx
│   ├── DashboardPage.tsx
│   ├── ClassroomPage.tsx
│   └── ChatPage.tsx
├── hooks/                    # Custom React hooks
├── types/                    # TypeScript interfaces
├── App.tsx                   # Route definitions
└── main.tsx                  # Entry point
```

#### Tính năng Giao diện

- **Responsive Design**: Sử dụng TailwindCSS breakpoints cho mobile/tablet/desktop
- **Đa ngôn ngữ (i18n)**: Hỗ trợ Tiếng Việt và Tiếng Anh
- **Dark/Light Mode**: Tùy chỉnh giao diện theo sở thích người dùng
- **Real-time Chat**: Giao diện chat với Slozy hiển thị đồng thời text và widgets
- **File Upload**: Drag & drop PDF cho tính năng sinh bài tập AI

#### Khởi chạy Frontend

```bash
# Di chuyển tới thư mục frontend
cd frontend/

# Cài đặt dependencies
npm install

# Khởi chạy development server
npm run dev
```

Truy cập `http://localhost:5173` để bắt đầu sử dụng giao diện. Đảm bảo rằng Backend (`:8080`) và AI Service (`:8000`) đã chạy trước để các tính năng hoạt động đầy đủ.

{{% notice tip %}}
Sử dụng **React Developer Tools** (extension Chrome/Firefox) để debug component tree và state management trong quá trình phát triển.
{{% /notice %}}

Phần tiếp theo sẽ hướng dẫn quy trình triển khai lên **AWS Cloud** sử dụng Fargate, ECR, ALB và các dịch vụ managed.
