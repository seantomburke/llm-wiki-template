---
name: llm-wiki-publish
description: >-
  Publish docs/wiki/ to the GitHub Wiki via the sync-wiki GitHub Action, or
  troubleshoot wiki sync failures. Use when the user asks to sync/publish the
  wiki, enable GitHub Wiki publishing, or fix a failed sync-wiki workflow.
---

# LLM Wiki — Publish to GitHub Wiki

The workflow [`.github/workflows/sync-wiki.yml`](../../../.github/workflows/sync-wiki.yml) copies
`docs/wiki/` into the repository's GitHub Wiki on pushes that touch `docs/wiki/**`
(and on `workflow_dispatch`).

## One-time setup (new repo from template)

1. In GitHub: **Settings → General → Features → Wikis** — enable.
2. Open the **Wiki** tab and create a page named `Home` with any placeholder text. Save.
   This creates the `{owner}/{repo}.wiki` git repository the Action checks out.
3. Ensure the default branch is `main` or `master` (the workflow listens to both).
4. Push a change under `docs/wiki/` or run the workflow manually (**Actions → Sync Wiki → Run workflow**).

`GITHUB_TOKEN` with `contents: write` is enough for same-repo wiki pushes; no extra secret is required.

## What the Action does

1. Checkout the code repo
2. Checkout `{repository}.wiki` into `./wiki`
3. `rsync -av --delete` from `docs/wiki/` → `wiki/` (excludes `.git`)
4. Rename `index.md` → `Home.md`
5. Commit and push if there is a diff

## Basename uniqueness (common failure mode)

GitHub Wiki flattens directories to page titles by **basename**. Two files like
`topics/overview.md` and `concepts/overview.md` overwrite each other. Always use
distinct filenames (`topic-overview.md`, …). Archive days must be `YYYY-MM-DD.md`,
not `DD.md`. Prefer `log-archive.md` over `archive/index.md`.

Wiki-links must use bare names: `[[page-name]]`, not `[[concepts/page-name]]`.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Checkout of `*.wiki` fails | Wiki not enabled, or no page created yet — create `Home` once in the UI |
| Push rejected | Branch protection on wiki (rare) or missing `contents: write` |
| Missing / wrong pages | Basename collision — search for duplicate basenames under `docs/wiki/` |
| `Home` empty or stale | Ensure `docs/wiki/index.md` exists; workflow renames it to `Home.md` |
| Workflow never runs | Path filter: only `docs/wiki/**` on `main`/`master`, or use `workflow_dispatch` |

## Manual sync (local)

```bash
# Requires an existing wiki repo and push access
git clone "https://github.com/${OWNER}/${REPO}.wiki.git" /tmp/wiki-sync
rsync -av --delete --exclude='.git' docs/wiki/ /tmp/wiki-sync/
mv /tmp/wiki-sync/index.md /tmp/wiki-sync/Home.md
cd /tmp/wiki-sync && git add -A && git commit -m "docs: manual wiki sync" && git push
```

Prefer the GitHub Action for routine publishes.
