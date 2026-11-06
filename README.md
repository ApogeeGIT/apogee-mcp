# Apogee MCP Server: bulk ads for Meta, TikTok & Snapchat

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=apogee&config=eyJ1cmwiOiJodHRwczovL2FwcC5hcG9nZWUuYWQvbWNwIn0%3D)

[Apogee](https://www.apogee.ad) is a bulk ad launcher for agencies and performance teams. This repository documents Apogee's **remote MCP server**, which lets AI agents (Claude, ChatGPT, Cursor, VS Code, Gemini CLI, Grok, Cline…) launch, manage and analyze ads across many **Meta (Facebook/Instagram), TikTok and Snapchat** ad accounts.

> Remote server, nothing to install. Endpoint: `https://app.apogee.ad/mcp` · Transport: Streamable HTTP · Auth: OAuth 2.1 (PKCE) or API key

## What your agent can do
- **Bulk launch:** creatives from Google Drive or uploads → campaigns, ad sets and ads in one plan
- **Multi-account / multi-platform:** every connected ad account across Meta, TikTok and Snapchat; copy ads from one Meta ad account to another, or relaunch Meta winners on TikTok and Snapchat
- **Manage:** duplicate, pause or resume, change budgets, launch from existing posts (incl. TikTok Spark Ads), search targeting and audiences
- **Analyze:** insights by date range, rankings by metric, creative fatigue
- **Safe:** scopes `read` / `launch` / `actions`; every launch or change is prepared first and runs only after your explicit yes (each plan runs once); ads created paused by default; budget caps

80 tools in total. Full reference: https://www.apogee.ad/developers/mcp/ · LLM-friendly docs: https://www.apogee.ad/developers/llms.txt

## Connect

**Claude (claude.ai / Desktop):** Customize → Connectors → + Add → Add custom connector → `https://app.apogee.ad/mcp` → sign in with Apogee.

**Claude Code**
```bash
claude mcp add --transport http apogee https://app.apogee.ad/mcp
```

**Cursor / Cline** (`mcp.json`), or click *Add to Cursor* above
```json
{
  "mcpServers": {
    "apogee": { "url": "https://app.apogee.ad/mcp" }
  }
}
```
The same config is in this repository's [`.mcp.json`](.mcp.json), so Claude Code and other clients that read a project `.mcp.json` pick it up when you open this repository.

**VS Code** (`.vscode/mcp.json`)
```json
{
  "servers": {
    "apogee": { "type": "http", "url": "https://app.apogee.ad/mcp" }
  }
}
```

**With an API key** (clients without OAuth): create a key in Apogee, Settings → API, and send it as `Authorization: Bearer apk_…`. See the [docs](https://www.apogee.ad/developers/mcp/).

## Example prompts
- "Launch these 12 UGC videos from my Google Drive folder as a new Meta campaign on the Acme ad account, €50/day."
- "List all my ad accounts on Meta, TikTok and Snapchat with yesterday's spend and ROAS."
- "Copy my 3 best Meta ads of last week to the Client B ad account."
- "Pause every Meta ad set with ROAS under 1.5 over the last 7 days across all clients."
- "Which creatives are showing fatigue this month?"

## For agents and directories
- [`server.json`](server.json): the entry published in the official MCP Registry as `ad.apogee/apogee`
- Server card: https://app.apogee.ad/.well-known/mcp/server-card.json
- OAuth metadata: https://app.apogee.ad/.well-known/oauth-protected-resource/mcp
- [`llms-install.md`](llms-install.md): setup steps for agents such as Cline
- llms.txt: https://www.apogee.ad/developers/llms.txt
- Docs: https://www.apogee.ad/developers/mcp/

## Requirements
An Apogee account on the **Pro plan or above** (MCP and API access), with at least one Meta, TikTok or Snapchat ad account connected.

## REST API
The same features are available over REST: `https://api.apogee.ad/api/v1` ([OpenAPI](https://api.apogee.ad/api/v1/openapi.json)), with an `Idempotency-Key` header on writes.

## Support
hello@apogee.ad · APOGEE SAS, Boulogne-Billancourt, France
