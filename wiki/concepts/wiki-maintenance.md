---
title: "Wiki Maintenance"
type: concept
tags: [maintenance, knowledge-synthesis, foundational]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md"]
confidence: high
---

# Wiki Maintenance

## Definition

Wiki maintenance is the ongoing bookkeeping work required to keep a knowledge base healthy, consistent, and useful over time. This includes updating cross-references, keeping summaries current, noting contradictions, maintaining [[concepts/index-files]], resolving conflicts, and ensuring all pages link properly. In the [[concepts/llm-knowledge-base]] pattern, LLMs perform this tedious work that humans typically abandon.

## How It Works

**Continuous maintenance:**

- **During [[concepts/ingest-workflow]]**:
  - Update existing entity and concept pages with new information
  - Add cross-links between new summary and related pages
  - Update index.md with new entries
  - Append to log.md with changes made
  - Flag contradictions between new and existing content

**Periodic maintenance ([[concepts/lint-workflow]]):**

- Find and fix orphan pages (no inbound links)
- Identify contradictions between pages
- Update stale claims superseded by newer sources
- Add missing cross-references
- Fill incomplete sections
- Strengthen low-confidence pages with additional research
- Prune or archive very low-value content

**Navigation structure:**

- Keep index.md current with all pages
- Maintain log.md as append-only history
- Update statistics and metadata
- Ensure consistent frontmatter across pages

## Key Parameters

- **Automation level**: How much maintenance happens automatically vs. requiring human approval
- **Update frequency**: Continuous (on every change) vs. periodic (weekly/monthly)
- **Conflict resolution**: Flag for human vs. auto-resolve with citation
- **Link density**: How aggressively to cross-reference related pages
- **Pruning threshold**: When to delete vs. archive vs. keep low-value pages

## When To Use

**Why LLMs excel at maintenance:**

Traditional wikis fail because "the tedious part of maintaining a knowledge base is not the reading or the thinking — it's the bookkeeping. Updating cross-references, keeping summaries current, noting when new data contradicts old claims, maintaining consistency across dozens of pages. Humans abandon wikis because the maintenance burden grows faster than the value."

LLMs don't:
- Get bored with repetitive bookkeeping
- Forget to update cross-references
- Lose track of which pages need updates
- Find it costly to touch 15 files in one pass

Result: "The wiki stays maintained because the cost of maintenance is near zero."

**Human role shifts to:**

- Curate sources (decide what to ingest)
- Direct analysis (what to emphasize)
- Ask good questions
- Think about what it all means
- Resolve ambiguities and contradictions
- Make strategic decisions about structure

**LLM role is everything else:**

- Read sources completely
- Extract entities and concepts
- Write and update pages
- Maintain cross-references
- Keep index current
- Log all changes
- Flag issues for human attention

## Risks & Pitfalls

- **Automation errors**: LLM may create incorrect cross-references or misinterpret contradictions
- **Maintenance creep**: Too much auto-maintenance can churn content unnecessarily
- **Context loss**: Aggressive pruning may delete valuable historical content
- **Link bloat**: Over-eager cross-referencing creates noise
- **False conflicts**: Flagging valid differences as contradictions
- **Maintenance theater**: Doing maintenance for its own sake rather than improving usefulness

## Related Concepts

- [[concepts/llm-knowledge-base]] — System requiring this maintenance
- [[concepts/lint-workflow]] — Periodic maintenance process
- [[concepts/ingest-workflow]] — Continuous maintenance during ingestion
- [[concepts/persistent-artifact]] — What maintenance keeps valuable
- [[concepts/index-files]] — Key structure requiring maintenance

## Sources

- [[summaries/llm-wiki]] — Why maintenance is the key bottleneck LLMs solve
