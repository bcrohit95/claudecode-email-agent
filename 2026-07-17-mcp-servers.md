# MCP Servers

Model Context Protocol (MCP) servers let Claude Code connect to external tools and data sources — think databases, APIs, file systems, or custom services — directly from your coding session. You add them once to your Claude Code config, and Claude can then call them as tools whenever they're useful, without you having to copy-paste context manually.

## Example: Adding an MCP server to Claude Code

```jsonc
// ~/.claude/claude.json  (or .claude/settings.json in your project)
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/your/project"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_yourtoken"
      }
    }
  }
}
```

Once configured, Claude can call `mcp__filesystem__read_file`, `mcp__github__create_issue`, etc. automatically during a session.

## Try it yourself

1. Install the official Postgres MCP server:
   ```bash
   npm install -g @modelcontextprotocol/server-postgres
   ```
2. Add it to your Claude Code config with your connection string.
3. Open Claude Code and ask: *"Show me the tables in my database"* — Claude will call the MCP tool without any extra setup.

> **Tip:** Run `/mcp` inside a Claude Code session to see all connected servers and their available tools.
