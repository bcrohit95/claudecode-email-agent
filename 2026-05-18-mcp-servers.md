# MCP Servers

MCP (Model Context Protocol) Servers extend Claude Code by connecting it to external tools and data sources — think databases, APIs, file systems, or services like Gmail and GitHub. You configure them in your project or user settings, and Claude can then call them as tools during a session, just like built-in tools. This turns Claude Code from a coding assistant into a connected agent that can read emails, query databases, or interact with any service that has an MCP server.

## Example

Add this to your `.claude/settings.json` to wire up Gmail and GitHub MCP servers:

```json
{
  "mcpServers": {
    "gmail": {
      "command": "npx",
      "args": ["-y", "@gptscript-ai/claude-gmail-mcp"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<your-token>"
      }
    }
  }
}
```

Once added, Claude will automatically have access to those tools in every session for that project.

## Try it yourself

Add the filesystem MCP server to your project settings:

```bash
npx @modelcontextprotocol/server-filesystem /path/to/your/project
```

Then ask Claude: "List all TypeScript files in my project." Watch it use the MCP tool automatically — no extra prompting needed.

> **Pro tip:** Run `claude mcp list` in your terminal to see all MCP servers currently configured for your session.
