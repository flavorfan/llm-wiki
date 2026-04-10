---
title: "Lint Workflow"
type: concept
tags: [knowledge-synthesis, maintenance, workflow, quality]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# Lint Workflow

## Definition

The lint workflow (also called "health check") is a periodic process where the LLM reviews the wiki to find issues and opportunities for improvement. Unlike code linting which checks syntax, wiki linting checks for inconsistent data, contradictions between pages, missing cross-references, orphaned pages, staleness, and gaps that could be filled with new research.

## How It Works

**Standard lint checks:**

1. **Orphan detection**: Pages with no inbound links from other pages
2. **Contradiction finding**: Claims that conflict between pages
3. **Staleness check**: Old claims superseded by newer sources
4. **Missing cross-references**: Related pages that should link to each other but don't
5. **Incomplete sections**: Pages missing expected sections per schema
6. **Low-confidence review**: Pages marked low-confidence that could be strengthened
7. **Gap analysis**: Important concepts mentioned but lacking dedicated pages
8. **Data imputation**: Missing data that could be filled with web search
9. **Connection discovery**: Interesting new relationships for article candidates

**Lint outputs:**

- **Must-fix errors**: Critical issues (contradictions, broken links)
- **Warnings**: Improvement opportunities (orphans, missing links)
- **Suggestions**: Ideas for new articles, sources to seek, questions to investigate
- **Auto-fixes**: Simple issues LLM can resolve immediately (add missing links, fill sections)
- **Reports**: List of issues requiring human judgment

## Key Parameters

- **Lint frequency**: Weekly, monthly, or after accumulating N sources
- **Auto-fix threshold**: Which issues LLM fixes automatically vs. flags for human
- **Gap depth**: How aggressively to suggest new articles and research directions
- **Web search**: Whether to impute missing data from web automatically
- **Confidence updates**: Whether to re-evaluate confidence levels based on corroboration
- **Pruning**: Whether to delete or archive very low-value pages

## When To Use

**Periodic linting** (recommended):

- After ingesting batch of related sources
- Monthly or quarterly maintenance
- Before major query/research sessions
- When wiki feels cluttered or inconsistent

**On-demand linting**:

- When you suspect contradictions exist
- After discovering errors in query results
- Before sharing wiki with others
- When preparing synthesis or output from wiki

**Continuous linting** (advanced):

- Lightweight checks on every ingest
- Automatic link suggestions during page creation
- Real-time contradiction detection

## Risks & Pitfalls

- **False positives**: LLM may flag valid differences as contradictions
- **Over-pruning**: Deleting pages that seem orphaned but are actually valuable
- **Suggestion overload**: Too many gap suggestions become overwhelming
- **Auto-fix errors**: Automatic corrections may introduce new problems
- **Context loss**: Removing "outdated" content may lose important historical context
- **Lint bloat**: Keeping detailed lint reports clutters the outputs
- **Web search drift**: Imputing data from web can introduce incorrect information
- **Perfectionism trap**: Spending too much time linting vs. adding new knowledge

## Related Concepts

- [[concepts/llm-knowledge-base]] — System that linting maintains
- [[concepts/wiki-maintenance]] — Broader category of upkeep work
- [[concepts/persistent-artifact]] — What linting keeps healthy over time
- [[concepts/ingest-workflow]] — Can accumulate issues that linting fixes
- [[concepts/graph-view]] — Visual tool for spotting orphans and clusters

## Sources

- [[summaries/llm-wiki]] — Lint workflow description and philosophy
- [[summaries/karpathy-x]] — Practical linting experience and health checks
- [[summaries/claude-karpathy-second-brain-video]] — Lint demonstration and gap finding
