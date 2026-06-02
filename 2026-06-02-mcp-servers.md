# MCP Servers

MCP (Model Context Protocol) Servers let Claude Code connect to external tools, databases, APIs, and services — extending what Claude can do beyond its built-in capabilities. You configure them in your project or user settings (`.claude/settings.json`), and once connected they appear as callable tools during your session. Common uses include GitHub, web search, databases, Slack, file systems, and custom internal APIs.

## Example: Add a GitHub MCP server

```json
// .claude/settings.json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
      }
    }
  }
}
```

Once added, Claude can search repos, read issues, create PRs, and more — all from within your conversation.

You can also add servers interactively from the CLI:

```bash
# Add a server by name (Claude Code fetches the config)
claude mcp add github

# List all configured MCP servers
claude mcp list

# Remove a server
claude mcp remove github
```

## Try it yourself

Run `claude mcp add` in your terminal — it walks you through adding a server interactively. Browse available community servers at https://modelcontextprotocol.io/servers to find one that fits your stack (databases, observability, CI/CD, and more).
