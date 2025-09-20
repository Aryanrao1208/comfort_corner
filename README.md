# Empath‑DS — Peer Mental‑Health Support (Repo Skeleton)

> **Short description**

Empath‑DS is a student project that implements a 7cups‑like peer emotional support platform with a frontend, Python backend, and AI chat integration. This repo contains the project skeleton, README, and a permissive MIT license so you can start coding quickly.

---

## MVP (what we'll build first)

1. Landing page with short quiz → personalized home/dashboard
2. Login / Signup (email + password, optional anonymous guest)
3. Dashboard: feed of user posts
4. One‑to‑one chat with a **verified** listener (text) — messages persisted
5. Pages: Path (progress updates), Community (posts), Become a Listener (onboarding)
6. Admin/reporting basics

---

## Tech stack (recommended)

* **Frontend:** Next.js (React) + Tailwind CSS
* **Backend:** FastAPI (Python) + Uvicorn
* **DB:** PostgreSQL
* **Realtime / Presence:** Redis (pub/sub) + WebSockets (FastAPI)
* **ORM / Migrations:** SQLAlchemy + Alembic (or Tortoise + Aerich if you prefer async ORM)
* **AI integration:** separate FastAPI endpoint that calls an LLM (OpenAI / local model) for assisted chat features
* **Dev / Deployment:** Docker + docker‑compose, GitHub Actions for CI

---

## Repo structure (suggested)

```
/empath-ds
├─ backend/                # FastAPI app
│  ├─ app/
│  │  ├─ main.py
│  │  ├─ api/
│  │  ├─ models/
│  │  ├─ core/
│  │  ├─ services/
│  │  └─ tests/
│  ├─ requirements.txt
│  └─ Dockerfile
├─ frontend/               # Next.js app
│  ├─ app/ (or pages/)
│  ├─ components/
│  ├─ styles/
│  └─ package.json
├─ infra/
│  └─ docker-compose.yml
├─ README.md
└─ LICENSE
```

---

## Quickstart (local development)

### Prerequisites

* Node.js & npm
* Python 3.10+
* Docker & docker‑compose (optional but recommended)
* PostgreSQL (local or docker)

### Local (minimum):

1. Clone the repo:

```bash
git clone git@github.com:<your-username>/empath-ds.git
cd empath-ds
```

2. Backend: create virtualenv & install

```bash
python -m venv .venv
source .venv/bin/activate    # or .venv\Scripts\activate on Windows
pip install -r backend/requirements.txt
cp backend/.env.example backend/.env
# set environment variables
```

3. Frontend: install

```bash
cd frontend
npm install
cp .env.local.example .env.local
```

4. Run backend (development)

```bash
cd backend
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

5. Run frontend

```bash
cd frontend
npm run dev
# opens at http://localhost:3000
```

### Docker (recommended):

A docker‑compose file will run backend, frontend (optional), Postgres and Redis. See `/infra/docker-compose.yml`.

---

## Environment variables (examples)

**backend/.env.example**

```
DATABASE_URL=postgresql://postgres:password@db:5432/empath
SECRET_KEY=replace_me_with_secure_key
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
REDIS_URL=redis://redis:6379/0
```

**frontend/.env.local.example**

```
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## First tasks (issues / tickets to create now)

1. **Project scaffolding** — create backend & frontend folders, add Dockerfile, basic .gitignore
2. **Auth & DB models** — implement `users`, `profiles` models and JWT auth endpoints
3. **Landing page + quiz UI (frontend)** — small React component that saves quiz result to backend
4. **Dashboard feed** — simple posts model + feed endpoint + frontend list view
5. **Chat skeleton** — WebSocket connection and message persistence (save messages to DB but UI can be minimal)

---

## Short design notes for the landing quiz

* Quiz should be short (4–6 questions). Save result as `profile.score` and tags (e.g., anxiety, stress, insomnia).
* On submit, create/update the user's `profile` and redirect to dashboard with a query param like `?onboarded=true` so the UI can show a personalized feed.
* Backend endpoint: `POST /api/onboard/quiz` with `{ user_id, answers: {...}, tags: [], score }`.

---

## Contributing

* Use a `main` branch as protected; create feature branches `feat/landing-quiz`, `feat/auth`, etc.
* Use GitHub issues and link PRs to issues. Add basic CI to run tests on PRs.

---

## License

This repository is licensed under the MIT License — see `LICENSE` file.

---

# LICENSE (MIT)

```
MIT License

Copyright (c) YEAR <Your Name>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

*If you want, I can now scaffold the initial code (FastAPI backend + Next.js frontend + Docker compose) and create the first working landing page + quiz and auth endpoints. Say **"scaffold"** and I will generate the code files for you to copy/run.*
