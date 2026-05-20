# Keyboard Shortcuts

Claude Code ships with a set of built-in keyboard shortcuts that let you navigate conversations, manage context, and trigger actions without ever reaching for the mouse. You can view all defaults by running `/help` inside a session, and you can fully customize or add chord bindings by editing `~/.claude/keybindings.json`. Mastering even a handful of shortcuts — like quickly clearing context or toggling fast mode — dramatically speeds up your workflow.

## Key defaults to know

| Shortcut | Action |
|---|---|
| `Ctrl+C` | Cancel the current response / interrupt a running tool |
| `Ctrl+L` | Clear the terminal display (keeps conversation history) |
| `Ctrl+R` | Fuzzy-search your prompt history |
| `Escape` / `Ctrl+G` | Abort the current tool call mid-flight |
| `Up / Down arrows` | Navigate previous prompts in the input box |

## Copy-pasteable customization example

Add a chord shortcut that inserts a ready-made debugging prompt:

```json
// ~/.claude/keybindings.json
{
  "bindings": [
    {
      "keys": "ctrl+d ctrl+b",
      "action": "insert_text",
      "value": "Add detailed debug logging to the function above and explain each log line."
    }
  ]
}
```

After saving, press `Ctrl+D` then `Ctrl+B` inside any Claude Code session to paste that prompt instantly.

## Try it yourself

1. Run `claude` to open a session.
2. Type a multi-line prompt, then press `Ctrl+R` — notice the fuzzy-search history overlay.
3. Open `~/.claude/keybindings.json` (create it if absent) and add one custom `insert_text` binding for a prompt you type repeatedly.
4. Restart Claude Code and verify the chord works.

> Tip: chord bindings (two-key sequences like `ctrl+d ctrl+b`) are great for longer boilerplate prompts — they're unlikely to conflict with terminal shortcuts.
