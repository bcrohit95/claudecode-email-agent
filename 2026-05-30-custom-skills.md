# Custom Skills

Custom Skills are reusable, shareable workflows you define for Claude Code — prompt files that live in `.claude/skills/` and become instant slash commands. You invoke them with `/skill-name` in any session, and Claude follows the instructions in that file automatically. They're perfect for encoding team conventions, repeated workflows, or complex multi-step tasks into a single reproducible command.

## Example

```bash
# Create a custom skill
mkdir -p .claude/skills

cat > .claude/skills/deploy-check.md << 'EOF'
Review the current branch for deploy readiness:
1. Run the test suite and report any failures
2. Check for uncommitted changes
3. Verify the changelog has an entry for today
4. Summarize go/no-go with a one-line verdict
EOF
```

Then in Claude Code, just type:
```
/deploy-check
```

Claude will run through all four steps automatically every time.

## Try it yourself

Create `.claude/skills/standup.md` with the content:

```
Summarize yesterday's git commits as a standup update, grouped by feature area. Keep it under 5 bullet points.
```

Then type `/standup` in Claude Code to instantly generate your daily standup notes from your actual commit history — no manual writing needed.
