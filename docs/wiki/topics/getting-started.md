# Getting started

**Summary**: Orientation page for a new LLM wiki — what lives where, and how to grow it.

**Sources**: Template stubs (no domain sources yet).

**Last updated**: (set on first real ingest)

---

This repository follows a three-layer pattern:

1. **`docs/raw/`** — evidence (living `current/` snapshots and immutable dated captures)
2. **`docs/wiki/`** — agent-maintained pages linked with `[[wiki-links]]`
3. **`docs/AGENTS.md`** — the schema the agent follows on every ingest, query, and lint

## First ingest

1. Drop a source into `docs/raw/current/` or `docs/raw/YYYY/MM/DD/`
2. Register it in `docs/raw/index.md` or that day's `README.md`
3. Ask the agent: *Ingest `docs/raw/...`*
4. Review the proposed pages, then let it update `index.md` and the operation log

## Related pages

- [[llm-wiki-pattern]]
