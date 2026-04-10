---
title: "Knowledge Compilation"
type: concept
tags: [knowledge-synthesis, foundational, retrieval]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md"]
confidence: high
---

# Knowledge Compilation

## Definition

Knowledge compilation is the process of incrementally building and maintaining a structured, persistent representation of knowledge from source documents, as opposed to retrieving from raw sources at query time. The LLM reads sources once, extracts key information, integrates it into an evolving wiki structure, and keeps cross-references and synthesis up to date. Knowledge is **compiled and kept current** rather than re-derived on every query.

## How It Works

**Compilation process:**

1. **Read and extract**: LLM reads new source document completely
2. **Integrate**: Identifies entities, concepts, claims; creates or updates relevant wiki pages
3. **Cross-reference**: Adds bidirectional links between related pages
4. **Synthesize**: Updates higher-level synthesis to reflect new information
5. **Flag contradictions**: Notes when new data contradicts existing claims
6. **Update metadata**: Logs changes, updates index, maintains consistency

**Persistent structure:**

- Summaries of all sources
- Entity pages (people, tools, organizations)
- Concept pages (ideas, methods, frameworks)
- Synthesis pages (comparisons, analyses, recommendations)
- Index and log files for navigation

**Ongoing maintenance:**

- New sources trigger updates across 10-15 existing pages
- Cross-references maintained automatically
- Contradictions surfaced for resolution
- Index files kept current

## Key Parameters

- **Granularity**: How detailed the compiled knowledge should be (full summaries vs. key points)
- **Update strategy**: Per-source incremental updates vs. batch processing
- **Conflict resolution**: How to handle contradictions (flag, version, choose highest confidence)
- **Link density**: How aggressively to cross-reference between pages
- **Confidence tracking**: Whether to track and display confidence levels per claim

## When To Use

**Prefer compilation over retrieval when:**

- Working with moderate-scale corpus (~100 sources, ~400K words)
- Need to synthesize across multiple sources frequently
- Want answers to compound and build on previous work
- Contradictions and gaps are important to track
- Cross-references and relationships matter as much as content
- Query latency should be low (no retrieval search needed)

**Compilation advantages:**

- **vs. RAG**: No need to retrieve and re-synthesize on every query; relationships already established
- **vs. Vector search**: Semantic connections explicit rather than implicit in embeddings
- **vs. Chat history**: Insights persist and compound rather than disappearing
- **Compounding value**: Each source makes the whole wiki more valuable

## Risks & Pitfalls

- **Compilation cost**: Initial processing requires touching many pages per source
- **Staleness**: Compiled knowledge can become outdated if sources aren't refreshed
- **Contradiction propagation**: Incorrect synthesis can spread across many pages before detection
- **Over-compilation**: Can spend too much effort structuring before critical mass of content
- **Scale limits**: At very large scale, may need to hybrid with retrieval (compile summaries, retrieve details)

## Related Concepts

- [[concepts/llm-knowledge-base]] — System architecture that uses compilation
- [[concepts/ingest-workflow]] — The compilation process in practice
- [[concepts/persistent-artifact]] — The result of compilation
- [[concepts/rag]] — Retrieval-based alternative approach
- [[concepts/wiki-maintenance]] — Ongoing work to keep compilation current

## Sources

- [[summaries/llm-wiki]] — Distinguishes compilation from retrieval-based approaches
