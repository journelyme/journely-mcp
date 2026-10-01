# Examples

Drop-in configurations and sample prompts for using the Journely MCP server.

## Files

- **`claude_desktop_config.json`** — Minimal Claude Desktop config snippet. Copy the `mcpServers` block into your existing config at `~/Library/Application Support/Claude/claude_desktop_config.json`. Replace `YOUR_TOKEN` with a free token from [journely.me/settings/api-keys](https://journely.me/settings/api-keys).

## Example prompts (Claude Desktop)

Once the MCP server is wired up, try these prompts to see how Claude orchestrates the 9 tools.

### Macro + sector synthesis (combines `get_macro_indicators` + `get_macro_forecast` + `get_sector_overview`)
> *"What does the Vietnamese macro picture look like right now, where are rates heading, and which sectors look cheapest on P/E? Use real data."*

### Single-stock deep dive (combines `get_stock_overview` + `get_stock_statements` + `get_stock_price_history`)
> *"Give me a full update on VIC — 5-year revenue and margin trend, cash flow, where the price sits vs its 1-year range, and any near-term macro catalysts."*

### Peer comparison (combines `get_stock_overview` + `get_stock_statements` with `type=ratios`)
> *"Compare FPT, CMG and ELC on ROE, ROIC and EV/EBIT over the last 5 years. Which one is compounding fastest?"*

### Earnings watchlist (uses `get_earnings_calendar` + `get_stock_forecast`)
> *"When do AAPL, MSFT and NVDA report next, and what EPS is the street expecting?"*

### Macro calendar planning (uses `get_macro_calendar`)
> *"What Vietnamese macro releases are scheduled this week, and which ones typically move the VN-Index?"*

## Contributing your own examples

If you build something useful, open a PR adding to this directory:
- A description of the use case
- The prompt(s) or code that worked
- (Optional) a screenshot or transcript

Single-file additions in any language welcome — Python, TypeScript, shell, whatever fits.
