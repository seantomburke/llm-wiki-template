---
name: llm-wiki-ingest
description: >-
  Ingest a raw source into the LLM wiki: read docs/raw/, update wiki pages,
  index, and operation log per docs/AGENTS.md. Use when the user says ingest,
  adds a new source under docs/raw/, or asks to update the wiki from captures.
---

# LLM Wiki — Ingest

Follow [`docs/AGENTS.md`](../../../docs/AGENTS.md). Do not invent domain-specific rules beyond that schema.

## Steps

1. **Locate the source** under `docs/raw/current/` or `docs/raw/YYYY/MM/DD/`.
2. **Read it fully.** If the payload approaches ~1 MB, stop and narrow before continuing.
3. **Discuss takeaways** with the user unless they asked you to proceed without review.
4. **Create or update** pages under `docs/wiki/topics/`, `docs/wiki/concepts/`, or other category folders. Use the page format (Summary, Sources, Last updated, body, Related pages).
5. **Wiki-link** related pages with bare names: `[[page-name]]`.
6. **Update** `docs/wiki/index.md` (one-line descriptions). Register new raw files in `docs/raw/index.md` or the day `README.md`. Do **not** list raw files in the wiki index.
7. **Log the operation**: write archive day file first (`docs/wiki/archive/YYYY/MM/YYYY-MM-DD.md`), update `log-archive.md` if new, then prepend to Recent in `docs/wiki/log.md`, then rotate tiers.
8. **Basename check**: ensure no two files under `docs/wiki/` share a basename.

## Capture before use

If you ran a live CLI/API that returned durable facts, save to `docs/raw/` *before* synthesizing, then ingest.

## Done when

- Relevant pages updated
- Index current
- Log + archive updated
- User can open `docs/wiki/index.md` and find the new material
