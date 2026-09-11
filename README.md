# LLM Wiki Template

A reusable [Karpathy-style LLM Wiki](https://github.com/karpathy): raw evidence in `docs/raw/`, an
agent-maintained markdown knowledge base in `docs/wiki/`, and rules in `AGENTS.md` so the wiki
compounds over time.

Use this template for **any** topic — product architecture, research notes, company ops, a codebase,
a personal second brain — not just infrastructure.

## Features

- Three-layer layout: **raw sources → wiki pages → schema**
- Bounded operation log with day archives (7-day / 90-day rotation)
- GitHub Action that publishes `docs/wiki/` to the **GitHub Wiki**
- Agent skills for **ingest**, **lint**, and **publish**
- Optional auto-merge workflow for bot PRs on docs-only repos
- Starter stub pages so the first ingest has a place to land

## Create a wiki from this template

1. Click **Use this template** on GitHub (or `gh repo create my-wiki --template <owner>/llm-wiki-template`).
2. Enable **Wikis** in the new repo settings and create one empty page named `Home` (required once so the `*.wiki` git remote exists).
3. Edit `AGENTS.md`, `SOUL.md`, and `docs/AGENTS.md` purpose/timezone for your domain.
4. Push to your default branch — wiki sync runs automatically when `docs/wiki/**` changes.
5. Open in Cursor / Claude Code and say: *Ingest `docs/raw/...`* or just ask a question.

## How it works

| Layer | Path | Description |
|-------|------|-------------|
| Raw sources | `docs/raw/` | Evidence: `current/` living snapshots + dated immutable captures |
| Wiki | `docs/wiki/` | Agent-maintained pages, index, and rolling log |
| Schema | `docs/AGENTS.md` | Page format, ingest, lint, citation, and sync rules |

## Quick reference

| Operation | What to say |
|-----------|-------------|
| Add a source | "Ingest `docs/raw/<path>`" |
| Ask a question | Just ask — agent reads `docs/wiki/index.md` first |
| Health-check | "Lint the wiki" |
| Publish | Push to default branch (or see `.agents/skills/llm-wiki-publish/`) |

## Agent skills

| Skill | Path | When to use |
|-------|------|-------------|
| Ingest | `.agents/skills/llm-wiki-ingest/` | Turning raw sources into wiki pages |
| Lint | `.agents/skills/llm-wiki-lint/` | Auditing contradictions, orphans, format drift |
| Publish | `.agents/skills/llm-wiki-publish/` | GitHub Wiki sync setup and troubleshooting |

## License

MIT — use freely. Attribution appreciated but not required.
