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

## Changelog generator (#1)

Requires Git, Bash and Python 3.8+ on your PATH. No packages, API keys or network
access are needed to generate a changelog from a local repository.

1. Copy `changelog.sh` and `changelog.py` together into your project, or keep this checkout.
2. Run `bash changelog.sh` in your project. From another directory, use
   `bash /path/to/changelog.sh --repo /path/to/project`.
3. Review the generated `CHANGELOG.md` at the target repository's root.

`--output release-notes.md` selects another file (relative to the repository root,
or an absolute path). Each run **replaces that file with a complete snapshot**;
it does not append to an existing release archive. Generation is atomic and
repeatable for unchanged history. Git commits, refs and tags are never modified.

The boundary is Git's nearest reachable tag (`git describe --tags --abbrev=0`),
including annotated and lightweight tags, rather than the highest version or an
unrelated branch's newest tag. The tagged commit is excluded. All later reachable
commits are included, including merge commits, oldest first within each section.
With no reachable tag, all history is used. An empty repository or HEAD exactly
at its tag produces four empty sections. Shallow history is rejected: obtain the
complete history and tags before running. The script never fetches automatically.

Classification uses the subject's leading word or Conventional Commit type:

| Section | Types / leading words |
| --- | --- |
| Added | feat, feature, add/adds/added, create/creates/created |
| Fixed | fix/fixes/fixed, bugfix, repair/repairs, resolve/resolves/resolved |
| Removed | remove/removes/removed, delete/deletes/deleted, drop/drops/dropped |
| Changed | Everything else, including refactors, docs, merges and reverts |

Scopes and breaking markers such as `feat(api)!:` are supported. Each commit gets
one section; its original subject and commit ID are retained. Bodies do not create
extra entries. This is a deterministic naming heuristic, not semantic analysis of
code changes: review ambiguous subjects. Subjects/tags are escaped as Markdown
text; no commit message is executed. Non-UTF-8 text uses replacement characters.

Run `python3 tests/test_changelog.py` to exercise the **actual Bash entry point**
against disposable Git repositories. The [real-repository sample](samples/README.md)
records a pinned MarkupSafe checkout, real tag, output and reproduction command.
CI runs these checks on standard Ubuntu without installing dependencies.
