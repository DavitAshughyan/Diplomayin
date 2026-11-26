# Diplomayin — Learn English with AI

Decoupled full-stack web application built with **Next.js (App Router)** and **FastAPI (Python 3.11+)**.

## Project Structure

- `frontend/` — Next.js App Router, TypeScript, Tailwind CSS, shadcn/ui
- `backend/` — FastAPI, Pydantic v2, SQLAlchemy 2.0 (async), Redis, Cloudflare R2

## Local Development

### Frontend (`http://localhost:3000`)

```bash
cd frontend
cp .env.example .env.local
npm install
npm run dev
```

### Backend (`http://localhost:8000`)

```bash
cd backend
cp .env.example .env
python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
# source venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

- Swagger UI: `http://localhost:8000/docs`
- Health Check: `http://localhost:8000/health`
