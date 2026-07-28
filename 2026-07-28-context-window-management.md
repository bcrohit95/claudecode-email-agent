# Context Window Management

Claude Code works within a finite context window — the total number of tokens (words + code) that can fit in a single conversation. When a long session fills up, Claude automatically summarizes older messages to free space, but you can also manage context proactively to keep responses sharp and avoid losing critical information.

## Key Concepts

- **Context limits:** Every model has a max context size. Sonnet 4.6 supports ~200k tokens. Large files, long diffs, or many tool results can fill it quickly.
- **Auto-summarization:** When the window gets full, Claude Code compresses older turns into a summary. Important details can be lost if you haven't anchored them.
- **CLAUDE.md as persistent context:** Put project facts, conventions, and key decisions in `CLAUDE.md` — it's loaded fresh each session, surviving context resets.

## Copy-Pasteable Example

```bash
# 1. Create a CLAUDE.md to anchor key facts across sessions
cat > CLAUDE.md << 'EOF'
# Project: MyApp

## Stack
- Python 3.12, FastAPI, PostgreSQL
- Tests: pytest, run with `pytest -x`

## Key conventions
- All API responses wrapped in {"data": ..., "error": null}
- Use snake_case for DB columns, camelCase in JSON responses

## Current focus
- Migrating auth to JWT (see src/auth/jwt.py)
EOF

# 2. In long sessions, explicitly ask Claude to summarize what it knows
# "Summarize the decisions we've made so far" -> paste summary into next session

# 3. Keep tool output lean — pipe large outputs through head/grep
git diff HEAD~5 | head -200   # don't dump 2000 lines into context
cat large_log.txt | grep ERROR | tail -50
```

## Try It Yourself

Open a project you've been working on and run `/init` — Claude Code will scan your codebase and write a `CLAUDE.md` for you automatically. Then open a new session and notice how Claude immediately understands your project structure without needing re-explanation. Edit `CLAUDE.md` to add any conventions or decisions that matter most to you.

**Bonus tip:** When you're deep in a long session and notice responses getting slower or less accurate, type `/clear` to reset the context window while keeping `CLAUDE.md` loaded — it's the fastest way to give Claude a clean slate without losing your project anchors.
