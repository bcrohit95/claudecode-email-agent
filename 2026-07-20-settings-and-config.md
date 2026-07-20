# Settings and Config

Claude Code stores its configuration in JSON files at two levels: **user-level** (`~/.claude/settings.json`) for preferences that apply across all projects, and **project-level** (`.claude/settings.json` at the repo root) for team-shared settings. You can also create a `settings.local.json` alongside the project file for personal overrides that aren't committed to version control. This layering lets you set global defaults while still customising per-repo behaviour.

## Example — allow a tool without being prompted every time

Add this to your project's `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(git log *)",
      "Bash(git diff *)"
    ]
  }
}
```

With these entries, Claude Code will run those `npm` and `git` commands automatically without pausing to ask for permission each time.

## Another common option — set a default model

In `~/.claude/settings.json`:

```json
{
  "model": "claude-sonnet-5"
}
```

You can override this per-project by adding a `model` key to the project-level settings file.

## Try it yourself

1. Open (or create) `~/.claude/settings.json` in your editor.
2. Add a `"permissions"` block with one `Bash(...)` pattern for a command you run often — something like `"Bash(pytest *)"`.
3. Start a Claude Code session and ask it to run your tests — notice there's no permission prompt.
4. Commit `.claude/settings.json` to your repo so teammates get the same frictionless experience.

> **Tip:** Run `/config` inside a Claude Code session to browse and edit settings interactively without touching the JSON files directly.
