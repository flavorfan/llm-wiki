---
title: "Ingest Workflow"
type: concept
tags: [knowledge-synthesis, ingest, workflow]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# Ingest Workflow

## Definition

The ingest workflow is the process of taking a new source document from the raw collection and integrating its knowledge into the wiki. The LLM reads the source, extracts key information, creates or updates relevant wiki pages, establishes cross-references, and logs the changes. This is the primary way knowledge enters and enriches the [[concepts/llm-knowledge-base]].

## How It Works

**Standard ingest steps:**

1. **Read source**: LLM reads the raw source document completely (article, paper, transcript, image)
2. **Discuss takeaways**: LLM summarizes key points, may confirm with human what to emphasize
3. **Create summary page**: New page in `wiki/summaries/` with full summary and metadata
4. **Identify entities and concepts**: Extract all people, tools, organizations, ideas, methods mentioned
5. **Create/update pages**: For each entity or concept, create page if new or update with new information
6. **Establish cross-links**: Add bidirectional wiki links between related pages
7. **Update index**: Add new pages to `wiki/index.md` or update existing entries
8. **Log activity**: Append entry to `wiki/log.md` with timestamp, source name, pages touched
9. **Flag contradictions**: If new information conflicts with existing wiki content, note it

**Typical impact**: Single source might touch 10-15 wiki pages through summary, entity updates, concept additions, and cross-references.

## Key Parameters

- **Ingestion mode**:
  - **Interactive**: Process one source at a time with human guidance on what to emphasize
  - **Batch**: Process multiple sources with less supervision
  - **Automated**: Use [[concepts/loop-automation]] to ingest on schedule

- **Granularity**: How detailed summaries and extractions should be
- **Link aggressiveness**: How liberally to create cross-references between pages
- **Update threshold**: When to update existing pages vs. just reference them
- **Human involvement**: How much to discuss vs. auto-process

## When To Use

**Interactive ingest** (recommended for):
- High-value sources where nuance matters
- Sources that might contradict existing knowledge
- When building initial wiki structure and learning domain
- Complex multi-faceted sources (long papers, books)

**Batch ingest** for:
- Many similar sources (e.g., collection of articles on same topic)
- Well-structured data where extraction is straightforward
- Catching up after collecting many raw sources

**Automated ingest** (with [[concepts/loop-automation]]):
- Continuous feeds (meeting transcripts, daily readings)
- Mobile notes that need processing when back at desktop
- Regular content monitoring (RSS, newsletters)

## Risks & Pitfalls

- **Shallow processing**: Batch mode may miss nuance or important connections
- **Duplicate content**: Same information from multiple sources can create redundant pages
- **Broken links**: If page creation and cross-linking aren't atomic, can leave dangling references
- **Over-extraction**: Creating too many low-value concept pages clutters wiki
- **Missing context**: Without human guidance, LLM may misinterpret domain-specific terminology
- **Index drift**: If index isn't updated atomically with pages, becomes stale
- **Log bloat**: Detailed logs can become overwhelming; need summary views

## Related Concepts

- [[concepts/llm-knowledge-base]] — Overall system that ingest feeds
- [[concepts/knowledge-compilation]] — The compilation process ingest performs
- [[concepts/obsidian-web-clipper]] — Common tool for capturing sources to ingest
- [[concepts/query-workflow]] — How to use the ingested knowledge
- [[concepts/lint-workflow]] — Clean up after many ingestions
- [[concepts/loop-automation]] — Automate ingestion on schedule

## Sources

- [[summaries/llm-wiki]] — Detailed ingest workflow description
- [[summaries/karpathy-x]] — Practical ingest experience with real data
- [[summaries/claude-karpathy-second-brain-video]] — Step-by-step ingest demonstration
