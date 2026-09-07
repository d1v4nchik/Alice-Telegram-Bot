# Security Policy

## Supported Versions

This project is a single-branch, self-hosted Telegram bot with no versioned
releases. Only the latest code on `main` is supported — please update to the
latest commit before reporting an issue.

## Reporting a Vulnerability

If you find a security vulnerability (for example: a way to bypass host-only
permission checks, leak another player's secret/DM content, or crash the bot
via crafted input), please **do not** open a public issue.

Instead, report it privately using
[GitHub Security Advisories](../../security/advisories/new) for this
repository. Include:

- A description of the vulnerability and its impact
- Steps to reproduce (a minimal Telegram command/callback sequence is ideal)
- Any relevant logs (with tokens/chat IDs redacted)

You should receive an initial response within a few days. Once a fix is
available, we'll coordinate on disclosure timing before any public writeup.

## Scope Notes

This bot handles Telegram bot tokens and in-game player data (character
secrets, notes, suspicion points) held in memory and in a local
`lobby_state.json` file. It does not handle payments, passwords, or any data
beyond what's needed to run the game. If you're self-hosting, treat your
`TELEGRAM_BOT_TOKEN` and `lobby_state.json` as sensitive — the latter
contains player names and Telegram user IDs.
