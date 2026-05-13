# Contributing to Journely MCP Server

Thanks for your interest in improving this project. This repository is the public-facing landing for the [Journely](https://journely.me) MCP server (hosted at `https://api.journely.me/mcp`). The server itself isn't open-source yet, so contributions here focus on **documentation, examples, integrations, and feedback**.

## What you can contribute

| Type | Examples |
|---|---|
| **Examples** | A working integration in Python, TypeScript, Go, Rust, etc.; a real Claude prompt that uses multiple tools well; a notebook demonstrating an analysis |
| **Docs improvements** | Typo fixes, clearer phrasing, missing-detail callouts, better comparison points |
| **Bug reports** | Wrong data from a tool, unexpected schema, slow response, anything that's surprising |
| **Tool requests** | "I wish Journely exposed X" — open an issue tagged `enhancement` |
| **Use-case writeups** | A blog post, a tweet thread, an article that uses Journely well — link it in an issue and we'll add it to the README "in the wild" section |

## How to submit a change

1. **Fork** this repository
2. **Branch:** `feature/your-change` or `fix/your-change`
3. **Make your change.** Keep PRs focused — one concern per PR
4. **Commit message:** use a short imperative subject line. Example: `Add Python example with httpx async client`
5. **Open a PR** against `main`. Describe what changed and why
6. Maintainers will review within a few business days. We're a small project, so expect occasional delays during launches

## Style

- **README:** Markdown, GitHub-flavored. Tables for tool/endpoint lists. Section headers in title case. Examples runnable as-pasted.
- **Code examples:** Self-contained. No "...assumed setup." Include the `Authorization` header explicitly with `YOUR_TOKEN` placeholder.
- **Tone:** Direct, peer-to-peer technical. No marketing fluff. Honesty over hype.

## What we won't accept

- Examples that include real API keys or tokens (ever)
- PRs that change `https://api.journely.me/...` URLs without coordinating with the maintainer
- Bulk auto-generated content
- Promotional content for unrelated products

## Reporting security issues

Don't open a public issue for security vulnerabilities. See [SECURITY.md](./SECURITY.md) for the disclosure process.

## Code of conduct

By participating, you agree to follow our [Code of Conduct](./CODE_OF_CONDUCT.md). Be respectful, be specific, be useful.

## Questions

Open an issue, or reach out to `hello@journely.me`.
