# Security Policy

## Reporting a vulnerability

If you discover a security vulnerability in the Journely MCP server, REST API, or anything in this repository (e.g., a leaked credential in a committed file), **please do not open a public GitHub issue**.

Instead, email **hello@journely.me** with:

- A clear description of the vulnerability
- Steps to reproduce
- The potential impact (data exposure, auth bypass, etc.)
- Optional: a proposed fix

You'll get an acknowledgement within **72 hours** and an estimated remediation timeline.

## What we treat as in-scope

- Authentication / authorization issues on `https://api.journely.me`
- Data leaks from the MCP or REST endpoints
- API-key handling weaknesses
- Server-side vulnerabilities (rate-limit bypass, injection, etc.)
- Anything in this repository that risks user secrets

## Out of scope

- Issues with third-party data providers we ingest from (forward to them)
- Self-XSS / social-engineering issues without a technical vulnerability
- DoS via volumetric attacks (covered by upstream infrastructure)
- "Best-practice" reports without a demonstrated exploit

## Acknowledgements

Researchers who responsibly disclose meaningful issues will be credited (with permission) in this file or in release notes. Journely is currently a solo / small-team operation — we don't run a paid bug bounty yet, but we deeply appreciate the help.

## API key handling — for users

- **Never commit your API key.** Use environment variables. The `.gitignore` in this repo blocks `.env`, `*.token`, and `*.key` files by default.
- **Rotate immediately** if you suspect a key has been exposed: revoke it at https://journely.me/settings/api-keys and generate a new one.
- **Free-tier keys** are throttled at 100 requests/day/key. If you see usage you don't recognize on the dashboard, rotate the key.
- The Journely server stores **only** the hashed prefix of your API key for auth — full keys are never logged.
