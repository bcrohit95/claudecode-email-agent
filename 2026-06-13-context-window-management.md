# Context Window Management

## What It Is

Claude Code has a finite context window — the amount of text (code, conversation, tool output) it can hold in memory at once. When the context fills up, older content gets summarised automatically so the session can continue, but you can also manage it proactively to keep responses fast and relevant.

## Key Techniques

**1. /compact — Manual compaction**
Run this slash command to compress the current conversation into a summary, freeing up space while preserving the key facts Claude needs to keep working.

```
/compact
```

**2. /clear — Full reset**
Wipes the entire conversation history and starts fresh. Use this when you have finished one task and are starting an unrelated one.

```
/clear
```

**3. CLAUDE.md — Persistent context**
Instead of re-explaining your project every session, put key facts in a `CLAUDE.md` file at the repo root. Claude reads it automatically at session start, so you spend your context budget on the actual task.

```markdown
# CLAUDE.md
## Stack
- Python 3.12, FastAPI, PostgreSQL
- Tests: pytest, run with `make test`
- Lint: ruff, run with `make lint`

## Key conventions
- Use snake_case for all identifiers
- All DB queries go through src/db/queries.py
```

**4. Scoped reads — Don't load what you don't need**
Point Claude at a specific file or function rather than "look at the whole repo."

```
# Instead of: "look at the project"
# Say: "look at src/auth/login.py lines 40-80"
```

## Copy-Pasteable Example

```bash
cat > CLAUDE.md << 'EOF'
# Project Context

## Tech stack
- Node 20, TypeScript, Express
- DB: SQLite via Prisma ORM
- Tests: Vitest (npm test)

## File layout
- src/routes/ — HTTP handlers
- src/services/ — business logic
- src/db/ — Prisma schema + migrations

## Do not edit
- prisma/migrations/ (auto-generated)
EOF
```

## Try It Yourself

1. Open a Claude Code session in any repo.
2. Have a long conversation until you see a "context compressed" notice.
3. Run `/compact` before that happens — notice how Claude summarises the key decisions so far.
4. Add a `CLAUDE.md` with your stack and conventions, then start a fresh session with `/clear` — you will spend far less context budget on project bootstrapping.
