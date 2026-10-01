<div align="center">
  <h1>Journely MCP Server</h1>
  <p><strong>Free MCP server for Vietnamese, Japanese, and US market data.</strong></p>
  <p>9 tools · REST + MCP parity · OpenAPI 3.1 documented · broker-neutral · live data</p>
  <br/>
  <p>
    <a href="https://journely.me/api-docs"><img alt="docs" src="https://img.shields.io/badge/docs-OpenAPI%203.1-blue" /></a>
    <a href="https://journely.me/api-docs/mcp"><img alt="MCP" src="https://img.shields.io/badge/MCP-Streamable%20HTTP-purple" /></a>
    <img alt="License" src="https://img.shields.io/badge/license-MIT-green" />
    <img alt="Markets" src="https://img.shields.io/badge/markets-VN%20%C2%B7%20JP%20%C2%B7%20US-orange" />
  </p>
</div>

---

> **⚠️ Not investment advice.** This server returns market data for research and AI-agent use. Outputs are data, not recommendations. You are responsible for verifying any analysis and for compliance with the rules of the markets and jurisdictions you operate in.

---

## What it is

[Journely](https://journely.me) operates a public, free-tier MCP server (Model Context Protocol, [spec 2025-06-18](https://modelcontextprotocol.io/)) that gives AI agents structured access to **Vietnamese, Japanese, and US market data** — macro indicators and forecasts, an economic calendar, sector aggregates, and per-stock fundamentals, analyst estimates and price history.

Every MCP tool is also a REST endpoint with the same data model. So you can:
- Wire it into Claude Desktop, Cursor, or any MCP-capable client → ask natural-language questions
- Call it directly from any HTTP client → drop into your own AI pipeline, notebook, or app

This repository is the public-facing landing for the server. **The MCP server itself runs at `https://api.journely.me/api/v1/journely/mcp`** — there's nothing to install or self-host.

## Why it exists

In 2026, every "Top MCP servers for financial data" roundup covers the same US-first providers (EODHD, Finnhub, Financial Modeling Prep, Alpha Vantage, MarketXLS, Financial Datasets). Vietnamese market coverage is thin or paid-only; broker-tied servers exist but lock you to one execution venue. Journely is **broker-neutral**, multi-market, and free at the tier most indie and research workloads need.

## Quick start

### Option 1 — Claude Desktop (MCP)

Add the server to `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "journely": {
      "url": "https://api.journely.me/api/v1/journely/mcp",
      "headers": {
        "Authorization": "Bearer jrn_live_YOUR_TOKEN"
      }
    }
  }
}
```

Get a free token at https://journely.me/settings/api-keys. Restart Claude Desktop. All 9 tools will appear and Claude can call them automatically.

Try a prompt:
> *"Pull VIC's last 5 years of revenue and margins, then check where Vietnamese inflation and rates are heading."*

### Option 2 — cURL (REST)

```bash
export JOURNELY_TOKEN="your-token-here"

# Vietnam macro indicators
curl -H "Authorization: Bearer $JOURNELY_TOKEN" \
  "https://api.journely.me/api/v1/journely/data/macro/indicators?country=VN"

# VIC (Vingroup) snapshot + quote
curl -H "Authorization: Bearer $JOURNELY_TOKEN" \
  "https://api.journely.me/api/v1/journely/data/stocks/VIC/overview?country=VN"

# VIC income statement (annual)
curl -H "Authorization: Bearer $JOURNELY_TOKEN" \
  "https://api.journely.me/api/v1/journely/data/stocks/VIC/statements?country=VN&type=income"
```

### Option 3 — Python (or any HTTP client)

```python
import httpx

client = httpx.Client(
    base_url="https://api.journely.me/api/v1/journely",
    headers={"Authorization": f"Bearer {TOKEN}"},
)

# Sector snapshot (broad-market, not country-split): P/E, margin, 1Y change
r = client.get("/data/sectors", params={"level": "sector"})
print(r.json())
```

## Tools

All 9 tools are exposed via both MCP and REST. One-to-one parity, same data model.

| MCP tool | REST endpoint | Returns |
|---|---|---|
| `get_macro_indicators` | `GET /data/macro/indicators` | GDP, inflation, labor, rates panel for US / JP / VN |
| `get_macro_forecast` | `GET /data/macro/forecast` | Forward-looking macro projections (4–8 quarters) |
| `get_macro_calendar` | `GET /data/macro/calendar` | Upcoming economic events (FOMC, CPI, NFP, GDP) with previous / forecast / actual |
| `get_sector_overview` | `GET /data/sectors` | Sector (11) or industry (145) snapshot — P/E, margin, dividend yield, 1D/1Y change. Broad-market, not country-split |
| `get_stock_overview` | `GET /data/stocks/{symbol}/overview` | Company snapshot + live quote — any US / JP / VN ticker |
| `get_stock_statements` | `GET /data/stocks/{symbol}/statements` | Income, balance sheet, cash flow, or ratios (ROIC, FCF yield, EV/EBIT) — annual or quarterly |
| `get_stock_forecast` | `GET /data/stocks/{symbol}/forecast` | Analyst consensus, price targets, rating trend |
| `get_stock_price_history` | `GET /data/stocks/{symbol}/history` | Closing prices — full daily for US; ~1Y daily + long-horizon snapshot for JP / VN |
| `get_earnings_calendar` | `GET /data/earnings-calendar` | Upcoming earnings dates + EPS / revenue estimates for a list of US tickers |

There is no ticker-search tool — pass any US / JP / VN symbol you already know (e.g. `AAPL`, `7203`, `FPT`).

Full OpenAPI 3.1 spec with interactive ReDoc UI: **https://journely.me/api-docs**
MCP transport details and tool schemas: **https://journely.me/api-docs/mcp**

## Pricing

Free tier with reasonable rate limits — designed for indie developers, research, and most agent workloads.

| Tier | Price | Rate limit | Notes |
|---|---|---|---|
| **Free** | $0 | 100 / day · 30 / hour | 1 key |
| Pro | see [pricing](https://journely.me/pricing) | 5,000 / day · 500 / hour | 5 keys |
| Max | see [pricing](https://journely.me/pricing) | 50,000 / day · 5,000 / hour | 20 keys |

Only `tools/call` counts against quota — `initialize`, `tools/list` and `ping` are free.

No card required to get a free key. No marketing emails after signup.

## Good for

- AI agents that need Vietnamese / Japanese / US market context
- Backtesting and analytics on VN-listed equities
- LLM-driven investment research workflows (Claude, GPT, Gemini all supported via MCP or REST)
- Vietnamese-diaspora investors building personal tooling
- Anyone learning to invest who wants real data behind their AI prompts

## Not for

- **Order execution.** No trading, positions, or orders endpoints — research data only.
- **HFT.** Pricing is updated frequently enough for fundamental and research workflows, not for millisecond strategies.
- **Investment advice.** Outputs are data, not recommendations.

## How it compares

| | Journely | Existing free libraries (vnstock, VNQuant) | Paid VN APIs (iTick, FiinGroup, EODHD-VN) | Broker MCP servers |
|---|---|---|---|---|
| **Free tier** | ✓ | ✓ | Limited | Usually tied to brokerage account |
| **MCP-native** | ✓ | ✗ (Python only) | ✗ | Sometimes |
| **REST API** | ✓ | ✗ | ✓ | Sometimes |
| **Multi-market** | VN + JP + US | Mostly VN | Mostly VN | Single broker's venues |
| **Broker-neutral** | ✓ | ✓ | ✓ | ✗ (locked to provider) |
| **OpenAPI documented** | ✓ | ✗ | Varies | Varies |

## Status

| | |
|---|---|
| **MCP transport** | Streamable HTTP (spec 2025-06-18), stateless |
| **Auth** | Bearer token (`jrn_live_…`), or OAuth 2.1 + PKCE for clients that support remote-connector sign-in (discovery at `/.well-known/oauth-protected-resource`) |
| **Server** | Live at `https://api.journely.me/api/v1/journely/mcp` |
| **Region** | Asia-Pacific (low-latency for VN/JP users; ~150-300ms US round-trip) |
| **Uptime target** | Best-effort; this is a community-free service. SLA available for paid tiers. |

## Feedback and contributions

This is a docs-and-examples repository for a hosted service. The MCP server itself isn't open-source (yet). To contribute:

- **Bugs or wrong data**: open a GitHub issue with the exact tool call and what you expected
- **Tool requests**: open an issue, tag `enhancement`
- **Built something cool with it**: PR a link to the `examples/` directory or DM [@journely](https://x.com/journely) on X

## Disclaimer

Nothing in this repository or the data returned by the Journely MCP server constitutes investment, legal, tax, or accounting advice. Data is provided as-is, on a best-effort basis. Markets move; data feeds occasionally lag or correct. **Verify before you act.**

## License

[MIT](./LICENSE) for this repository's contents (README, examples). The Journely service itself is governed by its [Terms of Service](https://journely.me/legal/terms).

---

**Built by [Trung Vu](https://journely.me) — Tokyo. Vietnamese. FIRE'd. Indie founder.**
Reach out: `hello@journely.me` · `journely.me` · [X / Twitter](https://x.com/journely)
