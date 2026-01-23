# API Specification - Learn Código Backend

## Base URL
```
https://api.learncodigo.com/v1
```

## Authentication
All endpoints except `/auth/*` require JWT Bearer token in Authorization header:
```
Authorization: Bearer <jwt_token>
```

---

## Authentication Endpoints

### POST /auth/register
Register new user

**Request:**
```json
{
  "username": "student_001",
  "password": "SecurePass123!",
  "email": "user@example.com"
}
```

**Response (201):**
```json
{
  "token": "eyJhbGc...",
  "user": {
    "id": 1,
    "username": "student_001",
    "email": "user@example.com",
    "created_at": "2026-01-23T10:00:00Z"
  }
}
```

**Validation:**
- Username: 3-20 chars, alphanumeric + underscore
- Password: min 8 chars, uppercase, number, special char
- Email: valid email format

---

### POST /auth/login
Authenticate user

**Request:**
```json
{
  "username": "student_001",
  "password": "SecurePass123!"
}
```

**Response (200):**
```json
{
  "token": "eyJhbGc...",
  "expires_in": 86400,
  "user": {
    "id": 1,
    "username": "student_001",
    "status": "online"
  }
}
```

**Error (401):**
```json
{
  "error": "Invalid credentials",
  "code": "AUTH_INVALID"
}
```

---

### POST /auth/refresh
Refresh JWT token

**Response (200):**
```json
{
  "token": "eyJhbGc...",
  "expires_in": 86400
}
```

---

## Study Sessions Endpoints

### POST /sessions
Create study session

**Request:**
```json
{
  "tempo": "02:30:45",
  "resumo": "Matemática - Cálculo integral",
  "disciplina": "Matemática",
  "tags": ["cálculo", "integral"]
}
```

**Response (201):**
```json
{
  "id": 42,
  "usuario_id": 1,
  "data": "2026-01-23",
  "tempo": "02:30:45",
  "resumo": "Matemática - Cálculo integral",
  "created_at": "2026-01-23T10:15:30Z"
}
```

---

### GET /sessions
List user's study sessions

**Query Params:**
- `limit`: int (default: 10, max: 100)
- `offset`: int (default: 0)
- `from`: date (YYYY-MM-DD)
- `to`: date (YYYY-MM-DD)
- `disciplina`: string (filter by subject)

**Response (200):**
```json
{
  "sessions": [
    {
      "id": 42,
      "data": "2026-01-23",
      "tempo": "02:30:45",
      "resumo": "Matemática",
      "created_at": "2026-01-23T10:15:30Z"
    }
  ],
  "total": 156,
  "limit": 10,
  "offset": 0
}
```

---

### GET /sessions/:id
Get specific session

**Response (200):**
```json
{
  "id": 42,
  "usuario_id": 1,
  "data": "2026-01-23",
  "tempo": "02:30:45",
  "resumo": "Matemática - Cálculo integral",
  "tags": ["cálculo", "integral"],
  "notas_completas": "Lorem ipsum...",
  "created_at": "2026-01-23T10:15:30Z",
  "updated_at": "2026-01-23T10:15:30Z"
}
```

---

### DELETE /sessions/:id
Delete session

**Response (204):** No Content

---

## Tasks Endpoints

### POST /tasks
Create task

**Request:**
```json
{
  "titulo": "Revisar capítulo 5",
  "descricao": "Completar exercícios 1-10",
  "prioridade": "alta",
  "data_vencimento": "2026-01-30",
  "tags": ["revisão"]
}
```

**Response (201):**
```json
{
  "id": 1,
  "titulo": "Revisar capítulo 5",
  "descricao": "Completar exercícios 1-10",
  "prioridade": "alta",
  "concluida": false,
  "data_vencimento": "2026-01-30",
  "created_at": "2026-01-23T10:15:30Z"
}
```

---

### GET /tasks
List tasks

**Query Params:**
- `status`: all|pending|completed
- `prioridade`: baixa|media|alta
- `sort`: created_at|data_vencimento

**Response (200):**
```json
{
  "tasks": [
    {
      "id": 1,
      "titulo": "Revisar capítulo 5",
      "prioridade": "alta",
      "concluida": false,
      "data_vencimento": "2026-01-30"
    }
  ],
  "total": 24
}
```

---

### PATCH /tasks/:id
Update task

**Request:**
```json
{
  "concluida": true,
  "titulo": "Revisar capítulo 5 - FEITO"
}
```

**Response (200):** Updated task object

---

### DELETE /tasks/:id
Delete task

**Response (204):** No Content

---

## Notes Endpoints

### POST /notes
Create note

**Request:**
```json
{
  "titulo": "Anotações Cálculo",
  "conteudo": "Integral definida...",
  "tags": ["matemática", "cálculo"],
  "compartilhado": false
}
```

**Response (201):**
```json
{
  "id": 1,
  "titulo": "Anotações Cálculo",
  "conteudo": "Integral definida...",
  "tags": ["matemática", "cálculo"],
  "compartilhado": false,
  "criado_em": "2026-01-23T10:15:30Z"
}
```

---

### GET /notes
List notes

**Response (200):**
```json
{
  "notes": [
    {
      "id": 1,
      "titulo": "Anotações Cálculo",
      "conteudo_preview": "Integral definida...",
      "tags": ["matemática"],
      "criado_em": "2026-01-23T10:15:30Z"
    }
  ],
  "total": 42
}
```

---

### GET /notes/:id
Get note

**Response (200):** Full note object

---

### PATCH /notes/:id
Update note

**Response (200):** Updated note

---

### DELETE /notes/:id
Delete note

**Response (204):** No Content

---

## Team Endpoints

### GET /team
List team members

**Response (200):**
```json
{
  "members": [
    {
      "id": 1,
      "username": "user_001",
      "status": "online",
      "avatar": "https://...",
      "last_seen": "2026-01-23T10:15:30Z"
    }
  ],
  "total": 1,
  "online_count": 1
}
```

---

### POST /team/invite
Send team invitation

**Request:**
```json
{
  "email": "colleague@example.com",
  "role": "member"
}
```

**Response (201):**
```json
{
  "invitation_id": "inv_123",
  "sent_to": "colleague@example.com",
  "created_at": "2026-01-23T10:15:30Z"
}
```

---

### GET /team/status
Get real-time team status

**Response (200):**
```json
{
  "members_online": 3,
  "members_total": 5,
  "last_activity": "2026-01-23T10:15:30Z"
}
```

---

## Analytics Endpoints

### GET /analytics/summary
Get study analytics

**Query Params:**
- `period`: week|month|all
- `disciplina`: filter by subject

**Response (200):**
```json
{
  "total_horas": 125.5,
  "total_sessoes": 48,
  "sessoes_this_week": 8,
  "disciplinas": [
    {
      "nome": "Matemática",
      "horas": 45.5,
      "sessoes": 20
    }
  ],
  "meta_progresso": 65,
  "streak_dias": 12
}
```

---

### GET /analytics/chart
Get chart data

**Query Params:**
- `metric`: horas|sessoes|disciplinas
- `granularity`: daily|weekly|monthly
- `from`: date
- `to`: date

**Response (200):**
```json
{
  "labels": ["Jan 20", "Jan 21", "Jan 22", "Jan 23"],
  "datasets": [
    {
      "label": "Horas Estudadas",
      "data": [2.5, 3.0, 2.8, 1.5]
    }
  ]
}
```

---

## Calendar Endpoints

### GET /calendar/events
Get events

**Query Params:**
- `from`: date
- `to`: date

**Response (200):**
```json
{
  "events": [
    {
      "id": 1,
      "titulo": "Prova Matemática",
      "data": "2026-02-05",
      "hora": "14:00",
      "descricao": "Capítulos 1-5",
      "tipo": "prova"
    }
  ]
}
```

---

### POST /calendar/events
Create event

**Request:**
```json
{
  "titulo": "Prova Matemática",
  "data": "2026-02-05",
  "hora": "14:00",
  "tipo": "prova|estudo|prazo"
}
```

---

## Real-time WebSocket Events (Socket.io)

### Connected Events
- `user:join` - User comes online
- `user:leave` - User goes offline
- `session:started` - User starts study session
- `session:ended` - User finishes session
- `task:created` - New task added
- `note:shared` - Note shared with team

### Client Subscribe
```javascript
socket.on('team:activity', (data) => {
  // { user, action, timestamp }
});
```

---

## Error Responses

### 400 Bad Request
```json
{
  "error": "Invalid input",
  "code": "VALIDATION_ERROR",
  "details": {
    "username": "Must be 3-20 characters"
  }
}
```

### 401 Unauthorized
```json
{
  "error": "Invalid or expired token",
  "code": "AUTH_EXPIRED"
}
```

### 403 Forbidden
```json
{
  "error": "Insufficient permissions",
  "code": "FORBIDDEN"
}
```

### 404 Not Found
```json
{
  "error": "Resource not found",
  "code": "NOT_FOUND"
}
```

### 409 Conflict
```json
{
  "error": "Username already exists",
  "code": "DUPLICATE"
}
```

### 429 Too Many Requests
```json
{
  "error": "Rate limit exceeded",
  "code": "RATE_LIMITED",
  "retry_after": 60
}
```

### 500 Internal Server Error
```json
{
  "error": "Internal server error",
  "code": "SERVER_ERROR",
  "request_id": "req_123"
}
```

---

## Rate Limiting
- Authentication endpoints: 5 requests/minute per IP
- API endpoints: 100 requests/minute per user
- WebSocket: 50 messages/minute per user

---

## Pagination
Default limit: 10, max: 100
```
GET /resource?limit=25&offset=50
```

---

## Sorting
```
GET /resource?sort=created_at:desc
GET /resource?sort=titulo:asc
```

---

## Filtering
```
GET /sessions?from=2026-01-01&to=2026-01-31&disciplina=Matemática
```

---

## Changelog
- v1.0.0 - Initial API release (2026-01-23)
