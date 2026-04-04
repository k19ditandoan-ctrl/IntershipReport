---
title: "Frontend React"
date: 2026-04-03
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

#### Frontend Overview

Slothub's frontend is built with **React 18 + TypeScript + Vite + TailwindCSS**, providing a modern, responsive, and multilingual (Vietnamese/English) SPA (Single Page Application). The application runs on port `5173` in the development environment.

#### API Integration

The frontend communicates with two backend services through a centralized `api.ts` module:

```typescript
// api.ts - API client configuration
const BACKEND_URL = import.meta.env.VITE_API_BASE_URL;     // Spring Boot :8080
const AI_URL = import.meta.env.VITE_FAST_API_BASE_URL;     // FastAPI :8000

// Interceptor automatically attaches JWT token
axios.interceptors.request.use((config) => {
    const token = localStorage.getItem('access_token');
    if (token) {
        config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
});
```

| Environment Variable | Target Service | Default Port |
|---------------------|---------------|--------------|
| `VITE_API_BASE_URL` | Spring Boot Backend (main REST API) | `8080` |
| `VITE_FAST_API_BASE_URL` | FastAPI AI Service | `8000` |

#### Authentication Management (AuthContext)

The frontend uses **React Context API** to manage authentication state across the entire application:

```typescript
// AuthContext.tsx - Authentication state management
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

    // Auto-logout when session expires
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

##### Authentication Flow

```
1. User enters email + password at /login
2. Frontend sends POST /auth/login to Spring Boot
3. Receives JWT token from response
4. Stores token in localStorage
5. Updates AuthContext → isAuthenticated = true
6. Redirects to Dashboard
```

##### Session Expired Handling

When any API request returns **HTTP 401 (Unauthorized)**, the axios interceptor:

```typescript
// 401 interceptor handling
axios.interceptors.response.use(
    (response) => response,
    (error) => {
        if (error.response?.status === 401) {
            // Dispatch custom event for AuthContext to catch
            window.dispatchEvent(
                new CustomEvent('Slothub:session-expired')
            );
        }
        return Promise.reject(error);
    }
);
```

{{% notice info %}}
The `Slothub:session-expired` event mechanism decouples the 401 handling logic from specific components, allowing any component in the application to react to session expiration without prop drilling.
{{% /notice %}}

#### AI Agent Widget Rendering

The most distinctive frontend feature is the ability to **automatically render UI widgets** from Slozy AI responses:

```typescript
// WidgetRenderer.tsx - Parse and render AI widgets
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

// Render corresponding component
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

##### Example Rendered Widgets

| Widget Type | Display | Description |
|-------------|---------|-------------|
| `ROADMAP` | Weekly study plan table | Review timeline with checkboxes |
| `QUIZ` | Interactive quiz form | Questions + interactive answers |
| `THEORY` | Theory card | Content extracted from curriculum |

#### Main Pages

| Page | Route | Description |
|------|-------|-------------|
| Login | `/login` | Authentication form |
| Dashboard | `/dashboard` | Classroom overview, statistics |
| Classroom | `/classrooms/:id` | Class details, members |
| Assignments | `/assignments` | Assignment list, submission |
| Timetable | `/timetable` | Weekly schedule |
| Attendance | `/attendance` | Attendance tracking table |
| Materials | `/materials` | Book library, PDF upload |
| AI Chat | `/chat` | Conversational interface with Slozy |
| Roadmap | `/roadmap` | AI-generated study roadmaps |
| Settings | `/settings` | Account information |

#### Frontend Source Structure

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

#### UI Features

- **Responsive Design**: TailwindCSS breakpoints for mobile/tablet/desktop
- **Internationalization (i18n)**: Vietnamese and English support
- **Dark/Light Mode**: User-customizable interface themes
- **Real-time Chat**: Slozy chat interface displaying both text and widgets simultaneously
- **File Upload**: Drag & drop PDF for AI exercise generation

#### Running the Frontend

```bash
# Navigate to frontend directory
cd frontend/

# Install dependencies
npm install

# Start development server
npm run dev
```

Visit `http://localhost:5173` to start using the interface. Ensure the Backend (`:8080`) and AI Service (`:8000`) are running first for full functionality.

{{% notice tip %}}
Use **React Developer Tools** (Chrome/Firefox extension) to debug the component tree and state management during development.
{{% /notice %}}

The next section guides you through the **AWS Cloud deployment** process using Fargate, ECR, ALB, and other managed services.
