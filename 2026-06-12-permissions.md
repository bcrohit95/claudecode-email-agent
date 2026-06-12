# Permissions

Claude Code's permission system controls which tools and shell commands Claude can run without stopping to ask you first. By default, Claude prompts you before executing potentially risky actions (file writes, shell commands, network calls), but you can pre-approve specific patterns so it flows uninterrupted on trusted operations. Permissions live in `.claude/settings.json` (project-level) or `~/.claude/settings.json` (global), under `allow` and `deny` arrays.

## Example

```json
// .claude/settings.json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(pytest *)",
      "Bash(git status)",
      "Bash(git diff *)",
      "Read(**/*)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force *)"
    ]
  }
}
```

This lets Claude run any `npm run` script, pytest, read-only git commands, and file reads without prompting — while always blocking force-pushes and recursive deletes.

## Try it yourself

Open your project and run `/permissions` in Claude Code to see your current allow/deny list. Then add one entry — try allowing `Bash(npm test)` — and watch Claude stop prompting for that command on your next session.
