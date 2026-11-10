# LLM Wiki Template

This repository is a Karpathy-style **LLM Wiki**: a persistent, compounding knowledge base
maintained by an AI agent. Humans curate sources and ask questions; the agent ingests,
synthesizes, links, and keeps the map current.

Customize this file for your topic (product, codebase, research area, company ops, etc.).
Replace the placeholders below, then delete any sections that do not apply.

---

## What this repo is

- **Layer 1 — Raw sources** (`docs/raw/`): immutable evidence and living snapshots.
  Split into `current/` (refreshed in place) and `YYYY/MM/DD/` (point-in-time captures, never modify).
- **Layer 2 — Wiki** (`docs/wiki/`): LLM-maintained markdown pages — topics, concepts, index, and log.
- **Layer 3 — Schema** (`docs/AGENTS.md`): page format, ingest workflow, lint rules, and conventions.

## Agent instructions

`AGENTS.md` is the only agent-instructions file in this repo. Every agent (Claude Code, Cursor,
Codex, …) reads it directly, so never add a `CLAUDE.md`. Start with this root file, then read any
`AGENTS.md` in the subdirectories you are about to work in; the one nearest a file takes precedence.

## Agent identity

Edit [`SOUL.md`](SOUL.md) to name and characterize the agent that lives in this repo.
The agent maintains the wiki; it does not replace human judgment on what belongs here.

## Setup

1. Create a new repository from this GitHub template.
2. Enable the GitHub Wiki on the new repo (Settings → Wikis), then create one empty page (e.g. `Home`) so the `*.wiki` git remote exists.
3. Push to your default branch — [`.github/workflows/sync-wiki.yml`](.github/workflows/sync-wiki.yml) publishes `docs/wiki/` to the GitHub Wiki.
4. Open the repo in Cursor / Claude Code and ask a question — the agent reads `docs/wiki/index.md` first.
5. Optional: copy `.env.template` → `.env` for any local API keys your ingest tools need.

## Full schema

See [`docs/AGENTS.md`](docs/AGENTS.md) for the complete wiki schema — page format, ingest workflow,
query workflow, lint instructions, and all conventions. This includes the **Raw file size (~1 MB guideline)**.

## Time zone

When responding with any time or timestamp, express it in your team's local zone and label it
explicitly (e.g. `2026-04-23 2:00 PM PDT`). Do not leave bare UTC times in wiki prose unless the
domain requires it — if you must show UTC, also show the local equivalent.

**Default for this template:** Pacific Time (PST/PDT). Change this line when you fork.

## Quick reference

| Operation | What to say |
|-----------|-------------|
| Add a new source | "Ingest `docs/raw/<path>`" |
| Ask a question | Just ask — agent reads `docs/wiki/index.md` first |
| Health-check the wiki | "Lint the wiki" |
| Publish to GitHub Wiki | Push to the default branch (auto-sync), or "sync the wiki" |
| Update after new captures | "Ingest the latest raw snapshots" |

## Folder structure

```
AGENTS.md               -- this file: agent entry point, quick reference
SOUL.md                 -- optional agent persona / voice
.env.template           -- optional secrets format (committed, no real values)
.agents/skills/         -- agent skills (ingest, lint, publish)
.github/workflows/
├── sync-wiki.yml       -- publish docs/wiki/ → GitHub Wiki
└── auto-merge-bot-prs.yml -- optional: auto-merge bot PRs (docs-only repos)
docs/
├── AGENTS.md           -- full wiki schema and conventions
├── raw/                -- source documents and tool output
│   ├── index.md        -- raw inventory: current/ + captures-by-date rollup
│   ├── current/        -- living snapshots (refreshed in place)
│   └── YYYY/MM/DD/     -- immutable point-in-time captures + README.md manifest
└── wiki/
    ├── index.md        -- table of contents for the entire wiki
    ├── log.md          -- rolling operation log (7 days full, 90 days indexed)
    ├── archive/        -- log-archive.md + YYYY/MM/YYYY-MM-DD.md full operation prose
    ├── topics/         -- one page per major subject area (customize freely)
    └── concepts/       -- cross-cutting ideas (customize freely)
```

Add more wiki subfolders (`entities/`, `people/`, `products/`, `runbooks/`, …) as your domain needs them.
Keep **basename uniqueness** across `docs/wiki/` — the GitHub Wiki sync flattens paths to basenames.
