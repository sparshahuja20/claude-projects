# Claude Projects

A collection of Claude Code experiments and MCP server configurations.

## MCP Servers

### GitHub MCP
Configured via `.mcp.json` using the `@modelcontextprotocol/server-github` server.

Requires a GitHub Personal Access Token set as an environment variable:

```bash
export GITHUB_PERSONAL_ACCESS_TOKEN=your_token_here
```

## Setup

1. Clone the repo
2. Set the `GITHUB_PERSONAL_ACCESS_TOKEN` environment variable
3. Open in Claude Code — the GitHub MCP server will load automatically
