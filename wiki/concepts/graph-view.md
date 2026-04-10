---
title: "Graph View"
type: concept
tags: [obsidian, visualization, knowledge-synthesis]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/Claude + Karpathy's Second Brain is INSANE.md", "raw/llm-wiki.md"]
confidence: high
---

# Graph View

## Definition

Graph view is [[entities/obsidian]]'s visual representation of wiki page interconnections, showing each page as a node and each wiki link as an edge. It provides an intuitive way to understand the structure of a [[concepts/llm-knowledge-base]], identify knowledge clusters, spot orphaned pages, and see how new sources integrate with existing knowledge.

## How It Works

**Visual representation:**
- Each markdown file appears as a node
- Wiki links (`[[page-name]]`) create edges between nodes
- Clusters form around highly connected concepts
- Isolated nodes indicate orphan pages (no connections)
- Distance between nodes suggests relationship strength

**Interactive features:**
- Click nodes to open pages
- Filter by tags or search terms
- Zoom to see dense clusters or overview
- Real-time updates as LLM adds pages and links

**Evolution over time:**
- **Empty vault**: 4-5 scaffold files with no connections
- **After first ingest**: Source connects to extracted entities and concepts
- **Growing wiki**: Clusters form around core topics
- **Mature wiki**: Dense interconnected network with clear knowledge domains

## Key Parameters

- **Layout algorithm**: How nodes are positioned (force-directed, hierarchical)
- **Filter settings**: Which pages/tags to show or hide
- **Color schemes**: Visual coding by type, tag, or recency
- **Edge display**: Show all links, only strong links, or bidirectional only
- **Node size**: Uniform or scaled by number of connections

## When To Use

**During ingestion:**
- Watch real-time as new source creates connections
- See which existing concepts the source relates to
- Verify expected entities and concepts are being extracted
- Spot if source is isolated (may indicate poor extraction)

**For exploration:**
- Find central hub pages (many connections)
- Discover unexpected relationships between topics
- Navigate by visual proximity rather than search
- Understand domain structure at a glance

**For maintenance:**
- Identify orphan pages needing links or deletion
- Find isolated clusters that should connect
- Spot over-connected pages that may need splitting
- Visualize health of wiki structure

**For presentation:**
- Show growth of knowledge base over time
- Demonstrate interconnectedness of concepts
- Explain domain relationships to others

## Risks & Pitfalls

- **Over-reliance**: Visual clustering doesn't necessarily indicate semantic coherence
- **Clutter**: Very large wikis become hard to read in graph view
- **Orphan anxiety**: Not all orphans are bad - some pages are legitimately standalone
- **False connections**: Accidental links or over-linking creates misleading structure
- **Performance**: Very large graphs (1000+ nodes) can be slow to render
- **2D limitations**: Complex relationships may need 3D or alternative visualizations

## Related Concepts

- [[concepts/llm-knowledge-base]] — System that graph view visualizes
- [[concepts/wiki-maintenance]] — Uses graph view to find issues
- [[concepts/lint-workflow]] — Identifies orphans and missing connections
- [[concepts/persistent-artifact]] — The evolving structure that graph shows

## Sources

- [[summaries/claude-karpathy-second-brain-video]] — Graph view demonstration and evolution
- [[summaries/llm-wiki]] — Graph view as wiki navigation tool
