---
title: "Query Workflow"
type: concept
tags: [knowledge-synthesis, query, workflow, retrieval]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md"]
confidence: high
---

# Query Workflow

## Definition

The query workflow is the process of asking questions against the compiled wiki and generating answers with citations. Unlike traditional RAG systems that retrieve from raw sources at query time, this workflow leverages the pre-compiled, cross-referenced wiki structure. Importantly, valuable query outputs can be filed back into the wiki as new pages, causing explorations to compound in the knowledge base.

## How It Works

**Standard query steps:**

1. **Read index**: LLM consults `wiki/index.md` to identify relevant pages
2. **Navigate to pages**: Read the identified pages in detail
3. **Follow cross-references**: Use wiki links to explore related concepts and entities
4. **Synthesize answer**: Generate response drawing from multiple pages
5. **Cite sources**: Include wiki links showing which pages informed the answer
6. **Evaluate value**: Determine if answer contains insights worth preserving
7. **File back** (optional): If valuable, create new wiki page (synthesis, comparison, analysis)
8. **Update index and log**: If new page created, add to navigation structure

**Query answer formats:**

- **Text**: Markdown page with synthesis and citations
- **Comparison**: Table or structured comparison (filed as synthesis page)
- **Slides**: Marp format presentation from wiki content
- **Visualizations**: Matplotlib charts, graphs, diagrams
- **Canvas**: Visual layouts (in Obsidian)

## Key Parameters

- **Search strategy**:
  - **Index-based**: Read index file to find pages (works to ~100 sources)
  - **Search tool**: Use [[concepts/search-engines]] like qmd for larger wikis
  - **Graph navigation**: Follow links from known relevant pages

- **Depth**: How many pages and cross-references to read
- **Filing threshold**: Which answers are valuable enough to preserve as wiki pages
- **Output format**: How to present the answer (text, slides, charts)
- **Citation style**: How explicitly to link back to source pages

## When To Use

**Ideal query types:**

- **Synthesis questions**: "How do concepts X and Y relate?"
- **Comparison questions**: "What are the trade-offs between approach A and B?"
- **Timeline questions**: "How has thinking on X evolved across these sources?"
- **Gap analysis**: "What aspects of X haven't been covered yet?"
- **Decision support**: "Given constraints Y and Z, which approach should I use?"
- **Connection discovery**: "Where does concept X appear across the wiki?"

**Filing answers back to wiki when:**

- Answer required synthesizing multiple sources in non-obvious way
- Created comparison or framework that will be useful repeatedly
- Discovered connections that should be preserved
- Generated visualization that aids understanding
- Answered question others might ask similarly

## Risks & Pitfalls

- **Index staleness**: If index isn't maintained, relevant pages won't be found
- **Over-filing**: Creating too many synthesis pages from routine queries clutters wiki
- **Citation overhead**: Too many citations make answers hard to read
- **Search limitations**: Index-based search eventually breaks down at scale
- **Context loss**: Filing answer without preserving the question context reduces value
- **Duplicate synthesis**: May create redundant synthesis pages if not checking existing pages first
- **Hallucination risk**: LLM may claim connections between pages that don't actually exist

## Related Concepts

- [[concepts/llm-knowledge-base]] — System that query workflow operates on
- [[concepts/persistent-artifact]] — Why filing queries back compounds value
- [[concepts/search-engines]] — Tools for finding relevant pages at scale
- [[concepts/output-formats]] — Different ways to present query results
- [[concepts/index-files]] — Primary navigation mechanism for queries
- [[concepts/ingest-workflow]] — How knowledge gets into wiki to query against

## Sources

- [[summaries/llm-wiki]] — Query workflow and filing back concept
- [[summaries/karpathy-x]] — Output formats and explorations compounding
