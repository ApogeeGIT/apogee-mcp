# Apogee

Apogee launches and manages Meta (Facebook, Instagram), TikTok and Snapchat ads across every ad account the user connected to Apogee. The first call opens Apogee's sign-in (OAuth): run `/mcp auth apogee` if Gemini CLI asks.

- Nothing is created, changed or transferred without the user's explicit yes to the whole recap: `prepare_launch` → `launch`, an action tool → `execute_action`, `prepare_bridge_transfer` → `bridge_transfer`.
- Ask the open questions one topic at a time, with the choices the tools return. Never answer for the user.
- Ads are created paused unless the user asks otherwise.
- `platform`: "meta" (default), "tiktok" or "snapchat". Never add numbers up across platforms.
- Start a launch with `list_ad_accounts`, then `get_launch_questions`.

Docs: https://www.apogee.ad/developers/mcp/
