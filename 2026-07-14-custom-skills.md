# Custom Skills

Custom Skills let you package reusable behaviors — multi-step workflows, project-specific commands, or team conventions — into a single slash command that Claude Code can invoke anywhere. You define a skill as a Markdown file under `.claude/skills/` (or `~/.claude/skills/` for global ones), describe when and how to use it, and Claude will read and follow those instructions automatically whenever the skill is triggered. This means you can encode things like "run our full review checklist" or "scaffold a new API endpoint" once and reuse them across every session.

## Example

Create a file at `.claude/skills/scaffold-endpoint.md`:

```markdown
---
name: scaffold-endpoint
description: Scaffold a new REST API endpoint with controller, route, and test stubs. Trigger when the user says "scaffold endpoint" or /scaffold-endpoint.
---

1. Ask the user for the endpoint name and HTTP method if not provided.
2. Create `src/controllers/<name>Controller.ts` using the project's controller pattern (check existing files for style).
3. Register the route in `src/routes/index.ts`.
4. Create `tests/<name>Controller.test.ts` with a describe block and one placeholder test.
5. Report the three files created.
```

Then in any Claude Code session just type:

```
/scaffold-endpoint
```

Claude will read the skill file and execute those exact steps.

## Try it yourself

Pick a task you repeat in every PR — like "check for console.logs before committing" — write it as a numbered checklist in `.claude/skills/pre-commit-check.md`, and invoke it with `/pre-commit-check`. Once it works the way you want, commit the file so your whole team gets the same workflow for free.
