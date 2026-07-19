# Keyboard Shortcuts

Claude Code ships with a set of built-in keyboard shortcuts that let you navigate conversations, manage context, and trigger actions without reaching for the mouse. You can view all current bindings by running `/help` inside a session, and you can fully customize them by editing `~/.claude/keybindings.json`. Mastering even a handful of shortcuts — like `Ctrl+C` to cancel a running tool and `Ctrl+R` to search history — dramatically speeds up your everyday workflow.

## Key shortcuts to know

| Shortcut | Action |
|---|---|
| `Ctrl+C` | Cancel the current tool / stop generation |
| `Ctrl+R` | Reverse search through prompt history |
| `Ctrl+L` | Clear the screen (keeps conversation context) |
| `Escape` | Return to the prompt without cancelling |
| `Up / Down` | Navigate previous prompts |
| `Tab` | Autocomplete slash commands |

## Custom keybindings example

Add or remap shortcuts in `~/.claude/keybindings.json`:

```json
[
  {
    "key": "ctrl+shift+r",
    "command": "workbench.action.reloadWindow",
    "description": "Reload Claude Code session"
  },
  {
    "key": "ctrl+shift+c",
    "command": "/clear",
    "description": "Clear conversation and reset context"
  }
]
```

You can also define **chord bindings** (two-key sequences) for more complex actions:

```json
[
  {
    "key": "ctrl+k ctrl+s",
    "command": "/compact",
    "description": "Compact context with a summary"
  }
]
```

## Try it yourself

Open a Claude Code session, type a long prompt, then press `Ctrl+R` and start typing a keyword from an earlier session — Claude Code searches your history just like a shell does. Then open `~/.claude/keybindings.json` (create it if it doesn't exist) and add a shortcut for your most-used slash command.
