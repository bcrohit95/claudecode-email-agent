# Slash Commands

Slash commands are built-in shortcuts you type directly in the Claude Code chat to trigger specific actions without writing out full instructions. They give you fast access to common workflows like clearing context, reviewing code, committing, or running custom skills you've defined. You can also create your own slash commands by adding skills to your project's `.claude/` directory.

## Example

```
# Clear your context window
/clear

# Review your current working diff for bugs and improvements
/code-review

# See all available commands and skills
/help

# Run a custom skill you've created
/my-deploy-skill
```

## Try it yourself

Open Claude Code in your terminal and type `/help` to see every built-in command available to you. Then look inside `.claude/agents/` or `.claude/skills/` in your project to see if any custom slash commands are already defined — or create a new `.md` file there to add your own.
