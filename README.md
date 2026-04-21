# My Chat App 💬

A real-time MERN chat application (frontend + backend) using Socket.io and MongoDB.

Features
- User authentication with JWT
- Real-time messaging with Socket.io
- Responsive UI with Tailwind CSS

---

## Tech Stack
- **Frontend:** React, Vite, Tailwind CSS, Zustand
- **Backend:** Node.js, Express, Socket.io
- **Database:** MongoDB Atlas
- **Containerization:** Docker (multi-stage)
- **CI/CD:** GitHub Actions (workflows in `.github/workflows`)

---

## Quick Start (local)

Prerequisites
- Node.js v18+
- Git

Clone & install
```bash
git clone https://github.com/SahilVijaySingh28/Mern-Chat-app.git
cd Mern-Chat-app
npm install
npm install --prefix frontend
```

Create `.env` (copy `.env.example` and fill values)
```env
# Example values — replace with your real ones
MONGO_DB_URI=mongodb+srv://<dbUser>:<dbPassword>@<cluster>.mongodb.net/<dbName>?retryWrites=true&w=majority
JWT_SECRET=<strong-random-string>
NODE_ENV=development
PORT=5000
```

Run in development
```bash
# Backend
npm run server

# Frontend (in another terminal)
cd frontend && npm run dev
```

Notes
- `backend/server.js` serves the built frontend from `frontend/dist` in production. Run `npm run build --prefix frontend` before `npm start` for production.

---

## Docker (local)

Build and run
```bash
docker build -t chat-app:dev .
docker run --env-file .env -p 5000:5000 --name chat-app chat-app:dev
```

Important
- Dockerfile now exposes port `5000` to match the server default.
- Make sure `.env` contains `MONGO_DB_URI` and `JWT_SECRET` (do not commit `.env`).

---

## Deploy to Render (PaaS)

Render is a simple way to deploy this app using your GitHub repo and the `Dockerfile` in the repo root.

Steps
1. Create a Render account and connect your GitHub repo.
2. New → Web Service → select repo and branch. Set Environment = `Docker`.
3. In the Render service → Environment, add these variables (secrets):
   - `MONGO_DB_URI` — your Atlas connection string
   - `JWT_SECRET` — secure random string
   - `NODE_ENV` — `production`
   - Leave `PORT` blank (Render injects `PORT` automatically)
4. (Optional) Create a Deploy Hook in Render (Settings → Deploy Hooks) and copy the URL.
5. Add the Deploy Hook URL as a GitHub secret named `RENDER_DEPLOY_HOOK` (if you want CD via Actions).

Render notes
- Render auto-injects `PORT` and your `server.js` reads `process.env.PORT` so no manual port setting is needed.

---

## CI / CD (GitHub Actions)

Included workflows
- `.github/workflows/ci.yml` — builds the frontend and runs linter on push/PR to `main`.
- `.github/workflows/docker-publish.yml` — builds and pushes the Docker image to GHCR and triggers Render via `RENDER_DEPLOY_HOOK` (if set).

Repository secrets to add
- `RENDER_DEPLOY_HOOK` — Render deploy hook URL (optional for CD)
- (Optional) `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN` if you prefer Docker Hub

---

## Environment variables (required)
- `MONGO_DB_URI` — MongoDB Atlas connection string
- `JWT_SECRET` — secure string used to sign JWT tokens
- `NODE_ENV` — `production` on Render

Generate a secure `JWT_SECRET` locally:
```bash
node -e "console.log(require('crypto').randomBytes(48).toString('hex'))"
```

MongoDB Atlas access
- If you see "Could not connect" errors, add your server IP to Atlas Network Access (or `0.0.0.0/0` for testing). For production on Render, consider VPC peering or Private Endpoints.

---

## Troubleshooting
- "Could not connect to any servers": check `MONGO_DB_URI`, Atlas DB user/password, and Atlas Network Access whitelist.
- "No open ports detected": ensure `EXPOSE 5000` is in `Dockerfile` and `server.js` listens on `process.env.PORT` or `5000`.
- View Docker logs locally: `docker logs -f <container>`.
- View Render logs in the Render dashboard for build/runtime errors.

---

## Project structure
```
.
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── socket/
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   └── App.jsx
│   └── package.json
├── .github/workflows/
├── Dockerfile
└── .env.example
```

---

## Contributing & License
- If you want to contribute, open a PR. Add tests and run linting before submitting.
- License: MIT

---

If you'd like, I can also add a `README-DEPLOY.md` with step-by-step screenshots for Render and Atlas, or a `render.yaml` for infra-as-code (without secrets). Tell me which you'd prefer.
