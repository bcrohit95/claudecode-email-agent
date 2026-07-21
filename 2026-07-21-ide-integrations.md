# IDE Integrations

Claude Code integrates directly into VS Code and JetBrains IDEs, letting you run Claude commands without leaving your editor. Once the extension is installed, Claude can read your open files, see your current cursor position, and apply edits inline — making it feel like a pair programmer sitting next to you rather than a separate terminal window.

## How it works

The extension connects to the Claude Code CLI running in the background. When you trigger Claude from inside the IDE (via the command palette or a keyboard shortcut), it automatically passes context like the active file and selected text, so you don't have to copy-paste code into a chat window.

## Copy-pasteable example

**VS Code — install the extension:**
```bash
code --install-extension anthropics.claude-code
```

Or search "Claude Code" in the Extensions panel (Ctrl+Shift+X / Cmd+Shift+X).

Once installed, open the command palette and try:
```
> Claude: Open Chat
> Claude: Explain selected code
> Claude: Fix selected code
```

**JetBrains (IntelliJ, PyCharm, WebStorm, etc.):**
Go to *Settings → Plugins → Marketplace*, search **Claude Code**, and install. The same commands appear under *Tools → Claude Code* in the menu bar.

## Try it yourself

1. Open a file with a bug or code you want to understand.
2. Select the relevant lines.
3. Open the command palette and run **"Claude: Explain selected code"**.
4. Watch Claude explain the selection using full file context — no copy-paste needed.

> **Tip:** In VS Code you can bind Claude commands to custom keyboard shortcuts via *Preferences → Keyboard Shortcuts* — search "Claude" to see all available actions.
