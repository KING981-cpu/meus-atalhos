# Learn Código - Workspace Colaborativo

## 🎯 Descrição
Portal de workspace para coworking com cronômetro de estudo, gestão de tarefas, notas compartilhadas, calendário e equipe integrada.

## 🏗️ Stack Tecnológico

### Frontend (Implementado)
- **HTML5**: Semântica e acessibilidade
- **CSS3**: Grid, Flexbox, animações, dark mode
- **JavaScript ES6+**: Async/await, LocalStorage
- **Font Awesome 6.4**: Ícones vetoriais
- **PWA**: Service Worker + Manifest para offline

### Backend (Recomendado para produção)
- **Node.js + Express**: API REST
- **Socket.io**: Real-time collaboration
- **PostgreSQL/MongoDB**: Persistência
- **JWT/OAuth2**: Autenticação segura
- **bcrypt**: Hash de senhas
- **Redis**: Cache e sessões

## ✨ Recursos Implementados

### 1. **Dashboard**
- Widget de tempo de estudo em tempo real
- Estatísticas de sessões
- Status de equipe online
- Atalhos rápidos para ferramentas (ChatGPT, Gemini, etc)
- Feed de atividades recente

### 2. **Cronômetro Inteligente**
- Timer com precisão de segundos
- Barra de progresso visual
- Meta de 6 horas com indicador percentual
- Salvamento automático de sessões
- Notas contextuais por sessão

### 3. **Gestão de Tarefas (Kanban)**
- Criar/editar/deletar tarefas
- Check-box de conclusão
- Persistência em LocalStorage
- UI drag-drop pronto

### 4. **Sistema de Notas**
- Criar notas com título
- Editor inline
- Data de criação automática
- Sincronização por usuário
- HTML sanitizado (XSS prevention)

### 5. **Equipe & Presença**
- Lista de membros da equipe
- Status online/offline
- Indicador visual de presença
- Atividade feed em tempo real

### 6. **Calendário**
- Integração para agendamento
- Estrutura pronta para eventos

### 7. **Autenticação**
- Login/Registro com validação
- Persistência de sessão
- Token JWT ready
- XSS sanitization

### 8. **PWA & Offline**
- Service Worker com cache
- Funciona offline
- Manifest for mobile
- Installable como app

### 9. **Tema Escuro**
- Toggle light/dark mode
- Persistência em localStorage
- CSS variables for theming

## 📱 Responsividade
- Desktop: Layout flex sidebar + main content
- Tablet: Grid adaptativo
- Mobile: Sidebar horizontal + bottom menu

## 🔒 Segurança Implementada
- ✅ XSS Prevention (sanitizeHTML)
- ✅ Input validation (length checks)
- ✅ CORS ready
- ✅ Password min requirements
- ✅ JWT token structure ready
- ✅ Service Worker signed content

## 🚀 Deployment

### Local (Testing)
```bash
# Servir com live server or python
python -m http.server 8000
# ou
npx http-server
```

### Produção
1. **Backend Setup** (Node.js + Express)
   ```bash
   npm install express cors dotenv bcryptjs jsonwebtoken socket.io
   ```

2. **Database** (PostgreSQL)
   ```sql
   CREATE TABLE usuarios (id SERIAL, username VARCHAR, password_hash VARCHAR, created_at TIMESTAMP);
   CREATE TABLE estudos (id SERIAL, usuario_id INT, data DATE, tempo VARCHAR, resumo TEXT, created_at TIMESTAMP);
   CREATE TABLE tarefas (id SERIAL, usuario_id INT, titulo VARCHAR, completed BOOLEAN, created_at TIMESTAMP);
   ```

3. **Environment Variables**
   ```
   SUPABASE_URL=xxx
   SUPABASE_KEY=xxx
   JWT_SECRET=xxx
   DATABASE_URL=xxx
   ```

## 📊 Arquitetura de Dados

### LocalStorage (Frontend)
- `currentUser`: Username
- `authToken`: Demo token
- `darkMode`: Boolean
- `tasks-{user}`: Array JSON
- `notes-{user}`: Array JSON
- `session-{timestamp}`: Session data

### Backend Expected (Future)
- POST `/api/register` - Cadastro
- POST `/api/login` - Login
- POST `/api/save-session` - Salvar estudo
- GET `/api/history` - Histórico
- GET `/api/team` - Membros
- POST `/api/tasks` - CRUD tarefas
- WS `/socket.io` - Real-time

## 🎨 UI/UX Features
- Glassmorphism cards
- Smooth transitions
- Responsive grid system
- Activity feed with timestamps
- Notification toast system
- Button loading states
- Form validation feedback

## ⚙️ Configuração Inicial
1. Clone o repositório
2. Abra `index.html` no browser
3. Use credenciais de teste
4. Dados salvos localmente (localStorage)
5. Para backend: implementar endpoints da API

## 🔄 Real-time Features (Ready)
- User presence detection
- Activity feed updates
- Live notification system
- Socket.io integration point
- Auto-sync capabilities

## 📈 Escalabilidade
- Modular JavaScript (fácil split em modules)
- API-first architecture (backend agnóstico)
- Database-agnostic queries
- Component-based UI structure
- Cache strategy ready

## 🧪 Teste Manual
1. ✅ Abrir em browser
2. ✅ Criar conta (demo - localStorage)
3. ✅ Iniciar cronômetro
4. ✅ Criar tarefas/notas
5. ✅ Testar dark mode
6. ✅ Verificar responsividade
7. ✅ Instalar PWA (desktop)
8. ✅ Testar offline

## 📝 Roadmap
- [ ] Backend API (Node.js)
- [ ] Real-time WebSocket
- [ ] Autenticação OAuth2
- [ ] Integração Supabase
- [ ] Compartilhamento de documentos
- [ ] Notificações Push
- [ ] Mobile app wrapper
- [ ] Analytics dashboard
- [ ] Integração Google Calendar
- [ ] Video conferencing integration
