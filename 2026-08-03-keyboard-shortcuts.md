# Keyboard Shortcuts

Claude Code has a set of built-in keyboard shortcuts that speed up your workflow without ever leaving the terminal. These shortcuts let you navigate history, manage multi-line input, and control the session — all from the keyboard. You can also customize or extend them by editing `~/.claude/keybindings.json`.

## Key Shortcuts to Know

| Shortcut | Action |
|---|---|
| `Ctrl+J` or `Enter` | Submit your message |
| `Shift+Enter` | Insert a newline (multi-line input) |
| `Up / Down Arrow` | Navigate message history |
| `Ctrl+C` | Interrupt a running tool or cancel current input |
| `Ctrl+L` | Clear the screen |
| `Ctrl+R` | Reverse-search your message history |
| `Esc` (double-tap) | Edit the last message you sent |

## Copy-Pasteable Example: Custom Keybinding

Add a chord shortcut to quickly insert a common prompt prefix:

```json
// ~/.claude/keybindings.json
[
  {
    "key": "ctrl+shift+p",
    "command": "insertText",
    "args": {
      "text": "Please review this code for security issues:\n"
    }
  }
]
```

Save the file — changes take effect the next time you start Claude Code.

## Try It Yourself

1. Open Claude Code in your terminal.
2. Start typing a long message, then press **Shift+Enter** to add a second line without submitting.
3. Press **Up Arrow** to pull in your previous message and edit it.
4. Try double-tapping **Esc** right after you send — it brings the message back into the input for a quick correction.

For a full list of bindable commands and chord syntax, run `/keybindings-help` inside Claude Code or check the docs.
