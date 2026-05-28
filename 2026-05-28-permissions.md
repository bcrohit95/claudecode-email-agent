# Claude Code Skill of the Day: Permissions

Permissions in Claude Code control which tools and shell commands Claude can
run automatically versus which ones require your explicit approval each time.
You configure them in `.claude/settings.json` (project-level) or
`~/.claude/settings.json` (global) using `"allow"` and `"deny"` lists, letting
you pre-approve safe, repetitive operations and block risky ones permanently.
This eliminates constant confirmation prompts for trusted commands while
keeping a safety net around destructive actions.

---

## Copy-Pasteable Example

Create or edit `.claude/settings.json` in your project root:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm test)",
      "Bash(npm run lint)",
      "Bash(git status)",
      "Bash(git diff)",
      "Read(**)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force)"
    ]
  }
}
```

With this config Claude will run your tests, linter, and git inspection
commands without asking, but will always be blocked from force-pushes or
recursive deletes.

---

## Try It Yourself

1. In your project root run:
   ```bash
   mkdir -p .claude && touch .claude/settings.json
   ```

2. Add the JSON above (or just the `"allow"` block with `"Bash(npm test)"`).

3. Ask Claude: *"Run my tests"* — it will execute without a permission prompt.

4. To make a permission global (applies to all projects), add the same entry
   to `~/.claude/settings.json` instead.

> **Tip:** Use the `/update-config` skill inside Claude Code to manage
> permissions interactively without hand-editing JSON.
