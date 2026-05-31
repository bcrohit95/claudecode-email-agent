# Claude Code Skill of the Day: Slash Commands

## What Are Slash Commands?

Slash commands are shortcuts you type directly in the Claude Code chat interface (starting with `/`) to trigger built-in or custom actions instantly. They let you invoke complex workflows — like running a code review, clearing context, or toggling settings — with a single short command instead of writing out a full prompt. You can also create your own custom slash commands as Markdown files in your project's `.claude/commands/` directory.

## Copy-Pasteable Example

**Built-in commands:**
```
/help              # List all available commands
/clear             # Clear the current conversation context
/compact           # Summarize context to save space
/config            # Open settings to change model, theme, etc.
/cost              # Show token usage and cost for this session
/review            # Trigger a code review skill
```

**Create a custom slash command:**
```bash
# Create a custom command for your project
mkdir -p .claude/commands
cat > .claude/commands/test-and-lint.md << 'EOF'
Run the test suite and linter, then summarize any failures.

Steps:
1. Run: npm test
2. Run: npm run lint
3. Report a concise summary of failures (if any) or confirm all passed.
EOF
```

Now in Claude Code chat, type:
```
/test-and-lint
```
...and Claude will execute that workflow automatically.

**Pass arguments to a custom command:**
```markdown
<!-- .claude/commands/explain-file.md -->
Explain the purpose of the file: $ARGUMENTS

Walk through its main exports, key logic, and any notable patterns.
```
Usage: `/explain-file src/auth/middleware.ts`

## Try It Yourself

1. Open Claude Code in your terminal (`claude`) or the web app.
2. Type `/help` and press Enter — browse the full list of built-in commands.
3. Create a `.claude/commands/standup.md` file in any project with a prompt like "Summarize today's git commits as a standup update." Then type `/standup` in Claude Code chat and watch it run.
