# Permissions

Claude Code uses a permissions system to control which tools and shell commands it can run automatically versus which require your explicit approval. By default, potentially dangerous operations (like writing files, running shell commands, or pushing to git) prompt you for confirmation, while read-only operations are usually allowed freely. You can customize these rules in your `settings.json` or `settings.local.json` to streamline your workflow without compromising safety.

## Example

In `.claude/settings.json`, you can allow specific bash commands to run without prompting:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run test:*)",
      "Bash(git status)",
      "Bash(git diff*)",
      "Bash(cat *)",
      "Read(*)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force*)"
    ]
  }
}
```

This setup lets Claude run your test suite, check git status, and read files without asking — but always prompts before any destructive or irreversible operation.

## Try it yourself

Run `/permissions` inside a Claude Code session to see your current permission state, then try adding a specific `Bash(npm run lint)` entry to your project's `.claude/settings.json`. Next time Claude needs to lint your code, it'll run without prompting — saving you a click on every iteration.
