# Changelog

All notable changes to this repository (the public landing for the Journely MCP server) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html) for the documentation versions.

The actual MCP server runs at `https://api.journely.me/api/v1/journely/mcp` and follows its own versioning. Material changes to the server's API surface will be reflected in this file as `[Server]` entries.

## [Unreleased]

### Fixed
- MCP endpoint URL in `README.md` and `examples/claude_desktop_config.json` — was `https://api.journely.me/mcp` (404), now the live `https://api.journely.me/api/v1/journely/mcp`
- Tool reference, quick-start cURL/Python snippets and example prompts updated to the current 9-tool surface (server 0.6.0); removed tools (`get_markets`, `list_symbols`, `get_sectors`, `get_stock_technicals`) no longer referenced
- Rate-limit table now matches the published per-plan limits (Free / Pro / Max)

### Added
- `server.json` for the official MCP Registry (remote Streamable HTTP endpoint)

### Server (0.6.0, current)
- 0.3.0 removed `get_markets`, `list_symbols`, `get_sectors`, `get_stock_technicals`
- 0.3.0–0.6.0 added `get_stock_forecast`, `get_stock_price_history`, `get_sector_overview`, `get_earnings_calendar`
- OAuth 2.1 + PKCE discovery (`/.well-known/oauth-protected-resource`) alongside bearer tokens

## [0.1.0] — 2026-05-13

### Added
- Initial public release of the Journely MCP server landing repo
- `README.md` with full quick-start (Claude Desktop, cURL, Python), 9-tool reference table, REST+MCP parity table, honest pricing disclosure, comparison vs vnstock / VNQuant / iTick / FiinGroup / broker MCPs
- `examples/claude_desktop_config.json` — drop-in snippet for Claude Desktop users
- `examples/README.md` — example prompt patterns demonstrating multi-tool orchestration
- `CONTRIBUTING.md`, `SECURITY.md`, `CODE_OF_CONDUCT.md` — community hygiene
- Issue + PR templates under `.github/`
- MIT license

### Server (live at api.journely.me/mcp at this release)
- 9 MCP tools: `get_markets`, `list_symbols`, `get_macro_indicators`, `get_macro_forecast`, `get_macro_calendar`, `get_sectors`, `get_stock_overview`, `get_stock_statements`, `get_stock_technicals`
- 9 REST endpoints with 1:1 parity to the MCP tools
- Streamable HTTP transport (MCP spec 2025-06-18)
- Free tier: 100 requests/day/key
