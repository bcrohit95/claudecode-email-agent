# Custom Skills

Custom Skills let you package reusable instructions into named slash commands (e.g. `/deploy`, `/review`) that Claude Code loads on demand from `.claude/skills/` in your project or `~/.claude/skills/` globally. Each skill is a Markdown file with a YAML frontmatter `description` field that tells Claude when to trigger it automatically, plus a body of instructions Claude follows when the skill runs. Skills eliminate copy-pasting long prompts and keep team workflows consistent across every session.

## Example

Create a file at `.claude/skills/deploy.md`:

```markdown
---
description: Deploy the current branch to the staging environment. Use when the user asks to deploy, ship, or push to staging.
---

# Deploy to Staging

1. Run `npm run build` and confirm it exits 0.
2. Run `npm test` — abort if any tests fail and tell the user which ones.
3. Run `./scripts/deploy.sh staging` and stream the output.
4. After a successful deploy, open the staging URL in the browser preview and confirm the health-check endpoint returns 200.
5. Post a one-line summary: what was deployed, the commit SHA, and the staging URL.
```

Now inside Claude Code you can type `/deploy` to invoke it, or Claude will trigger it automatically when you say "ship this to staging."

## Try it yourself

1. Create `.claude/skills/standup.md` with a description like "Summarize what changed today for the standup meeting."
2. Add instructions that run `git log --since=yesterday --oneline` and format the output as bullet points.
3. Open Claude Code and type `/standup` — Claude will follow your instructions and give you a ready-to-paste standup update.
