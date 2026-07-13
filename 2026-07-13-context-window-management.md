# Context Window Management

## What It Is

Claude Code operates within a finite context window — the total amount of text (your messages, file contents, tool outputs, and Claude's replies) that can be held in memory at once. When conversations grow long, the harness automatically compresses older messages into a rolling summary so work can continue without hitting hard limits. Understanding this helps you avoid surprises and keep sessions productive.

## Key Concepts

- **Context = everything**: your prompts, Claude's replies, file reads, bash output, tool results — all count toward the limit.
- **Auto-compression**: when the window fills, earlier turns are summarized and compacted. Important details usually survive, but very long raw outputs (e.g. full log dumps) may be trimmed.
- **CLAUDE.md as stable memory**: anything you want Claude to remember across compressions or sessions should live in `CLAUDE.md` — it's re-injected at the start of every turn.

## Copy-Pasteable Example

```bash
# Keep noisy command output from bloating your context:
# Instead of running a command that prints 10,000 lines directly...
npm test 2>&1 | tail -50          # only last 50 lines reach Claude

# Or redirect large outputs to a file and let Claude read just what it needs:
npm test > /tmp/test-output.txt 2>&1
# Then ask Claude: "Read /tmp/test-output.txt and summarize the failures."

# Use CLAUDE.md for persistent facts you never want compressed away:
echo "## Architecture\n- API lives in src/api/\n- DB config in config/db.ts" >> CLAUDE.md
```

## Try It Yourself

Open a long-running Claude Code session and intentionally pipe a large command output through `| tail -100` before sending it. Then add one persistent fact about your project to `CLAUDE.md` and notice how it survives even after context compression kicks in. This single habit — trim noise, persist signal — keeps sessions accurate and focused for hours.
