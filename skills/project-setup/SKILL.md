---
name: project-setup
description: >
  Sets up a new fullstack project from scratch. Invoke manually with
  /project-setup when starting a new repo. Do not auto-trigger.
disable-model-invocation: true
user-invocable: true
---

# Project Setup

## Step 1 — Ask all questions before doing anything

Ask these together in a single message. Do not begin until confirmed.

1. Project name and one-line description?
2. Backend: Python/FastAPI · Node/Express · Go/Gin · None
3. Frontend: React (JavaScript) · React (TypeScript) · Vue · None
4. Database: SQLite · PostgreSQL · None

Confirm choices, then begin.

---

## Step 2 — Common steps (every project)

- `git init` at root
- `.gitignore` covering: `.env`, `__pycache__/`, `.venv/`, `node_modules/`,
  `logs/`, `.codegraph/`, `*.pyc`, `dist/`, `.DS_Store`
- `.claudeignore` — same as `.gitignore` plus any large data folders
- `README.md` — project name and one-line description only
- `.env.example` — placeholder keys, no real values

---

## Step 3 — Backend scaffold

### Python / FastAPI

```bash
cd backend
uv init .
uv add fastapi "uvicorn[standard]"
```

Then create:
- `backend/main.py` — single `/health` endpoint returning `{"status": "ok"}`
- `backend/config/config.yaml` — empty sections as placeholders
- `backend/agents/`, `backend/api/`, `backend/db/` — empty directories with `.gitkeep`

### SQLite (with Python)

- `backend/db/schema.sql` — empty, ready for table definitions
- `backend/db/init_db.py` — reads and runs schema.sql, uses `CREATE TABLE IF NOT EXISTS`
- Add `db_path` key to `config.yaml`

### React (JavaScript)

```bash
npm create vite@latest frontend -- --template react
cd frontend && npm install
```

Ask user: Tailwind / styled-components / plain CSS / none.
Install only what they confirm. Nothing speculative.

### React (TypeScript)

```bash
npm create vite@latest frontend -- --template react-ts
cd frontend && npm install
```

Same styling question as above.

---

## Step 4 — Claude Code configuration

Create `.claude/settings.json` at project root:

```json
{
  "model": "opusplan"
}
```

Create `.claude/CLAUDE.md` at project root with these sections:

```
# [Project Name]
[One-line description]

## Stack
- Backend: [language / framework]
- Frontend: [framework / None]
- Database: [choice / None]
- Package manager: [uv / npm / etc]

## Commands
- Start backend: [command]
- Start frontend: [command]
- Run tests: [command]
- Lint: [command]

## Structure
- [key folder]: [what lives here]
- [key folder]: [what lives here]
```

---

## Step 5 — CodeGraph

```bash
codegraph init
```

Creates `.codegraph/` and builds the full symbol graph in one step.
File watcher maintains it automatically. No further manual steps needed.
Confirm `.codegraph/` is in `.gitignore`.

---

## Step 6 — Final steps

If frontend and backend both exist:

```bash
npm install --save-dev concurrently
```

Write `dev` script in root `package.json`:

```json
{
  "scripts": {
    "dev": "concurrently \"npm run dev:backend\" \"npm run dev:frontend\""
  }
}
```

Then:

1. Start each server independently and confirm no errors
2. Initial commit: `git add -A && git commit -m "Initial scaffold"`
3. Print summary: what was created, how to run, what is next
