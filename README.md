# Bolt — Daily Motivation Web App

This repository contains a Vite + React frontend and a small TypeScript Express backend.

## Run locally

Prerequisites:

- Node.js 16+
- npm
- Supabase project and keys

Frontend (in one terminal):

```powershell
Set-Location -Path 'Bolt_ai_motivative_app\Bolt_ai_motivative_app'
npm install
npm run dev
# open http://localhost:5173/
```

Backend (in another terminal):

```powershell
Set-Location -Path 'Bolt_ai_motivative_app\Bolt_ai_motivative_app\backend'
npm install
# set server envs (or use .env)
$env:POSTGRES_CONNECTION_STRING='postgresql://username:password@host:5432/postgres'
$env:PORT='5000'
npm run dev
# API: http://localhost:5000/api/...
```

## Environment variables

- Client (in `.env` at project root):
  - `VITE_SUPABASE_URL` — Supabase project URL (https://<project>.supabase.co)
  - `VITE_SUPABASE_ANON_KEY` — Supabase anon/public key
  - `VITE_OPENAI_API_KEY` — (If used client-side) **Prefer** moving this to server-side for security
- Server (backend `.env` or environment):
  - `POSTGRES_CONNECTION_STRING` — Postgres connection string for Supabase

Do NOT commit your real `.env` — use `.env.example` as a template.

## Deploy frontend to Vercel

1. Login to https://vercel.com and connect your GitHub repository.
2. Vercel will detect the project as a Vite app. Use these settings if prompted:
   - Framework: `Vite` / `Other`
   - Build Command: `npm run build`
   - Output Directory: `dist`
3. Add the environment variables on Vercel (Settings → Environment Variables): `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`.
4. Deploy.

We included `vercel.json` to help Vercel build as a static site.

## Deploy backend (recommended separate service)

The backend is a TypeScript Express app and should be deployed to a Node hosting provider (Render, Railway, Heroku, Fly, etc.).

General steps:

1. Build the backend: `npm run build` (will emit JS to `dist/`).
2. Start with `npm run start:prod` (expects `dist/server.js`).
3. Configure `POSTGRES_CONNECTION_STRING` as a secret in the host.

Note: For production on serverless platforms you may prefer converting endpoints to serverless functions.

## What I added

- `README.md` — this file
- `vercel.json` — Vercel static-build config
- backend scripts to build/start for production

If you want, I can:

- Move OpenAI calls server-side and secure the key
- Add GitHub Actions to build and run tests on push
- Convert backend to serverless API routes for deployment with Vercel
