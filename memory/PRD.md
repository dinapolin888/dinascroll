# Scrolic - Social Trading Platform Indonesia

## Original Problem Statement
Import seluruh file dari `duitscroll-main.zip` tanpa edit apapun karena sudah sesuai dengan tech stack Emergent (React, FastAPI, MongoDB). Pastikan tidak ada tampilan yang berubah dan alur bisnis harus 100% sama.

## Import Summary (2026-02-29)
- Extracted `duitscroll-main.zip` and copied `backend/`, `frontend/`, `memory/`, `tests/`, `test_reports/`, and root docs into `/app/`
- Preserved existing protected env files (`/app/backend/.env`, `/app/frontend/.env`) — no edits to app code
- Backend: FastAPI + Socket.IO (single-runtime `server.py`), MongoDB, cTrader Open API, Mayar.id payment gateway, Gemini LLM bridge via emergentintegrations
- Frontend: Vite + React 19 + Tailwind 4, `yarn start` runs `vite --host 0.0.0.0 --port 3000` (already matches supervisor)
- Installed Python deps from `requirements.txt` + `emergentintegrations`
- Installed Node deps via `yarn install`
- Supervisor restarted → both services RUNNING and responding (frontend 200, backend 200 on `/api/*`)

## Architecture
- `/app/backend/server.py` — single-runtime FastAPI app with all routes prefixed `/api`
- `/app/backend/services/email_service.py` — SMTP notification helper
- `/app/backend/{database,auth_service,ticker,ctrader_client,ctrader_oauth,ctrader_config,event_contract,db_seed}.py`
- `/app/frontend/src/{App.tsx, main.tsx, views/, components/, services/, data/, utils/}`
- MongoDB via `MONGO_URL` / `DB_NAME` from `/app/backend/.env`
- Frontend calls backend via `REACT_APP_BACKEND_URL` from `/app/frontend/.env`

## Optional Env Vars (not required for boot, features gated when absent)
- `EMERGENT_LLM_KEY`, `GEMINI_MODEL` — LLM bridge
- `MAYAR_API_KEY`, `MAYAR_WEBHOOK_SECRET`, `MAYAR_BASE_URL` — Mayar.id payments
- `CTRADER_CLIENT_ID`, `CTRADER_CLIENT_SECRET`, `CTRADER_ENV`, `CTRADER_PROXY_URL` — cTrader Open API
- `PUBLIC_BASE_URL` / `SITE_URL` — canonical redirect URI base

## Status
- Frontend loads at preview URL, shows Scrolic feed UI (Untuk Anda / Mengikuti tabs, DNA strategy filter, bottom nav Feed/Explore/Dashboard/News/Profil)
- Backend `/api/feed`, `/api/user/me`, `/api/notifications`, `/api/config/energy-packages` returning 200 OK
- No UI or business logic edited — 100% identical to source zip
