# Keyboard Shortcuts

Claude Code ships with a set of keyboard shortcuts that let you navigate and control your session without reaching for the mouse or typing slash commands. Shortcuts work in the interactive REPL and cover common actions like submitting a prompt, clearing the screen, interrupting a running tool, and toggling between modes. You can view the full built-in list with `/help` and customize or add your own bindings in `~/.claude/keybindings.json`.

## Key built-in shortcuts

| Shortcut | Action |
|---|---|
| `Enter` | Submit your current message |
| `Shift+Enter` | Insert a newline (multi-line input) |
| `Ctrl+C` | Interrupt / cancel the current operation |
| `Ctrl+L` | Clear the terminal screen |
| `Up / Down` | Cycle through prompt history |
| `Ctrl+R` | Reverse-search prompt history |
| `Esc` | Cancel current input / return to prompt |

## Copy-pasteable example — add a custom keybinding

Create or edit `~/.claude/keybindings.json`:

```json
{
  "bindings": [
    {
      "key": "ctrl+shift+r",
      "command": "/review",
      "description": "Run code review on current diff"
    },
    {
      "key": "ctrl+shift+t",
      "command": "/test",
      "description": "Run the test suite"
    }
  ]
}
```

After saving, restart Claude Code — the new chords are live immediately.

## Try it yourself

1. Open Claude Code and type a multi-line prompt using `Shift+Enter` to add newlines before hitting `Enter` to submit.
2. Mid-response, press `Ctrl+C` to interrupt and see how Claude Code stops cleanly.
3. Add the `/review` binding above, then trigger it with `Ctrl+Shift+R` — notice you never had to type the slash command manually.
