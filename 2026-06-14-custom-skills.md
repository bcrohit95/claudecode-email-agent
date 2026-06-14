# Custom Skills

Custom Skills let you package reusable, multi-step workflows into named slash commands that Claude Code can invoke automatically. Instead of repeating a long series of instructions every session, you write the workflow once as a Markdown file and trigger it with `/skill-name` from anywhere in Claude Code. Skills live in `~/.claude/skills/` (global) or `.claude/skills/` (project-level) and are written in plain Markdown with optional front-matter for metadata.

## Example

Create a file at `.claude/skills/run-checks.md`:

```markdown
---
description: Run linter, type-check, and tests in sequence, then summarize failures
---

1. Run `npm run lint` and capture output.
2. Run `npm run typecheck` and capture output.
3. Run `npm test` and capture output.
4. Summarize any failures found across all three commands in a bullet list.
   If everything passes, say "All checks passed."
```

Now type `/run-checks` in Claude Code and it executes all three steps automatically.

## Try it yourself

Create `.claude/skills/git-summary.md` with the instruction: "Show a one-paragraph summary of all commits made today, grouped by author." Then open Claude Code in any git repo and type `/git-summary` — no extra context needed, Claude will run `git log` and synthesize the summary for you.
