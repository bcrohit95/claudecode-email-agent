# Settings and Config

Claude Code's behavior is controlled through `settings.json` files at three levels: **global** (`~/.claude/settings.json`), **project** (`.claude/settings.json`), and **local** (`.claude/settings.local.json`). Settings cascade from global → project → local, so project-level settings override global ones and local settings override both — letting you customize Claude per-repo without touching your global config.

The most powerful settings are **permissions** (which tools Claude can run without asking), **environment variables** (injected into every session), and **hooks** (shell commands that fire automatically on events like tool calls or session end). You can edit `settings.json` directly or use the `/config` slash command inside Claude Code for interactive changes.

## Copy-pasteable example

Add this to your project's `.claude/settings.json` to allow `npm test` and `npm run lint` without permission prompts, and set a custom env var:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm test)",
      "Bash(npm run lint)",
      "Bash(npm run build)"
    ]
  },
  "env": {
    "NODE_ENV": "test",
    "MY_API_BASE": "http://localhost:3000"
  }
}
```

To set a model preference globally:

```json
// ~/.claude/settings.json
{
  "model": "claude-opus-4-7"
}
```

## Try it yourself

Open a project you work in often and run:

```bash
cat .claude/settings.json 2>/dev/null || echo "No project settings yet"
```

Then add an `allow` entry for the test command you run most (`pytest`, `go test ./...`, `cargo test`, etc.) so Claude never has to ask permission to run it again. Commit `.claude/settings.json` to share the config with your whole team.
