# Team Collaboration Platform

A full-stack collaboration tool for teams to manage projects, tasks (Kanban), and real-time chat – complete with role-based access control.

---

## ✨ Features

• **Project management** – create, edit, delete projects within a team  
• **Kanban board** – drag & drop tasks across _To-do_, _In-Progress_, _Done_  
• **Role-based access** – Admin / Manager / Member permissions enforced on both API & UI  
• **Real-time chat** – Socket.IO powered team chat  
• **Live updates** – tasks and messages broadcast instantly  
• **Team overview** – list members & roles  
• **Dark mode** – Tailwind + Shadcn UI  

---

## ⚙️ Tech Stack

Backend
- Node.js + Express
- MongoDB Atlas (Mongoose ODM)
- Firebase Admin (JWT verification)
- Socket.IO (real-time)
- Joi (validation)

Frontend
- React 18 + TypeScript (Vite bundler)
- Tailwind CSS + Shadcn UI
- Socket.IO-client
- React Router 6
- @hello-pangea/dnd (Kanban)

Deployment
- **Backend**: Render _or_ Railway  
- **Frontend**: Vercel _or_ Netlify  
- **Database**: MongoDB Atlas

---

## 🗂️ Monorepo Structure
```
backend/          # Express API & WebSocket server
  src/
    models/
    routes/
    middleware/
    config/
    server.js
frontend/         # Vite + React client app
  src/
    components/
    pages/
  ...
```

---

## 🔑 Environment Variables

### Backend (`backend/.env`)
```env
PORT=5000
MONGO_URI=mongodb+srv://<user>:<pass>@cluster.mongodb.net/collab
FIREBASE_SERVICE_ACCOUNT={"type":"service_account", ...}
```

### Frontend (`frontend/.env`)
```env
VITE_API_URL=https://<your-backend-domain>/api
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
```

> Create both files by copying the provided `.env.example` or snippet above and filling in your values.

---

## 🚀 Local Development

Backend
```bash
cd backend
pnpm install          # or npm/yarn
pnpm dev              # nodemon hot-reload
```
Frontend
```bash
cd frontend
pnpm install
pnpm dev              # open http://localhost:5173
```

---

## ☁️ Deployment Guide

### 1. MongoDB Atlas
1. Create an Atlas cluster → Database Access → create user & password.  
2. Whitelist IP or set to `0.0.0.0/0`.  
3. Grab the connection string → set `MONGO_URI`.

### 2. Backend (Render example)
1. Push code to GitHub.
2. Create **Web Service** on Render → _Public Git repository_.
3. Build command: `pnpm install --filter backend --prod` (or `npm install` inside backend).  
   Start command: `node backend/src/server.js`  
4. Add env vars from [Backend env section](#backend-backend-env).
5. Expose port **$PORT** (Render auto handles).  
6. Save → first deploy builds & starts API at `https://<service>.onrender.com`.

### 3. Frontend (Vercel example)
1. Import repo on Vercel.
2. Framework = **Vite**.
3. Root directory: `frontend`.
4. Build command: `pnpm run build` (or `npm run build`).
5. Output directory: `dist`.
6. Environment variables from [Frontend env](#frontend-frontend-env) – make sure `VITE_API_URL` points to Render URL + `/api`.
7. Deploy → Vercel hosts at `https://your-app.vercel.app`.

### 4. Custom Domains
Point CNAME / A records per platform docs.

---

## 📜 API Summary

| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET    | /api/projects        | Authenticated | List team projects |
| POST   | /api/projects        | Admin/Manager | Create project |
| PUT    | /api/projects/:id    | Admin/Manager | Update project |
| DELETE | /api/projects/:id    | Admin         | Delete project |
| GET    | /api/tasks?projectId | Authenticated | List tasks in project |
| POST   | /api/tasks           | Admin/Manager | Create task |
| PUT    | /api/tasks/:id       | Admin/Manager | Update status/assignee |
| DELETE | /api/tasks/:id       | Admin/Manager | Delete task |
| POST   | /api/messages        | Authenticated | Send chat message |
| GET    | /api/messages        | Authenticated | Fetch chat history |
| GET    | /api/team/members    | Authenticated | List team members |

WebSocket events (`Socket.IO`): `taskCreated`, `taskUpdated`, `taskDeleted`, `newMessage`.

---

## 🧑‍💻 Contributing
PRs welcome!  
1. Fork & clone  
2. Create a feature branch  
3. Commit & push  
4. Open Pull Request

---

## 📄 License
MIT 