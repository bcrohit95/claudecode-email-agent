# Settings and Config

Claude Code's behavior is controlled through JSON settings files stored at `~/.claude/settings.json` (global) or `.claude/settings.json` (project-level). These files let you configure permissions, environment variables, hooks, and default behaviors — without needing to pass flags every time you run the CLI. Project-level settings override global ones, so you can tailor behavior per repo.

## Copy-pasteable example

Create or edit `~/.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm:*)",
      "Bash(git:*)",
      "Bash(python3:*)"
    ]
  },
  "env": {
    "NODE_ENV": "development"
  },
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo '[hook] Bash tool finished'"
          }
        ]
      }
    ]
  }
}
```

The `permissions.allow` list pre-approves specific tools so Claude stops prompting you. The `env` block injects environment variables into every session. The `hooks` block wires shell commands to tool lifecycle events.

## Try it yourself

Run: `claude /config`

This opens the interactive settings editor. Try adding `Bash(npm:*)` to your allow list — next time Claude wants to run an npm command, it will proceed automatically without a prompt. You can also directly edit `~/.claude/settings.json` in any text editor and the changes take effect on the next Claude Code session.
