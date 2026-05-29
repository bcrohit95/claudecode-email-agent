# Context Window Management

## What It Is
Claude has a finite context window — the total amount of text (your messages, file contents, tool results, and Claude's replies) that can fit in one session. When a session grows too large, older content is summarized or dropped, which can cause Claude to "forget" earlier instructions or code. Understanding how to manage the context window keeps Claude accurate and efficient throughout long sessions.

## Key Concepts
- **Compact vs. Summarize**: Claude Code automatically compacts the conversation when it nears the limit, summarizing prior turns. You can trigger this manually with `/compact` to reclaim space before it becomes critical.
- **Be selective with reads**: Instead of asking Claude to read entire large files, point it to specific line ranges (`Read file.py lines 50-100`) so tool results don't bloat the context.
- **CLAUDE.md as persistent memory**: Put project-wide facts (architecture, conventions, key paths) in `CLAUDE.md` so you don't have to re-paste them every session — Claude reads it fresh each time.

## Copy-Pasteable Example

```bash
# Manually compact the conversation to free up context space
/compact

# Read only the relevant portion of a large file
# (in your prompt to Claude)
"Read src/api/routes.py lines 1-80 and tell me what auth middleware is used"

# Check roughly how full your context is
/status
```

## CLAUDE.md Tip
Put this near the top of your `CLAUDE.md` to remind Claude of critical facts without eating conversation space each turn:

```markdown
## Key Paths
- API entry point: src/api/main.py
- DB models: src/models/
- Config: config/settings.yaml

## Conventions
- All new endpoints must have a corresponding test in tests/api/
- Use snake_case for Python, camelCase for JS
```

## Try It Yourself
Open a long session where you've already read several files. Type `/compact` — Claude will summarize the history and free up space. Then check `/status` to see the updated token usage. Notice how Claude retains the important context (your goals, key file facts) while dropping the raw tool-result noise.
