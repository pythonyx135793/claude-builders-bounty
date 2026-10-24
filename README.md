# Claude Builders Bounty 🤖

> A community bounty board for Claude Code builders.

Building with Claude Code? Have tasks to delegate?
Want to get paid for contributing to AI projects?
You're in the right place.

---

## How it works

**To post a bounty**
1. Open a GitHub issue with a clear description and acceptance criteria
2. Comment `/opire create $XXX` in the issue to set the reward
3. Share the link — contributors will find it

**To claim a bounty**
1. Browse the open issues below
2. Comment `/opire try` in the issue you want to work on
3. Submit a PR — payment is automatic on merge ✅

---

## Active Bounties

| # | Task | Amount | Status |
|---|------|--------|--------|
| [#1](../../issues/1) | SKILL: Generate a CHANGELOG from git history | $50 | 🟢 Open |
| [#2](../../issues/2) | TEMPLATE: CLAUDE.md for a Next.js + SQLite project | $75 | 🟢 Open |
| [#3](../../issues/3) | HOOK: Block destructive bash commands in Claude Code | $100 | 🟢 Open |
| [#4](../../issues/4) | AGENT: PR reviewer with structured Markdown output | $150 | 🟢 Open |
| [#5](../../issues/5) | WORKFLOW: n8n + Claude API — automated weekly dev summary | $200 | 🟢 Open |

---

## Rules

- Tasks must be related to Claude Code or AI tooling
- Every issue must have clear acceptance criteria before a bounty is activated
- Payment is handled by [Opire](https://opire.dev) (Stripe)
- Quality over speed — a solid PR beats a fast one

---

## Community

- 🐦 X: [@ClaudeBounty](https://x.com/ClaudeBounty)
- 📧 Contact: claudebounty@gmail.com

---

*Started by the Claude builder community · March 2026 · MIT License*

## Bash safety hook (#3)

Requires Python 3.9+ and Claude Code 2.1.295+ with the Bash tool. From this
checkout, install with one command:

```bash
python3 install_hook.py
```

This copies the hook to `~/.claude/hooks/bash_guard.py` and registers it in
`~/.claude/settings.json`, preserving unrelated settings and hooks. Restart
Claude Code afterward and check its `/hooks` menu. `CLAUDE_CONFIG_DIR` or
`--config-dir PATH` selects an alternate configuration directory.

The hook denies recursive forced removal, forced Git pushes, `DROP TABLE`,
`TRUNCATE`, and `DELETE FROM` without a same-statement `WHERE`. It records
blocked commands in `hooks/blocked.log`. Other commands retain Claude Code's
normal permission checks. See the [policy, examples and tests](docs/bash-guard.md)
for supported syntax and limits.
