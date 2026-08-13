---
name: project-setup
description: >
  Sets up a new fullstack project from scratch. Invoke manually with
  /project-setup when starting a new repo.
disable-model-invocation: true
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
- `README.md` — project name and one-line description only
- `.env.example` — placeholder keys, no real values

---

## Step 3 — Scaffold

**Fallback rule — applies to any confirmed stack WITHOUT a section below**
(Node/Express, Go/Gin, Vue, PostgreSQL, or anything added to the menu later):

1. Propose a minimal scaffold plan before running anything: init command,
   a single health-check entrypoint, and a directory layout mirroring the
   patterns in this file (config/, api/, db/ with .gitkeep).
2. Show the exact commands you intend to run.
3. Get explicit confirmation, then execute. Never improvise silently.
4. Note in the final summary that this stack used the fallback path, so the
   user can decide whether to promote it to a dedicated section.

### Python / FastAPI

```bash
cd backend
uv init .
uv add fastapi "uvicorn[standard]"
```

If `uv` is not installed, stop and tell the user before proceeding.

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

Create `.claude/settings.json` at project root. These deny rules are the
enforced replacement for a context-exclusion file (Claude Code has no native
`.claudeignore`):

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./**/secrets/**)",
      "Bash(git push --force*)",
      "Bash(git push -f*)"
    ]
  }
}
```

Do NOT set a `model` key here — model preference lives in
`~/.claude/settings.json` so it isn't forced on anyone else who clones the repo.

Create `CLAUDE.md` at project root, filled in with the actual confirmed values
(no bracket placeholders left behind):

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
Write every line in this file in plain English. A developer who has
never seen this repo should understand what each folder does from
one reading.
- [key folder]: [what lives here]
- [key folder]: [what lives here]
```

---

## Step 5 — CodeGraph

Check first: `command -v codegraph`.

- If installed: run `codegraph init`. Creates `.codegraph/` and builds the full
  symbol graph; the file watcher maintains it automatically. Confirm
  `.codegraph/` is in `.gitignore`.
- If NOT installed: skip this step, note it in the final summary, and do not
  attempt to install it without asking.

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

1. Start each server independently and confirm no errors. If a server fails to
   start, report the error and stop — do not commit a broken scaffold.
2. Initial commit: `git add -A && git commit -m "Initial scaffold"`
3. Print summary: what was created, how to run, what was skipped (if anything),
   and what is next
