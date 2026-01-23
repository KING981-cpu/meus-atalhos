# Backend API Required

This frontend requires a backend API server to handle authentication and data persistence securely.

## Required Endpoints

### POST /api/register
- **Request:** `{ username: string, password: string }`
- **Response:** `{ message: string, token?: string }`
- **Action:** Hash password with bcrypt, store user, return auth token

### POST /api/login
- **Request:** `{ username: string, password: string }`
- **Response:** `{ message: string, token: string }`
- **Action:** Verify hashed password, return JWT token

### POST /api/save-session
- **Auth:** Bearer token required
- **Request:** `{ tempo: string, resumo: string }`
- **Response:** `{ message: string, id: number }`
- **Action:** Store study session for authenticated user

### GET /api/history
- **Auth:** Bearer token required
- **Response:** `[{ id, data, tempo, resumo }, ...]`
- **Action:** Return user's last 10 study sessions

### DELETE /api/history/:id
- **Auth:** Bearer token required
- **Response:** `{ message: string }`
- **Action:** Delete study session (verify ownership)

## Security Requirements
- Use bcrypt for password hashing (cost factor: 12)
- Implement JWT for session tokens (expiry: 24h)
- Validate input on server side
- Use HTTPS only
- Implement rate limiting on /login and /register
- Add CORS headers for frontend domain only
