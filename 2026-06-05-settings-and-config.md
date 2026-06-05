# Settings and Config

Claude Code's behavior can be customized through settings files at three levels: global (`~/.claude/settings.json`), project (`.claude/settings.json`), and session-local (`.claude/settings.local.json`). Settings control things like permissions, environment variables, hooks, model selection, and more — with more specific files taking precedence over broader ones. This layered system lets you share safe project settings with your team while keeping personal overrides local.

## Copy-Pasteable Example

Create a project-level settings file at `.claude/settings.json`:

```json
{
  "model": "claude-opus-4-8",
  "permissions": {
    "allow": ["Bash(npm:*)", "Bash(git status)", "Bash(git diff*)"],
    "deny": ["Bash(rm:-rf*)"]
  },
  "env": {
    "NODE_ENV": "development",
    "DEBUG": "true"
  }
}
```

This pins the model to Opus, pre-approves common npm and git commands, blocks dangerous `rm -rf`, and injects environment variables for every session in this project.

## Try It Yourself

Run `/config` inside Claude Code to open an interactive settings editor — no JSON editing required. To see what settings are active right now, run:

```bash
cat ~/.claude/settings.json        # global settings
cat .claude/settings.json          # project settings (if it exists)
cat .claude/settings.local.json    # your local overrides (gitignored)
```

Pro tip: commit `.claude/settings.json` to your repo so teammates get the same permission allowlist and model, but add `.claude/settings.local.json` to `.gitignore` for personal tweaks.
