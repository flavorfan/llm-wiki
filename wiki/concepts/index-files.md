---
title: "Index Files"
type: concept
tags: [indexing, navigation, knowledge-synthesis]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md"]
confidence: high
---

# Index Files

## Definition

Index files are special wiki pages that catalog all other pages in the knowledge base, providing a content-oriented navigation structure. The primary index (`index.md`) lists every wiki page with a link, one-line summary, and metadata (category, date, tags, confidence). This allows the LLM (and humans) to discover relevant pages without requiring embedding-based search at moderate scale (~100 sources, ~400K words).

## How It Works

**Primary index structure (index.md):**

```markdown
## Concepts
| Page | Tags | Confidence | Updated |
|------|------|------------|---------|
| [[concepts/concept-name]] | tag1, tag2 | high | 2026-04-10 |

## Entities
| Page | Tags | Updated |
|------|------|---------|
| [[entities/entity-name]] | tag1, tag2 | 2026-04-10 |

## Summaries
| Page | Source | Key Topics | Created |
|------|--------|------------|---------|
| [[summaries/summary-name]] | raw/source.md | topic1, topic2 | 2026-04-10 |

## Statistics
- Total pages: 42
- High confidence: 30
- Sources ingested: 15
```

**Query workflow:**

1. LLM reads index.md to find relevant pages by scanning summaries and tags
2. Identifies 3-10 candidate pages
3. Reads those pages in detail
4. Follows cross-references to related pages
5. Synthesizes answer with citations

**Maintenance:**

- Updated on every [[concepts/ingest-workflow]]
- Add new pages to appropriate section
- Update counts in statistics section
- Ensure all pages appear (no orphans in index)
- Keep summaries concise (one line per page)

## Key Parameters

- **Organization**: How to categorize pages (by type, topic, recency)
- **Summary length**: One line vs. paragraph per page
- **Metadata**: What fields to include (tags, confidence, dates, source count)
- **Update frequency**: On every change vs. periodic regeneration
- **Search aid**: Whether to include keywords for common queries

## When To Use

**Index-based navigation works when:**

- Wiki has ~10-200 pages
- Categories are well-defined (concepts, entities, summaries, syntheses)
- Queries map clearly to categories ("who is X" → entities, "how does Y work" → concepts)
- One-line summaries sufficiently describe content
- Tag system provides useful filtering

**Need to augment index with search when:**

- Wiki exceeds ~200 pages
- Queries require full-text search across page content
- Summaries too brief to determine relevance
- Need semantic similarity beyond keyword matching
- Want to search within specific sections of pages

**Complementary to:**

- **Log file**: Chronological vs. content view
- **Graph view**: Visual vs. textual navigation
- **Search tools**: Precise vs. exploratory discovery
- **Tag system**: Thematic vs. structural grouping

## Risks & Pitfalls

- **Stale index**: If not updated on every change, becomes misleading
- **Summary drift**: One-line summaries may not reflect page evolution
- **Categorization ambiguity**: Some pages fit multiple categories
- **Scalability limits**: Index becomes unwieldy beyond ~200 pages
- **Search bias**: LLM may over-rely on index summaries and miss nuances in pages
- **Maintenance burden**: Manual index updates error-prone (should be automated)

## Related Concepts

- [[concepts/llm-knowledge-base]] — System that index navigates
- [[concepts/query-workflow]] — Primary consumer of index
- [[concepts/ingest-workflow]] — Updates index on every source
- [[concepts/search-engines]] — Complementary tool for larger wikis
- [[concepts/wiki-maintenance]] — Includes keeping index current

## Sources

- [[summaries/llm-wiki]] — Index files description and role in navigation
