---
title: "Knowledge Graph"
type: concept
tags: [knowledge-synthesis, foundational, data-structure, linking]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/Andrej Karpathy's LLM Wiki  Bye Bye RAG.md", "raw/llm-wiki.md"]
confidence: high
---

# Knowledge Graph

## Definition

A knowledge graph is an interconnected network of entities, concepts, and relationships where nodes represent discrete pieces of knowledge (entities, concepts, facts) and edges represent meaningful connections between them. In the context of LLM wikis, a knowledge graph emerges naturally from the cross-linking of markdown pages, creating a structured representation of knowledge in natural language rather than formal ontologies.

## How It Works

In an LLM wiki, the knowledge graph is implemented through:

1. **Entity and concept pages** as nodes - Each distinct entity (person, tool, organization) or concept (strategy, technique, framework) gets its own page
2. **Wiki links as edges** - Bidirectional `[[page-name]]` links create explicit relationships between pages
3. **Semantic clustering** - Related pages cluster through shared tags and mutual references
4. **Incremental growth** - New sources add nodes and edges; ingest workflow maintains connectivity
5. **Natural language encoding** - Unlike formal knowledge graphs (RDF, triples), relationships are expressed in readable prose

## Key Parameters

- **Density**: Ratio of actual links to possible links - higher density indicates better interconnection
- **Hub pages**: Highly connected nodes that serve as central reference points (e.g., foundational concepts)
- **Orphans**: Pages with no inbound links - health checks should identify and address these
- **Clusters**: Groups of tightly connected pages around specific themes or topics
- **Depth**: Number of hops needed to traverse from one page to any other

## When To Use

- When knowledge accumulates over time and relationships between pieces matter
- When the same entities or concepts appear across multiple sources
- When queries require synthesizing information from multiple related topics
- When you need to discover non-obvious connections between disparate areas
- As an alternative to hierarchical folder structures that force single-parent categorization

## Risks & Pitfalls

- **Over-linking**: Creating links everywhere reduces signal - link only when relationship is meaningful
- **Under-linking**: Missing connections limits the graph's utility - lint workflow should catch these
- **Inconsistent naming**: Multiple pages for the same concept fragment the graph - use consistent terminology
- **Shallow pages**: Nodes with little content become dead ends - ensure each page adds substantive value
- **Graph becomes write-only**: If the structure is too complex to navigate, it defeats the purpose - balance interconnection with clarity

## Related Concepts

- [[concepts/persistent-artifact]] - The wiki as the durable manifestation of the knowledge graph
- [[concepts/graph-view]] - Obsidian's visualization tool for seeing the knowledge graph structure
- [[concepts/wiki-maintenance]] - Keeping the graph healthy through lint checks
- [[concepts/index-files]] - Structured navigation alternative to pure graph traversal
- [[concepts/llm-knowledge-base]] - The overall pattern that generates knowledge graphs

## Comparison to RAG

Traditional RAG systems don't build explicit knowledge graphs - they rely on vector similarity in embedding space. This means:
- **RAG**: Implicit, statistical relationships recalculated per query
- **Knowledge Graph**: Explicit, curated relationships that persist and compound

The LLM wiki approach creates a knowledge graph that combines machine precision (LLM maintains links) with human judgment (curator directs what sources to ingest).

## Sources

- [[summaries/bye-bye-rag]] - "Over time, your system stops being a collection of files and becomes a connected knowledge graph written in natural language"
- [[summaries/llm-wiki]] - Cross-referencing as core operation, backlinks mentioned in architecture
