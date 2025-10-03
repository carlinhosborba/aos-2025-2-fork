# ex01-express — API (Users, Messages e Tarefas)
Express + Sequelize + PostgreSQL (Neon) + Vercel

## 🔗 Links
- **GitHub (código):** https://github.com/carlinhosborba/aos-2025-2-fork
- **Vercel (produção):** https://aos-2025-2-fork-3xsvnqq1n-carlos-borbas-projects.vercel.app

## 🧰 Stack
- Node.js + Express
- Sequelize (ORM) + PostgreSQL (Neon)
- Vercel (Serverless Functions)
- Dotenv / CORS

## ▶️ Como rodar local
```bash
# entrar na pasta do projeto
cd ex01-express

# instalar deps
npm install

# criar .env com a URL do Neon (exemplo abaixo) e subir
npm run dev
# http://localhost:3000
```

### Variáveis de ambiente
Use **DATABASE_URL** (URL completa do Neon).  
Exemplo de `.env`:
```env
DATABASE_URL=postgres://usuario:senha@host/neondb?sslmode=require
PORT=3000
```

## 🌐 Endpoints (base: /api)
### Health
- `GET /api/health` → `{ status: "ok" }`

### Users
- `GET /api/users`
- `GET /api/users/:id`
- `POST /api/users` → `{ name, email }`
- `PUT /api/users/:id` → `{ name?, email? }`
- `DELETE /api/users/:id`

### Messages
- `GET /api/messages`
- `GET /api/messages/:id`
- `POST /api/messages` → `{ text, userId }`
- `PUT /api/messages/:id` → `{ text }`
- `DELETE /api/messages/:id`

### Tarefas (atividade nova)
- `GET /api/tarefas`
- `GET /api/tarefas/:objectId`
- `POST /api/tarefas` → `{ descricao }`  (campo `concluida` default: `false`)
- `PUT /api/tarefas/:objectId` → `{ descricao?, concluida? }`
- `DELETE /api/tarefas/:objectId`

## 🧪 Testes rápidos (curl)
```bash
BASE="https://aos-2025-2-fork-3xsvnqq1n-carlos-borbas-projects.vercel.app"

# health
curl -i $BASE/api/health

# criar usuário
curl -i -X POST $BASE/api/users   -H "Content-Type: application/json"   -d '{"name":"Carlos","email":"carlos@example.com"}'

# listar usuários
curl -i $BASE/api/users

# criar tarefa
curl -i -X POST $BASE/api/tarefas   -H "Content-Type: application/json"   -d '{"descricao":"Estudar Sequelize"}'
```

## 📦 Postman
Baixe a coleção pronta e importe no Postman/Desktop:
- [Download da coleção Postman](sandbox:/mnt/data/aos-2025-ex01.postman_collection.json)

A coleção usa a variável `base_url`, já apontando para o domínio da Vercel.

## 🚀 Deploy (Vercel)
- `vercel.json` mapeia as rotas `api/*.js` e expõe `/api/*`.
- **ENV (Preview/Production):** `DATABASE_URL`
- A homepage (`/`) pode responder “Cannot GET /” — o backend expõe apenas `/api/*`.

## ℹ️ Observações
- Se aparecer **500 FUNCTION_INVOCATION_FAILED** no Vercel, confira se `DATABASE_URL` está definida no ambiente correto (Preview/Production).
