---
title: "LLM Knowledge Base"
type: concept
tags: [knowledge-synthesis, foundational, llm-agents, markdown]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# LLM Knowledge Base

## Definition

An LLM knowledge base is a system where a large language model incrementally builds and maintains a persistent, structured wiki from raw source documents, rather than simply retrieving from sources at query time. The key innovation is that knowledge is **compiled once and kept current** through continuous LLM maintenance, creating a compounding artifact that grows richer with each source and query.

## How It Works

**Three-layer architecture:**

1. **Raw sources** — Immutable collection of source documents (articles, papers, transcripts, images, data files). The LLM reads from but never modifies these.

2. **The wiki** — Directory of LLM-generated markdown files including summaries, entity pages, concept pages, comparisons, and synthesis documents. The LLM owns this layer entirely - creating, updating, cross-referencing, and maintaining consistency.

3. **The schema** — Configuration document (e.g., CLAUDE.md, AGENTS.md) that defines wiki structure, conventions, and workflows. Co-evolved by human and LLM over time.

**Core workflows:**

- **[[concepts/ingest-workflow]]** — Process new sources into wiki
- **[[concepts/query-workflow]]** — Answer questions against wiki, file valuable outputs back
- **[[concepts/lint-workflow]]** — Health-check for contradictions, gaps, and enhancement opportunities

**Navigation at scale:**

- [[concepts/index-files]] provide content-oriented catalog of all pages
- Append-only logs provide chronological record of changes
- Works at ~100 sources / ~400K words without embedding-based RAG
- Custom [[concepts/search-engines]] can be added as scale increases

## Key Parameters

- **Scale**: Moderate scale (~100 sources, ~400K words) works with simple index files; larger scale may require search infrastructure
- **Update frequency**: Depends on use case - can be manual per-source, batch processing, or automated with loop/cron
- **Maintenance burden**: Near-zero for humans (LLM handles all bookkeeping)
- **Specialization**: Can maintain separate knowledge bases for different domains (personal, business, research topics)

## When To Use

**Ideal for:**
- Research projects spanning weeks/months with evolving synthesis
- Personal knowledge management (goals, health, learning, reading)
- Business intelligence (meeting notes, customer calls, competitive analysis)
- Reading companion wikis (books, courses, long-form content)
- Team knowledge bases fed by Slack, transcripts, documents
- Due diligence, trip planning, hobby deep-dives

**Advantages over alternatives:**
- **vs. RAG/NotebookLM**: Knowledge accumulates and compounds rather than being re-derived on each query
- **vs. Human wikis**: LLMs handle tedious cross-referencing and maintenance that humans abandon
- **vs. Chat history**: Explorations and insights persist as structured pages rather than disappearing
- **vs. Claude Projects**: More structured, scales better, optimized for knowledge synthesis

## Risks & Pitfalls

- **Initial setup overhead**: Requires defining schema, workflows, and conventions upfront
- **Too many vaults**: Managing multiple knowledge bases can become maintenance burden itself
- **Stale data**: Without regular linting, contradictions and outdated claims can accumulate
- **Scale limitations**: Simple index-based navigation eventually breaks down; may need to add search infrastructure
- **Quality dependency**: Wiki quality depends on source quality and LLM's understanding - garbage in, garbage out
- **Context window limits**: Very large wikis may require chunking or external search tools
- **Over-structuring**: Can be tempting to over-engineer taxonomy and structure before content exists

## Related Concepts

- [[concepts/second-brain]] — Popular framing for personal knowledge management system
- [[concepts/knowledge-compilation]] — Core mechanism distinguishing this from retrieval-based systems
- [[concepts/wiki-maintenance]] — The bookkeeping work LLMs excel at
- [[concepts/persistent-artifact]] — Why this compounds value over time
- [[concepts/rag]] — Alternative approach using retrieval at query time

## Sources

- [[summaries/llm-wiki]] — Abstract pattern definition and philosophy
- [[summaries/karpathy-x]] — Real-world workflow from originator
- [[summaries/claude-karpathy-second-brain-video]] — Practical implementation tutorial
