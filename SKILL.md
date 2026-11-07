---
name: awesome-tools
description: Search curated SaaS and AI tools on Awesome Tools, inspect categories and tags, submit a product for a free DR 20+ backlink listing or a paid Featured Launch, verify backlink badges, and send feedback with the Awesome Tools MCP server.
---

# Use the Awesome Tools MCP Server

Awesome Tools is a curated software and AI tools directory with a remote Streamable HTTP MCP server at `https://awesome.tools/mcp`. No API key or sign-in is required.

## Step 1. Check that the server is connected

Look for these 7 tools (your client may prefix them, for example `mcp__awesome-tools__search_tools`):

- `search_tools`
- `get_tool`
- `list_categories`
- `list_tags`
- `submit_tool`
- `verify_my_backlink`
- `submit_feedback`

If they are not available, tell the user how to add the remote server:

- **Claude Code:** `claude mcp add --transport http awesome-tools https://awesome.tools/mcp`
- **Cursor / Claude Desktop:** Add remote MCP server URL `https://awesome.tools/mcp` (no authentication required).

## Step 2. Discovering and researching tools

1. Call `list_categories` or `list_tags` to see available taxonomy slugs and published tool counts.
2. Call `search_tools` with `query`, `category`, `tag`, `isFeatured`, and `limit` (1–50, default 20) to find published tools.
3. Call `get_tool` with `slug` to read full details for a tool or check the status and eligibility of a pending submission.

## Step 3. Submitting a SaaS or AI tool

Only submit a product when the user has authorized you to submit their website and contact email.

1. Call `list_categories` first and pick 1 to 3 matching category slugs.
2. Choose the `plan`:
   - `free_backlink`: Free for custom domains with Domain Rating 20+ that place a visible Awesome Tools badge or link on their homepage (or a page linked from the homepage). Saves the draft listing, screens the domain, and returns the badge HTML snippet.
   - `featured_49`: $49 one-time Featured Launch (permanent listing, dofollow link, featured placement, no backlink required).
   - `sponsor_149`: $149 one-time Featured + Newsletter Sponsor (everything in `featured_49` plus a Sponsored Pick slot in the Awesome Tools Newsletter and 30 days pinned in category top picks).
3. **Never confirm paid spend without asking first:**
   - For `featured_49` or `sponsor_149`, call `submit_tool` with `confirmPaymentSpend: false` (or omit it) first. This returns a side-effect-free price preview (`status: "preview"`, `amountUsd`, `benefits`).
   - Show the user the exact price and plan benefits and ask for confirmation.
   - Only after the user approves the spend, call `submit_tool` again with the same fields and `confirmPaymentSpend: true` to get the `checkoutUrl` (Stripe Checkout). Give the user the `checkoutUrl` so they can pay in their browser.
4. **Completing a free backlink listing:**
   - After submitting with `plan: "free_backlink"`, place the returned badge HTML (`backlink.badgeHtml`, `backlink.badgeHtmlDark`, or `backlink.textLinkHtml`) on the product's homepage or a page linked from the homepage.
   - Call `verify_my_backlink` with `{ "slug": "<tool-slug>", "backlinkUrl": "https://..." }`. Once verified on an eligible domain, the listing is scheduled for publication.

## Step 4. Sending feedback

Use `submit_feedback` with `category` (`"bug"`, `"missing_feature"`, `"question"`, or `"other"`), `message`, and optional `slug` to contact the Awesome Tools team (`sales@awesome.tools` / `https://awesome.tools/submit`).
