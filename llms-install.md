# Awesome Tools MCP Server — Automated Installation Guide

This guide is written for AI coding agents (Cline, Cursor, Claude Code, Codex, Windsurf, VS Code, etc.) to install and configure the Awesome Tools MCP server automatically. Follow the steps in order.

## What this server does

Awesome Tools (`https://awesome.tools/mcp`) is a remote Streamable HTTP MCP server for [Awesome Tools](https://awesome.tools), a curated directory of SaaS and AI tools. It provides 7 tools:

- `search_tools` — search published tools by keyword, category, tag, or featured status.
- `get_tool` — inspect a published tool or check the status and DR eligibility of a pending submission.
- `list_categories` — list all directory categories and published tool counts.
- `list_tags` — list all directory tags and published tool counts.
- `submit_tool` — submit a SaaS or AI tool (`free_backlink` for DR 20+ domains, `featured_49` for $49 Featured Launch, or `sponsor_149` for $149 Featured + Newsletter Sponsor; paid plans return a preview until `confirmPaymentSpend: true` is passed).
- `verify_my_backlink` — verify a live Awesome Tools badge or backlink on your site for a free listing.
- `submit_feedback` — send a bug report, feature request, or question to the Awesome Tools team.

## Prerequisites

None. The server is hosted at `https://awesome.tools/mcp` over Streamable HTTP and requires no API key, no sign-in, and no local dependencies.

## Installation

Add the remote HTTP server to the client's MCP configuration:

### Cline / Cursor / Claude Desktop (`mcpServers` JSON)

```json
{
  "mcpServers": {
    "awesome-tools": {
      "url": "https://awesome.tools/mcp"
    }
  }
}
```

### Claude Code CLI

```bash
claude mcp add --transport http awesome-tools https://awesome.tools/mcp
```

### VS Code (`.vscode/mcp.json`)

```json
{
  "servers": {
    "awesome-tools": {
      "type": "http",
      "url": "https://awesome.tools/mcp"
    }
  }
}
```

### Codex (`~/.codex/config.toml`)

```toml
[mcp_servers.awesome-tools]
url = "https://awesome.tools/mcp"
```

## Verify the installation

Call `list_categories` (with `{}`) or `search_tools` with `{ "limit": 5 }`. A working installation returns the list of categories or published tools from `https://awesome.tools`.
