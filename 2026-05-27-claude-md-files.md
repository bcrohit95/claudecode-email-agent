# Claude Code Daily Skill: CLAUDE.md Files

## What it is
CLAUDE.md is a Markdown file that Claude Code reads automatically at the start of every session. Place one in your project root to give Claude persistent context about your codebase — architecture notes, coding conventions, preferred commands — without re-explaining things each time.

You can have two levels:
- **~/.claude/CLAUDE.md** — global preferences that apply to every project
- **<project>/CLAUDE.md** — repo-specific guidance (checked into source control)

## Copy-pasteable example

Create a CLAUDE.md in your project root:

```markdown
# My Project

## Stack
- Backend: FastAPI + PostgreSQL
- Frontend: React + TypeScript

## Commands
- Run tests: `pytest -x`
- Lint: `ruff check . && mypy .`
- Dev server: `uvicorn app.main:app --reload`

## Conventions
- Use snake_case for Python, camelCase for TypeScript
- All DB queries go through the repository layer (app/repositories/)
- Never commit secrets; use .env (gitignored)
```

Claude will read this file automatically and follow your conventions every session.

## Try it yourself
1. Run: `claude /init` — Claude Code will scan your project and generate a CLAUDE.md for you automatically.
2. Review and edit the generated file to add anything it missed (secret commands, gotchas, team norms).
3. Commit it to your repo so your whole team benefits from the same Claude context.
