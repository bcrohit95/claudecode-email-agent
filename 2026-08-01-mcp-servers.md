# MCP Servers

## What It Is

MCP (Model Context Protocol) servers are external processes that extend Claude Code's capabilities by exposing tools, resources, and prompts over a standardized protocol. You can connect Claude Code to an MCP server so it can interact with databases, APIs, file systems, or any custom service — without Claude needing built-in knowledge of that service. Think of MCP servers as plugins that give Claude new superpowers specific to your workflow.

## Copy-Pasteable Example

Add an MCP server to your Claude Code project by editing `.claude/settings.json`:

```json
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
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token-here"
      }
    }
  }
}
```

Once configured, restart Claude Code and you can ask: "List all open PRs in my repo" or "Search files matching *.log" — Claude will use the MCP tools automatically.

## Try It Yourself

Run `claude mcp list` in your terminal to see which MCP servers are currently configured. Then try adding the official filesystem MCP server with:

```bash
claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem .
```

This gives Claude direct access to read and write files in your current directory via the MCP protocol. Explore available community servers at https://github.com/modelcontextprotocol/servers.
