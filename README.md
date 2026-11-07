# Awesome Tools MCP Server: Search Curated SaaS & AI Tools and Submit Your Product

Connect Claude Code, Cursor, Claude Desktop, VS Code, Codex, or any MCP client to [Awesome Tools](https://awesome.tools) over Streamable HTTP. Search curated software and AI tools, browse categories and tags, submit your own product for a free dofollow backlink (DR 20+) or a Featured Launch, verify your backlink badge, and send feedback. No API key or sign-in is required.

```bash
claude mcp add --transport http awesome-tools https://awesome.tools/mcp
```

This repository contains the setup manifests and agent skill for the hosted Awesome Tools MCP server at `https://awesome.tools/mcp`.

## Add it

The hosted server uses Streamable HTTP and requires no API key, no account, and no local installation.

### Claude Code

```bash
claude mcp add --transport http awesome-tools https://awesome.tools/mcp
```

Run `/mcp` inside Claude Code to verify the connection and inspect the available tools.

### Cursor

Add this to `~/.cursor/mcp.json` or `.cursor/mcp.json` inside your project:

```json
{
  "mcpServers": {
    "awesome-tools": {
      "url": "https://awesome.tools/mcp"
    }
  }
}
```

### Claude Desktop and claude.ai

Open **Customize** → **Connectors** → **+ Add** → **Add custom connector**:

- **Name:** `Awesome Tools`
- **URL:** `https://awesome.tools/mcp`
- **Authentication:** **No sign in**

### VS Code

Add this to `.vscode/mcp.json` (VS Code uses `servers`, not `mcpServers`):

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

### Codex

Add this to `~/.codex/config.toml`:

```toml
[mcp_servers.awesome-tools]
url = "https://awesome.tools/mcp"
```

### Claude Code plugin (server + skill together)

This repository is also a Claude Code plugin marketplace:

```bash
claude plugin marketplace add Illyism/awesome-tools-mcp
claude plugin install awesome-tools@awesome-tools-mcp
```

Or install the standalone agent skill in any compatible agent:

```bash
npx skills add Illyism/awesome-tools-mcp
```

## Tools

| Tool | What it does |
| --- | --- |
| `search_tools` | Search published SaaS and AI tools on Awesome Tools by `query`, `category`, `tag`, `isFeatured`, and `limit` (default 20, max 50). |
| `get_tool` | Get a tool by `slug`. Returns full public details for published tools, or submission status, DR eligibility, and next steps for unpublished submissions. |
| `list_categories` | List all directory categories with their `slug` and published tool count. Use these slugs when calling `submit_tool`. |
| `list_tags` | List all directory tags with their `slug` and published tool count. |
| `submit_tool` | Submit your own SaaS or AI tool (`free_backlink` for DR 20+ sites with a reciprocal badge, `featured_49` for $49 Featured Launch without a backlink, or `sponsor_149` for $149 Featured + Newsletter Sponsor). Paid plans always return a price preview first until `confirmPaymentSpend: true` is passed after requester approval, which returns a Stripe Checkout URL. |
| `verify_my_backlink` | Check that the Awesome Tools badge or link is live on your site (`slug` and optional `backlinkUrl`) for an unpublished free listing and schedule publication once verified. |
| `submit_feedback` | Send a `bug`, `missing_feature`, `question`, or `other` message to the Awesome Tools team (optionally referencing a tool `slug`). |

## How tool submission works

1. **Discover categories:** Call `list_categories` to pick 1 to 3 relevant category slugs.
2. **Choose a plan:**
   - `free_backlink`: Free for custom domains with Domain Rating 20+ that place a visible Awesome Tools badge or link on their homepage (or a page linked from the homepage). Returns the HTML/SVG badge snippet and instructions.
   - `featured_49`: $49 one-time Featured Launch. Skips the backlink requirement and includes a permanent listing, a dofollow link, and featured placement.
   - `sponsor_149`: $149 one-time Featured + Newsletter Sponsor. Includes everything in Featured Launch plus a Sponsored Pick slot in the Awesome Tools Newsletter and 30 days pinned in category top picks.
3. **Preview before spending:** Calling `submit_tool` with a paid plan and `confirmPaymentSpend: false` (default) returns the price and benefits without saving a listing or sending any email. After the user approves the spend, call `submit_tool` again with `confirmPaymentSpend: true` to receive a Stripe Checkout URL. No payment ever happens inside MCP; the user completes payment on Stripe.
4. **Verify free backlinks:** After placing the badge HTML on your site for a `free_backlink` submission, call `verify_my_backlink` with your tool `slug` and `backlinkUrl`.

## Links

- **Website:** [https://awesome.tools](https://awesome.tools)
- **Submit a tool:** [https://awesome.tools/submit](https://awesome.tools/submit)
- **Agent skill (`SKILL.md`):** [https://awesome.tools/SKILL.md](https://awesome.tools/SKILL.md)
- **LLM index (`llms.txt`):** [https://awesome.tools/llms.txt](https://awesome.tools/llms.txt)
- **MCP discovery manifest:** [https://awesome.tools/.well-known/mcp](https://awesome.tools/.well-known/mcp)
- **Support:** [https://awesome.tools/submit](https://awesome.tools/submit) or `sales@awesome.tools`
