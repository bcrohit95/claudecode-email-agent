# MCP Servers

**Model Context Protocol (MCP) servers** let Claude Code connect to external tools and data sources — like databases, APIs, file systems, or web browsers — through a standardized interface. You configure them once in your Claude Code settings and Claude can then call them as tools during any session. This is how you extend Claude beyond its built-in capabilities without writing custom integrations each time.

## Copy-pasteable example

Add a filesystem MCP server to your project settings:

```json
// .claude/settings.json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/user/projects"]
    }
  }
}
```

After saving, run `claude` and ask: *"List the files in my projects folder"* — Claude will use the MCP server automatically.

## Try it yourself

Install the official Postgres MCP server (`npx @modelcontextprotocol/server-postgres`) and point it at a local DB. Then ask Claude to describe your schema or write a query — no copy-pasting connection strings or table names needed.
