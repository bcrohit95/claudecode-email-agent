# CLAUDE.md Files

## What It Is

CLAUDE.md is a special Markdown file that Claude Code reads automatically at the start of every session. It lets you encode persistent project context — coding conventions, architecture notes, key commands, and team norms — so you never have to re-explain the same things. Place it at the root of your repo and Claude will treat its contents as standing instructions throughout the session.

## Copy-Pasteable Example

Create a CLAUDE.md at your project root:

```markdown
# MyApp Project

## Stack
- Backend: FastAPI (Python 3.12)
- Frontend: React + TypeScript
- DB: PostgreSQL via SQLAlchemy (async)

## Dev Commands
- Run tests: `pytest -x`
- Start dev server: `uvicorn app.main:app --reload`
- Lint: `ruff check . && mypy .`

## Conventions
- All new endpoints must have a corresponding Pydantic request/response schema.
- Use `snake_case` for Python, `camelCase` for TypeScript.
- Never commit secrets; use `.env` files loaded via `python-dotenv`.

## Important Files
- `app/config.py` — central settings (loaded from env)
- `app/models/` — SQLAlchemy ORM models
- `frontend/src/api/` — all API client calls live here
```

Now every Claude Code session automatically knows your stack, commands, and conventions without any prompting.

## Hierarchy & Scoping

CLAUDE.md files are composable:
- `~/.claude/CLAUDE.md` — global rules for all your projects
- `<project-root>/CLAUDE.md` — project-wide context
- `<subdirectory>/CLAUDE.md` — scoped rules for that subtree (e.g., a `frontend/CLAUDE.md` just for React conventions)

All three are loaded and merged; more specific files take precedence.

## Try It Yourself

1. Run `claude` in any project you work on regularly.
2. Ask: "What testing framework does this project use?" — Claude probably won't know.
3. Add a `CLAUDE.md` at the root with your stack details.
4. Start a fresh session and ask the same question — Claude will answer instantly from the file.

Bonus: run `/init` inside Claude Code and it will auto-generate a starter CLAUDE.md by scanning your repo structure.
