<p align="center"><img src="logo.png" alt="SecurePutCalls" width="120" /></p>

# SecurePutCalls MCP Server

Wheel strategy research for options income traders, inside Claude, ChatGPT, Cursor, VS Code and any other MCP client. Find cash-secured put and covered call candidates, check a ticker's risk before selling, read today's conditions for selling options, and analyze any short put or covered call (even one at your broker) with roll candidates.

**Read-only.** SecurePutCalls never places trades. Educational information, not investment advice.

- **Server URL:** `https://secureputcalls.com/mcp` (Streamable HTTP)
- **Sign-in:** OAuth 2.0 with your SecurePutCalls account (free plan available), or a Pro API key as a Bearer token
- **Website:** https://secureputcalls.com/claude-connector
- **Server card:** https://secureputcalls.com/.well-known/mcp/server-card.json

## Tools

| Tool | What it returns |
|---|---|
| `get_wheel_candidates` | Cash-secured puts and covered calls from the Wheel Screener's weekday scan: strike, expiration, cushion, capital, annual return, delta, liquidity, a 0-100 wheel score, and earnings before expiry. Filter by capital, DTE, sector, score, or "no earnings before expiry". |
| `get_symbol_risk` | One ticker's best puts and calls, tail-risk scores, and (in market hours) liquidity, gamma and short-squeeze metrics. |
| `get_market_conditions` | Today's conditions for selling options: favorable / caution / avoid, from SPY implied volatility, term structure, expected weekly move and put/call ratio. |
| `analyze_option_position` | Any short put or covered call you describe: cushion, cost to close, delta, profit captured, earnings before expiry, a take-profit / let-expire / roll read, and up to 5 roll candidates that never move to a riskier strike. |
| `get_roll_suggestions` | Your tracked positions expiring soon, each with the same analysis and roll candidates (Premium and Pro). |
| `get_my_positions` | Your tracked positions with live cushion, risk level and earnings before expiry. |
| `get_weekly_picks` | Your Weekly Picks paper trades and their results. |

## Plans

| Plan | Daily tool calls | Notes |
|---|---|---|
| Free | 20 | Top 5 candidates, 3 Weekly Picks, position analysis |
| Premium | 100 | Full screener filters, roll suggestions |
| Pro | Unlimited | Everything, plus the REST API |

See https://secureputcalls.com/pricing.

## Connect

**Claude (claude.ai / Desktop):** Settings → Connectors → find **SecurePutCalls** in the directory, or *Add custom connector* with `https://secureputcalls.com/mcp`.

**Claude Code:**
```bash
claude mcp add --transport http securePutCalls https://secureputcalls.com/mcp
```

**Cursor / Windsurf / VS Code / Cline (mcp.json):**
```json
{
  "mcpServers": {
    "securePutCalls": { "url": "https://secureputcalls.com/mcp" }
  }
}
```
Your client opens a browser window to sign in the first time.

**ChatGPT, Le Chat, Perplexity and other clients:** add a custom MCP connector with the URL above.

## Try asking

- "Which cash-secured puts expiring next week have no earnings before expiry?"
- "Check the risk on NVDA before I sell a put."
- "I'm short the AAPL 330 put expiring Oct 16, sold for $2.50. Take profit, let it expire or roll?"
- "Is this a good week to sell puts?"

## Support

- Docs: https://secureputcalls.com/developer-docs
- Support: pritima@secureputcalls.com
- Privacy: https://secureputcalls.com/privacy

## License

The files in this repository are MIT licensed (see [LICENSE](LICENSE)). The SecurePutCalls
name and logo are trademarks of SecurePutCalls LLC and aren't covered by that license; use of
the hosted service is governed by the [Terms of Service](https://secureputcalls.com/terms).
