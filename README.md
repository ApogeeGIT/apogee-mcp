# Apogee MCP server: bulk-launch Meta, TikTok and Snapchat ads from any AI agent

[Apogee](https://apogee.ad) is the ad launcher e-commerce brands and agencies use to ship hundreds of creatives a week on **Meta (Facebook, Instagram), TikTok and Snapchat**. Its remote MCP server lets Claude, ChatGPT, Cursor, Gemini CLI, VS Code, Grok and any MCP client launch and manage those ads, across **every ad account you connected**, the way the Apogee app does: an interview, a full recap, your yes, then the launch.

```
https://app.apogee.ad/mcp
```

Streamable HTTP · OAuth 2.1 (PKCE, dynamic client registration, client ID metadata documents) or an API key · 80 tools, each annotated (`title`, `readOnlyHint`, `destructiveHint`, `openWorldHint`).

## When to use Apogee

- **Many ad accounts, many clients.** One connection reaches every Meta, TikTok and Snapchat ad account connected to your Apogee workspace: switch client by naming the account, no reconnection.
- **Several ad platforms at once.** The same launch interview, the same naming convention and the same recap on Meta, TikTok and Snapchat; performance read per platform, in each account's currency, never summed across platforms.
- **Bulk launches.** A Google Drive folder, a Frame.io project, a Dropbox link or files on your computer become ads in one go: each creative's formats (9:16, 4:5, 1:1) grouped into one ad, your naming convention applied, ad sets built your way (one per concept, all in one, or into existing ad sets).
- **Duplicate with post ID.** Relaunch a winning ad into up to 30 ad sets on the same post, likes and comments kept.
- **Bridge.** Relaunch your best Meta ads on TikTok or Snapchat, or copy them to another Meta ad account.
- **Agencies and teams.** Each teammate connects with their own Apogee login and permissions; every launch is logged in the app's history.

## Safety

- Nothing is created, changed or transferred without your explicit yes to the whole recap: `prepare_launch` → `launch`, an action tool → `execute_action`, `prepare_bridge_transfer` → `bridge_transfer`. A prepared plan expires after 24 hours.
- Ads are created **paused** unless you ask otherwise.
- You choose the scopes when you connect: `read`, `launch`, `actions`. Tools outside them are not listed to the assistant.
- Daily budget caps and launch limits per ad account apply to every call.

## Connect

You need an Apogee account with your ad accounts connected. The MCP comes with the Pro, Growth and Scale plans ([pricing](https://apogee.ad/en/pricing/)).

| Client | How |
|---|---|
| Claude (claude.ai, desktop) | Customize → Connectors → **+ Add** → Add custom connector → `https://app.apogee.ad/mcp` → Sign in now |
| ChatGPT | [chatgpt.com/plugins](https://chatgpt.com/plugins) → **+** → Add custom MCP server → `https://app.apogee.ad/mcp`, OAuth |
| Claude Code | `claude mcp add --transport http apogee https://app.apogee.ad/mcp` |
| Cursor | `~/.cursor/mcp.json`: `{ "mcpServers": { "apogee": { "url": "https://app.apogee.ad/mcp", "headers": { "Authorization": "Bearer apk_…" } } } }` (or OAuth from the desktop app, without `headers`) |
| VS Code (Copilot agent mode) | **MCP: Add Server** → HTTP → `https://app.apogee.ad/mcp` → name it `apogee` |
| Gemini CLI | `gemini mcp add --transport http apogee https://app.apogee.ad/mcp` |
| Grok (grok.com) | grok.com/connectors → New Connector → Custom → `https://app.apogee.ad/mcp` |
| Any other MCP client | Server URL `https://app.apogee.ad/mcp`; OAuth, or `Authorization: Bearer apk_…` with a key from [Settings → API](https://app.apogee.ad/home?settings=api) |

Step-by-step guides for each assistant: [app.apogee.ad/docs/mcp](https://app.apogee.ad/docs/mcp) · for agents: [app.apogee.ad/llms.txt](https://app.apogee.ad/llms.txt).

## Example prompts

- "Launch the new creatives of this Drive folder in my Summer campaign, one ad set per concept, with my naming convention."
- "For each of my clients' ad accounts, which ads spent more than twice the target CPA yesterday? Prepare their pause."
- "Duplicate my 3 best ads of last week into every prospecting ad set of campaign X, keeping their post IDs."
- "Relaunch my top 5 Meta ads of the month on TikTok, in my TikTok testing campaign."
- "Give me yesterday's spend, CPA and ROAS on Meta, TikTok and Snapchat, one platform at a time."

## Tools

### Accounts and structure (every platform)

| Tool | What it does | Effect |
|---|---|---|
| `whoami` | Who am I | Read-only |
| `list_ad_accounts` | List ad accounts | Read-only |
| `list_campaigns` | List campaigns | Read-only |
| `list_adsets` | List ad sets | Read-only |
| `list_ads` | List ads | Read-only |
| `list_pages` | List Facebook pages | Read-only |
| `list_instagram_accounts` | List a page's Instagram accounts | Read-only |
| `list_pixels` | List pixels | Read-only |
| `list_lead_forms` | List instant forms | Read-only |
| `list_custom_audiences` | List custom audiences | Read-only |
| `list_posts` | List posts usable as ads | Read-only |
| `search_targeting` | Search targeting | Read-only |
| `list_targeting` | List TikTok / Snapchat targeting | Read-only |
| `list_tiktok_posts` | List TikTok posts (Spark Ads) | Read-only |
| `list_tiktok_music` | List TikTok music (carousels) | Read-only |
| `list_platform_templates` | List Quick Bulk Edit templates | Read-only |
| `get_templates` | Show what a copy would take | Read-only |
| `get_latest_in_campaign` | Latest ad set and ad of a campaign | Read-only |

### Creatives in (Drive, Frame.io, Dropbox, your computer)

| Tool | What it does | Effect |
|---|---|---|
| `import_link` | Import creatives from a link | Prepares (nothing live) |
| `import_status` | Follow an import | Read-only |
| `list_drive_folder` | List a Google Drive folder | Read-only |
| `get_upload_urls` | Get upload URLs | Prepares (nothing live) |
| `confirm_uploads` | Check uploaded files | Read-only |

### Bulk launch (Meta, TikTok, Snapchat)

| Tool | What it does | Effect |
|---|---|---|
| `get_launch_questions` | Launch interview | Read-only |
| `prepare_launch` | Prepare a launch | Prepares (nothing live) |
| `launch` | Launch a prepared plan | Changes (after your yes) |
| `launch_status` | Follow a launch | Read-only |
| `list_launches` | List launches | Read-only |
| `create_campaign` | Prepare a new campaign | Prepares (nothing live) |

### Meta performance

| Tool | What it does | Effect |
|---|---|---|
| `get_account_overview` | Ad account performance overview | Read-only |
| `get_campaigns` | Campaign performance | Read-only |
| `get_adsets` | Ad set performance | Read-only |
| `get_ads` | Ad performance | Read-only |
| `get_top_performers` | Best and worst ads | Read-only |
| `get_daily_breakdown` | Performance per day | Read-only |
| `get_ad_creatives` | Ads' creatives and texts | Read-only |
| `get_audience_insights` | Audience insights | Read-only |
| `get_account_spend_limit` | Ad account spend limit | Read-only |
| `get_campaign_budget_optimization` | Campaign budget settings (CBO) | Read-only |
| `get_ad_performance_by_placement` | Performance by placement | Read-only |
| `get_ad_performance_by_age_gender` | Performance by age and gender | Read-only |
| `get_ad_performance_by_device` | Performance by device | Read-only |
| `get_creative_fatigue_metrics` | Creative fatigue | Read-only |
| `get_video_metrics` | Video hook and hold rates | Read-only |

### TikTok and Snapchat performance

| Tool | What it does | Effect |
|---|---|---|
| `get_platform_overview` | TikTok / Snapchat account overview | Read-only |
| `get_platform_performance` | TikTok / Snapchat performance by campaign, ad set or ad | Read-only |
| `get_platform_daily_breakdown` | TikTok / Snapchat daily breakdown | Read-only |
| `get_platform_top_performers` | TikTok / Snapchat top and worst performers | Read-only |

### Changes, prepared then confirmed

| Tool | What it does | Effect |
|---|---|---|
| `pause_ad` | Prepare to pause ads | Prepares (nothing live) |
| `pause_adset` | Prepare to pause ad sets | Prepares (nothing live) |
| `activate_ad` | Prepare to activate ads | Prepares (nothing live) |
| `activate_adset` | Prepare to activate ad sets | Prepares (nothing live) |
| `update_budget` | Prepare a budget change | Prepares (nothing live) |
| `scale_budget` | Prepare to scale budgets by a percentage | Prepares (nothing live) |
| `duplicate_ad` | Prepare to duplicate an ad (post kept) | Prepares (nothing live) |
| `duplicate_adset` | Prepare to duplicate an ad set | Prepares (nothing live) |
| `duplicate_campaign` | Prepare to duplicate a campaign | Prepares (nothing live) |
| `create_adset` | Prepare a new ad set | Prepares (nothing live) |
| `create_ad` | Prepare a new ad | Prepares (nothing live) |
| `create_ad_from_post` | Prepare an ad from an existing post | Prepares (nothing live) |
| `update_adset_targeting` | Prepare a targeting change | Prepares (nothing live) |
| `update_campaign_status` | Prepare to pause or activate a campaign | Prepares (nothing live) |
| `set_platform_status` | Prepare a TikTok / Snapchat pause or activation | Prepares (nothing live) |
| `set_platform_daily_budget` | Prepare a TikTok / Snapchat daily budget change | Prepares (nothing live) |
| `execute_action` | Run a prepared action | Changes (after your yes) |

### Bridge: relaunch winners on another platform or ad account

| Tool | What it does | Effect |
|---|---|---|
| `prepare_bridge_transfer` | Prepare a Bridge transfer | Prepares (nothing live) |
| `bridge_transfer` | Run a prepared Bridge transfer | Changes (after your yes) |
| `bridge_transfer_status` | Follow a Bridge transfer | Read-only |
| `list_bridge_transfers` | List the ads already bridged | Read-only |
| `get_bridge_stats` | Bridge stats per creative | Read-only |
| `get_bridge_daily_stats` | Bridge stats per day | Read-only |

### Brand and creative research

| Tool | What it does | Effect |
|---|---|---|
| `get_business_profile` | Business profile | Read-only |
| `update_business_profile` | Update the business profile | Changes (after your yes) |
| `fetch_website_content` | Summarize the brand's website | Read-only |
| `fetch_ad_comments` | Raw ad comments | Read-only |
| `trigger_comment_sync` | Sync ad comments | Prepares (nothing live) |
| `fetch_customer_reviews` | Customer reviews | Read-only |
| `search_reddit` | Search Reddit | Read-only |
| `search_meta_ad_library` | Search the Meta Ad Library | Read-only |
| `load_reference` | Load an audit reference | Read-only |

## Discovery endpoints

- Protected resource metadata: `https://app.apogee.ad/.well-known/oauth-protected-resource/mcp`
- Authorization server metadata: `https://app.apogee.ad/.well-known/oauth-authorization-server`
- Registry entry: `ad.apogee/apogee` ([server.json](server.json))

## Links

[Website](https://apogee.ad) · [MCP docs](https://apogee.ad/developers/mcp) · [REST API](https://app.apogee.ad/docs/api) · [Privacy](https://apogee.ad/en/legal/privacy/) · [Terms](https://apogee.ad/en/legal/terms/) · Support: hello@apogee.ad

This repository documents the hosted server; the server itself runs at Apogee and is not open source.
