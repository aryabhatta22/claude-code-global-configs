---
name: project-setup
description: Sets up a new fullstack project from scratch. Use when starting any
  new repo, scaffolding a new project, or setting up a development environment.
  Invoke with /setup-project.
disable-model-invocation: true
---

## Before doing anything, ask the user these questions all at once:

1. Project name?
2. Backend language and framework?
   Options: Python/FastAPI, Node/Express, Go/Gin, None
3. Frontend?
   Options: React (JavaScript), React (TypeScript), Vue, None
4. Database?
   Options: SQLite, PostgreSQL, None
5. Confirm the choices, then begin.

---

## Common Steps (Every Project)
- git init at root
- .gitignore for chosen stack(s)
- README.md (project name + one-line description)
- .env.example with placeholder keys
- If frontend exists: root package.json with concurrently

---

## Python / FastAPI Backend
- Create backend/ directory
- uv init . inside backend/
- uv add fastapi "uvicorn[standard]"
- Create main.py with basic health check endpoint
- Create config/config.yaml with empty sections
- Create backend/agents/, backend/api/, backend/db/

## SQLite Database (with Python)
- Create db/schema.sql
- Create db/init_db.py (runs schema.sql, uses CREATE TABLE IF NOT EXISTS)
- Add DB path to config.yaml

## React Frontend (JavaScript)
- From root: npm create vite@latest frontend -- --template react
- cd frontend && npm install
- ask for necessary only package installation based on user choices. Like styling options: styled-components, tailwind etc or logging option for backend. Don't make it too large just initially required packages.

## React Frontend (TypeScript)
- From root: npm create vite@latest frontend -- --template react-ts

---

## Final Steps (All Projects)
- If frontend + any backend: npm install --save-dev concurrently at root
- Write dev script in root package.json
- Verify: start each server independently, confirm no errors
- Print summary: what was created, how to run
