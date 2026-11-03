# Installing the Apogee MCP server (for AI agents such as Cline)

Apogee is a **remote** MCP server: there is nothing to install or build.

- Server URL: `https://app.apogee.ad/mcp`
- Transport: Streamable HTTP (every call is a `POST` answered with JSON; no SSE stream)
- Authentication, one of:
  1. **OAuth 2.1** (preferred): add the server with no headers; the client discovers sign-in from `https://app.apogee.ad/.well-known/oauth-protected-resource/mcp` and opens Apogee's consent page.
  2. **API key**: the user creates a key in Apogee, Settings → API (https://app.apogee.ad/home?settings=api), with only the scopes needed (`read`, `launch`, `actions`). Send it as `Authorization: Bearer apk_…`. Never commit the key to a shared project file.

## Configuration

OAuth:

```json
{
  "mcpServers": {
    "apogee": {
      "type": "streamableHttp",
      "url": "https://app.apogee.ad/mcp"
    }
  }
}
```

API key:

```json
{
  "mcpServers": {
    "apogee": {
      "type": "streamableHttp",
      "url": "https://app.apogee.ad/mcp",
      "headers": { "Authorization": "Bearer apk_YOUR_KEY" }
    }
  }
}
```

## Check

Call `whoami`: it returns the Apogee account, the credential and its scopes. Then `list_ad_accounts` lists the connected Meta ad accounts (`platform: "tiktok"` or `"snapchat"` for the others).

## Requirements

An Apogee account on the Pro plan or above, with at least one Meta, TikTok or Snapchat ad account connected. Docs: https://www.apogee.ad/developers/mcp/ · Support: hello@apogee.ad
