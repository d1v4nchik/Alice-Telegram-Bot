# Contributing to Alice Is Missing – Telegram Bot

Thanks for taking the time to contribute! This is a self-hosted Telegram bot
for running the *Alice Is Missing* tabletop game, and contributions of all
sizes are welcome — bug reports, bug fixes, docs, and new features.

## Before you start

- Check [open issues](../../issues) and [pull requests](../../pulls) to avoid
  duplicating work.
- For anything beyond a small fix, open an issue first to discuss the change
  — it saves everyone time if the approach needs adjusting.
- By contributing, you agree to follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## Development setup

```bash
git clone https://github.com/d1v4nchik/Alice-Telegram-Bot.git
cd Alice-Telegram-Bot
pip install -r requirements.txt
cp .env.example .env   # fill in TELEGRAM_BOT_TOKEN from @BotFather
python3 main.py
```

The bot runs on long-polling, so no public URL or webhook setup is needed for
local development.

## Project layout

| File | Purpose |
|---|---|
| `main.py` | Entry point — registers handlers, starts polling |
| `alice_handlers.py` | Command and callback handlers |
| `alice_helpers.py` | Game logic, background loops, state persistence |
| `alice_models.py` | `GameSession` / `PlayerState` data classes |
| `alice_keyboards.py` | Reply/inline keyboard layouts |
| `content.py` | Trigger cards, secrets, and other game text |

Game state is persisted to `lobby_state.json` (git-ignored — it's runtime
data, not source).

## Making changes

1. Fork the repo and create a branch off `main`.
2. Keep changes focused — one logical change per pull request.
3. Verify your change:
   ```bash
   python3 -m py_compile alice_handlers.py alice_helpers.py alice_models.py alice_keyboards.py main.py
   python3 -c "import alice_helpers, alice_handlers, alice_models, alice_keyboards"
   ```
   There's no automated test suite yet — a PR that adds one for a piece of
   game logic (e.g. `elapsed_seconds`, `_pick_trigger`) is very welcome.
4. If you touch a live game flow (trigger scheduling, pause/resume, lobby
   state), run the bot locally against a real Telegram group/DM and exercise
   the flow — this codebase has bitten itself before on state that only
   breaks under a live restart or a second concurrent game.

## Submitting a pull request

- Describe *why* the change is needed, not just what it does.
- Reference the issue it closes, if any (`Closes #123`).
- Keep commit messages descriptive; squash noisy WIP commits before opening
  the PR.

## Reporting bugs

Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md). Include
steps to reproduce, what you expected, and what actually happened — bot logs
are especially helpful since most failures here are async/timing related.

## Reporting security issues

Please do **not** open a public issue for security vulnerabilities — see
[SECURITY.md](SECURITY.md) instead.
