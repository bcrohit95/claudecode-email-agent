# CLAUDE.md Files

CLAUDE.md is a special markdown file that Claude Code reads automatically at the start of every session, giving it persistent project-level context about your codebase, conventions, and preferences — without you having to re-explain things each time. You can place one in your project root (for project-wide guidance), in subdirectories (for folder-specific context), or in `~/.claude/CLAUDE.md` (for global, cross-project preferences). It acts like a standing briefing: architecture notes, coding style rules, commands to run, things Claude should never do — all encoded once and automatically loaded.

## Copy-Pasteable Example

Create a `CLAUDE.md` in your project root:

```markdown
# Project: My API Service

## Stack
- Python 3.12 + FastAPI
- PostgreSQL via SQLAlchemy (async)
- Pytest for tests; run with `pytest -x`

## Coding Conventions
- Use snake_case for all identifiers
- Keep functions under 30 lines
- Never use `print()` — use `logging.getLogger(__name__)` instead

## Important Commands
- Start dev server: `uvicorn app.main:app --reload`
- Run migrations: `alembic upgrade head`
- Lint: `ruff check . && mypy .`

## Do Not
- Commit secrets or .env files
- Use synchronous database calls in async routes
- Skip type annotations on public functions
```

Claude Code will automatically load this file at session start and follow these rules throughout your conversation.

## Try It Yourself

Run this in your project root to scaffold a CLAUDE.md with your stack info:

```bash
claude "Generate a CLAUDE.md for this project based on the files you see. Include the tech stack, key commands, and coding conventions."
```

Then review and refine it — it becomes your project's persistent AI memory.
