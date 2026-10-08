# Installing the SecurePutCalls MCP server (instructions for AI agents)

SecurePutCalls is a **remote** MCP server. There is nothing to download, build or run locally.

1. Add this server to the client's MCP configuration:
   ```json
   {
     "mcpServers": {
       "securePutCalls": {
         "url": "https://secureputcalls.com/mcp"
       }
     }
   }
   ```
   - Transport: Streamable HTTP. Clients that need an explicit type use `"type": "streamableHttp"` (or `"http"`).
   - Claude Code: `claude mcp add --transport http securePutCalls https://secureputcalls.com/mcp`
2. Do **not** add an API key or environment variables. The first call returns HTTP 401 with OAuth discovery metadata; the client then opens a browser window where the user signs in to (or creates) a free SecurePutCalls account and approves access.
   - Advanced: users with a Pro plan can instead send `Authorization: Bearer sk_live_...` (created in SecurePutCalls → Settings → Developer API & Webhooks).
3. Verify by listing tools. Expect: `get_wheel_candidates`, `get_symbol_risk`, `get_market_conditions`, `analyze_option_position`, `get_roll_suggestions`, `get_my_positions`, `get_weekly_picks`.
4. Test with a call that needs no saved data, for example `get_market_conditions` with no arguments.

Notes for the agent:
- All tools are read-only. SecurePutCalls never places trades; trading happens only in the user's own broker.
- Responses include data timestamps (`scannedAt`, `asOf`) and risk flags. Surface them to the user, and treat null risk values as "unavailable", not zero risk.
- Each account has a daily tool-call allowance (Free 20, Premium 100, Pro unlimited). A plan or quota message is not an installation error.
