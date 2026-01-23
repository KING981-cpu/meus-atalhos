# 🧪 Testing Checklist - Learn Código

## Manual Testing Steps

### ✅ Authentication Flow
- [ ] Abrir `index.html` em browser
- [ ] Clicar em "Criar conta"
- [ ] Preencher usuário (min 3 char) e senha (min 6 char)
- [ ] Verificar validação de campos vazios
- [ ] Verificar mensagens de erro inline
- [ ] Fazer login com credenciais
- [ ] Verificar persistência de usuário no topo

### ✅ Dashboard Features
- [ ] Verificar exibição de nome do usuário
- [ ] Status online/offline ativo
- [ ] Cards de estatísticas visíveis
- [ ] Atalhos rápidos carregam (ChatGPT, Gemini, etc)
- [ ] Activity feed atualiza
- [ ] Notificações toast aparecem

### ✅ Timer/Cronômetro
- [ ] Clicar "Iniciar" - timer começa
- [ ] Timer incrementa corretamente (segundos, minutos, horas)
- [ ] Barra de progresso preenche (6h = 100%)
- [ ] Percentual atualiza em tempo real
- [ ] Pausar para o timer
- [ ] Notas salvam com sessão
- [ ] Badge de tempo atualiza

### ✅ Tarefas (Kanban)
- [ ] Clicar "+" para nova tarefa
- [ ] Prompt solicita título
- [ ] Tarefa aparece na lista
- [ ] Checkbox marca como concluído
- [ ] Tarefa concluída fica com strikethrough
- [ ] Botão delete remove tarefa
- [ ] Tarefas persistem após reload

### ✅ Notas
- [ ] Clicar "+" para nova nota
- [ ] Título obrigatório
- [ ] Data criação automática
- [ ] Botão edit abre conteúdo
- [ ] Conteúdo salva corretamente
- [ ] Delete remove nota
- [ ] Notas persistem por usuário

### ✅ Histórico/Cloud
- [ ] Salvar sessão com timer > 0
- [ ] Mensagem "Erro" se timer = 0
- [ ] Sessão aparece no histórico
- [ ] Data formatada corretamente
- [ ] Tempo exibido corretamente
- [ ] Nota/resumo salvo
- [ ] Contador de sessões atualiza

### ✅ Navegação
- [ ] Sidebar buttons mudam de tab
- [ ] Tab ativo destaca em azul
- [ ] Conteúdo da tab carrega
- [ ] Transições suaves
- [ ] Botão nav ativo indica página

### ✅ Tema Escuro
- [ ] Clicar "Tema" alterna dark mode
- [ ] Cores ajustam corretamente
- [ ] Persistência em localStorage
- [ ] Reload mantém tema

### ✅ Responsividade
- [ ] Desktop: sidebar lateral
- [ ] Tablet (768px): grid 2 colunas
- [ ] Mobile: stack vertical
- [ ] Toques funcionam em mobile
- [ ] FAB bottom button mobile

### ✅ Logout
- [ ] Clicar "Sair" abre confirmação
- [ ] Confirmar volta ao login
- [ ] Timer resetado
- [ ] Session limpa
- [ ] Campos de input vazios

### ✅ Validações
- [ ] Username < 3 char: erro
- [ ] Username > 20 char: erro
- [ ] Senha < 6 char: erro
- [ ] Campo vazio: erro
- [ ] Nota > 500 char: erro
- [ ] Mensagens de erro em vermelho

### ✅ PWA Features
- [ ] Abrir DevTools > Application
- [ ] Verificar manifest.json carregado
- [ ] Service Worker registrado
- [ ] Cache populado
- [ ] Funciona offline (desconectar rede)
- [ ] Installable em desktop

### ✅ XSS Protection
- [ ] Tentar injetar: `<img src=x onerror=alert('xss')>` em nota
- [ ] Verificar que renderiza como texto
- [ ] HTML tags não executam

### ✅ Performance
- [ ] Carregar rápido < 2s
- [ ] Timer não causa lag
- [ ] Transições suaves (60fps)
- [ ] Sem console errors

### ✅ Acessibilidade
- [ ] Tab navigation funciona
- [ ] Botões focáveis
- [ ] Cores com contraste suficiente
- [ ] Icons têm labels
- [ ] Inputs têm placeholders

## Browser Testing Matrix

| Browser | Desktop | Tablet | Mobile |
|---------|---------|--------|--------|
| Chrome  | ✅      | ✅     | ✅     |
| Firefox | ✅      | ✅     | ✅     |
| Safari  | ✅      | ✅     | ✅     |
| Edge    | ✅      | ✅     | ✅     |

## Performance Metrics
- [ ] First Paint: < 1s
- [ ] Time to Interactive: < 2s
- [ ] Lighthouse score: > 90
- [ ] LocalStorage usage: < 5MB

## Security Tests
- [ ] Sem credenciais hardcoded
- [ ] LocalStorage não expõe senhas
- [ ] CORS headers prontos
- [ ] XSS sanitization ativo
- [ ] Input validation no cliente
- [ ] Backend validation needed

## Bug Tracking
- [ ] Sem console errors
- [ ] Sem console warnings
- [ ] Reload mantém estado
- [ ] Multiple tabs sincronizam?
- [ ] LocalStorage conflicts?

## Edge Cases
- [ ] Usuário muito longo?
- [ ] Caracteres especiais em nota?
- [ ] Rápidos cliques em botões?
- [ ] Rapid timer start/pause?
- [ ] Multiple windows abertos?
- [ ] Long session (24+ horas)?
