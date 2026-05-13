# Changelog

All notable changes to this repository (the public landing for the Journely MCP server) will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html) for the documentation versions.

The actual MCP server runs at `https://api.journely.me/mcp` and follows its own versioning. Material changes to the server's API surface will be reflected in this file as `[Server]` entries.

## [Unreleased]

### Added
- Nothing yet

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
