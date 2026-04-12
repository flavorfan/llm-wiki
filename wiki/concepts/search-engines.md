---
title: "Search Engines"
type: concept
tags: [search, retrieval, tools, infrastructure]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md"]
confidence: medium
---

# Search Engines

## Definition

Search engines are tools that enable fast text-based search across knowledge bases. In the context of LLM wikis, they provide the retrieval layer that allows LLMs to find relevant documents before generating responses.

## How It Works

Traditional search engines work by:
1. **Indexing** — pre-processing documents to build searchable indexes
2. **Query processing** — parsing user queries into search terms
3. **Retrieval** — finding documents matching the query
4. **Ranking** — ordering results by relevance

In LLM wiki contexts, search engines may be replaced by or augmented with:
- Full-text search within the LLM's context window (token-based search)
- Vector similarity search for semantic retrieval
- Graph-based traversal following wiki links

## Key Parameters

- **Index size** — number of documents or tokens indexed
- **Query latency** — time to return results
- **Recall** — percentage of relevant documents found
- **Precision** — percentage of returned documents that are relevant

## When To Use

Use traditional search engines when:
- The knowledge base exceeds the LLM's context window
- Fast retrieval of specific documents is needed
- The corpus is too large for complete ingestion

Consider context-window-based approaches when:
- The entire knowledge base fits within the LLM's context window
- You want the LLM to have complete awareness of all documents
- Cross-document synthesis is important

## Risks & Pitfalls

- **Context fragmentation** — retrieving individual documents may miss connections between them
- **Ranking failures** — may not retrieve the most relevant documents for LLM synthesis
- **Stale indexes** — search results may not reflect recent updates
- **Query mismatch** — keyword search may miss semantically similar content

## Related Concepts

- [[concepts/rag]] — Retrieval-Augmented Generation uses search engines as a component
- [[concepts/llm-knowledge-base]] — Compares search-based vs context-window-based approaches
- [[concepts/query-workflow]] — Uses search to find relevant pages
- [[concepts/index-files]] — Alternative to search engines for navigation

## Sources

- raw/llm-wiki.md — Discusses context window approach as alternative to search
- raw/karpathy-x.md — Mentions "search engines" in context of Obsidian workflow
