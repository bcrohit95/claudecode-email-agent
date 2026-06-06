# IDE Integrations

Claude Code integrates directly into VS Code and JetBrains IDEs (IntelliJ, PyCharm, WebStorm, GoLand, etc.), bringing the full Claude Code experience — inline diffs, chat sidebar, and terminal access — without leaving your editor. The integration automatically shares your current file and selection with Claude, so you can ask questions or request edits with precise context using `@file#line-range` references. Both extensions connect to the same `claude` binary you use in the terminal, so your settings, permissions, and MCP servers carry over seamlessly.

---

## Copy-pasteable example — VS Code setup & usage

```bash
# 1. Install the extension
Ctrl+Shift+X  →  search "Claude Code"  →  Install

# 2. Open Claude Code in a new tab
Ctrl+Shift+P  →  "Claude Code: Open in New Tab"

# 3. Toggle focus between editor and Claude input
Ctrl+Esc        (Windows/Linux)
Cmd+Esc         (Mac)

# 4. Auto-insert a file/selection reference into the prompt
Alt+K           (Windows/Linux)   — inserts @filename#line-range
Option+K        (Mac)

# JetBrains: install from
# Settings → Plugins → Marketplace → search "Claude Code"
```

---

## Try it yourself

Open any file in VS Code, select 3–5 lines of code, then press `Alt+K` (Windows/Linux) or `Option+K` (Mac). Claude Code will auto-insert an `@filename#line-range` reference into the prompt box. Type your question and press Enter — Claude sees exactly the lines you highlighted, with no copy-pasting needed.
