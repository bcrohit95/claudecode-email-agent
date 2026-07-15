# Slash Commands

Slash commands are built-in shortcuts you type directly in the Claude Code prompt to trigger specific actions or skills — think of them like keyboard shortcuts for your AI workflow. You can run things like `/review`, `/fix`, `/commit`, or custom skills your team has defined, all without leaving the chat interface. They work both in the CLI and the web app, and can be chained with arguments for fine-grained control.

## Example

```
# Run a code review at medium effort
/code-review --effort medium

# Commit staged changes with an auto-generated message
/commit

# Run your custom skill with an argument
/deep-research "What are the best practices for React Server Components in 2026?"
```

## Try it yourself

Open Claude Code and type `/` — you'll see a menu of available slash commands autocomplete as you type. Pick `/help` to see the full list, or try `/code-review` on a file you recently changed to get instant feedback without leaving your editor.
