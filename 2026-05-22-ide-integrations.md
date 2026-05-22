# IDE Integrations

Claude Code integrates directly into VS Code and JetBrains IDEs (IntelliJ, PyCharm, WebStorm, etc.), letting you run Claude Code commands without ever leaving your editor. Once installed, you get an embedded terminal panel with Claude Code running alongside your editor, so you can ask Claude to edit files and immediately see the diffs inline in your IDE's file tree.

## How to install

**VS Code:**
```bash
# Install the extension from the marketplace
code --install-extension anthropics.claude-code

# Or search "Claude Code" in the VS Code Extensions panel (Ctrl+Shift+X)
```

**JetBrains (IntelliJ, PyCharm, WebStorm, etc.):**
```
Settings → Plugins → Marketplace → search "Claude Code" → Install
```

After installing, open the Claude Code panel (usually a sidebar icon or via the terminal panel) and it will launch Claude Code in your project's root directory automatically.

## Key IDE-specific features

```
# In VS Code, Claude Code adds:
# - Diff viewer: edits show as inline diffs you can accept/reject
# - Command palette integration: Ctrl+Shift+P → "Claude Code"
# - File context: @-mention open files directly in the chat

# Example: Ask Claude to refactor while seeing the diff live
> Refactor the fetchUser function in src/api.ts to use async/await
# → Claude edits the file, VS Code shows the diff in the editor gutter
```

## Try it yourself

1. Install the Claude Code VS Code extension and open a project.
2. Press `Ctrl+Shift+P` and type "Claude Code" to see available commands.
3. Ask Claude to "explain the current file" while a file is open — it will automatically read the file you're viewing and give you a contextual explanation.
