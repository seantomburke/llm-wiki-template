---
name: llm-wiki-lint
description: >-
  Audit the LLM wiki for contradictions, orphans, missing concept pages,
  stale claims, format drift, and basename collisions. Use when the user says
  lint the wiki, audit the wiki, or health-check the knowledge base.
---

# LLM Wiki — Lint

Follow the **Lint** section in [`docs/AGENTS.md`](../../../docs/AGENTS.md).

## Checklist

1. Read `docs/wiki/index.md` and spot-check linked pages.
2. Contradictions between pages (flag both sides + sources).
3. Orphan pages (no inbound `[[wiki-links]]` from other pages; index alone does not count as enough if nothing else links).
4. Concepts mentioned in prose that lack their own page.
5. Claims that look stale vs newer raw captures or newer log entries.
6. Page format compliance (Summary, Sources, Last updated, Related pages).
7. Basename uniqueness under `docs/wiki/` (required for GitHub Wiki sync).
8. Log rotation sanity (Recent ≤ 7 days of full prose; archive day files exist for Recent entries).

## Report format

Numbered findings. Each item: problem, evidence (paths), suggested fix. Do not silently rewrite the wiki unless the user asks you to apply fixes.
