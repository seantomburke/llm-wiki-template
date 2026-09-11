# LLM wiki pattern

**Summary**: A Karpathy-style knowledge base where an LLM maintains interlinked markdown pages from curated raw sources, so answers compound over time.

**Sources**: Template stubs.

**Last updated**: (set on first real ingest)

---

## Why

Chat transcripts are ephemeral. A wiki with an index, citations, and an operation log turns each
investigation into durable memory the next session can reuse.

## Layers

```mermaid
flowchart TD
    Raw["docs/raw/<br/>evidence"] --> Ingest["Ingest"]
    Ingest --> Pages["topics / concepts / …"]
    Pages --> Index["index.md"]
    Ingest --> Log["log.md + archive/"]
    Pages --> Sync["GitHub Wiki publish"]
```

## Related pages

- [[getting-started]]
