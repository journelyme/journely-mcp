# Examples

Drop-in configurations and sample prompts for using the Journely MCP server.

## Files

- **`claude_desktop_config.json`** — Minimal Claude Desktop config snippet. Copy the `mcpServers` block into your existing config at `~/Library/Application Support/Claude/claude_desktop_config.json`. Replace `YOUR_TOKEN` with a free token from [journely.me/settings/api-keys](https://journely.me/settings/api-keys).

## Example prompts (Claude Desktop)

Once the MCP server is wired up, try these prompts to see how Claude orchestrates the 9 tools.

### Macro + sector synthesis (combines `get_macro_indicators` + `get_sectors`)
> *"What does the Vietnamese macro picture look like for Q2 2026, and which sectors are most exposed to the interest-rate environment? Use real data."*

### Single-stock deep dive (combines `get_stock_overview` + `get_stock_statements` + `get_stock_technicals`)
> *"Give me a full update on VIC after Q4 2025 earnings — fundamentals, recent technicals, and any near-term macro catalysts."*

### Sector-relative analysis (combines `get_sectors` + `list_symbols` + `get_stock_overview`)
> *"Find the three most profitable Vietnamese real estate companies by ROE and tell me which one is currently trading at the steepest discount to the sector P/E."*

### Macro calendar planning (uses `get_macro_calendar`)
> *"What Vietnamese macro releases are scheduled this week, and which ones typically move the VN-Index?"*

## Contributing your own examples

If you build something useful, open a PR adding to this directory:
- A description of the use case
- The prompt(s) or code that worked
- (Optional) a screenshot or transcript

Single-file additions in any language welcome — Python, TypeScript, shell, whatever fits.
