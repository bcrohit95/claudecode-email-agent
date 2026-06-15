# Slash Commands

Slash commands are built-in shortcuts you type directly in the Claude Code chat to trigger specific actions — things like clearing context, reviewing code, or running predefined workflows. They save you from typing long instructions repeatedly and give Claude a crisp, unambiguous signal about what you want. You can also create *custom* slash commands (stored as Markdown files in `.claude/commands/`) so your team's repeated workflows become one-word triggers.

## Example

```bash
# Built-in slash commands
/clear          # Wipe the conversation context and start fresh
/review         # Kick off a code review of the current diff
/help           # List all available slash commands

# Creating a custom slash command
mkdir -p .claude/commands
cat > .claude/commands/standup.md << 'EOF'
Summarize the git log from the last 24 hours into a short standup update:
- What was completed
- Any blockers mentioned in commit messages
EOF

# Now use it in chat:
# /standup
```

## Try it yourself

Open Claude Code in your project, type `/help` and press Enter to see every slash command available to you. Then create a `.claude/commands/deploy-check.md` file that instructs Claude to verify tests pass and the build is clean before deploying — you'll have a `/deploy-check` command ready to run any time.
