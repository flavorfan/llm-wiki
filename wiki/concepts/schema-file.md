---
title: "Schema File"
type: concept
tags: [foundational, llm-agents, configuration]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md"]
confidence: high
---

# Schema File

## Definition

The schema file (e.g., `CLAUDE.md` for [[entities/claude-code]], `AGENTS.md` for other harnesses) is the configuration document that tells the LLM how the wiki is structured, what the conventions are, and what workflows to follow when ingesting sources, answering questions, or maintaining the wiki. This is what transforms a generic LLM into a disciplined wiki maintainer.

## How It Works

**Core schema contents:**

1. **Purpose and philosophy**: What this knowledge base is for, core principles
2. **Directory structure**: Layout of `raw/`, `wiki/`, `outputs/`, subdirectories
3. **File naming conventions**: Lowercase, hyphens, slug matching title
4. **Page format**: Frontmatter fields (title, type, tags, dates, sources, confidence)
5. **Required sections**: What sections each page type must include
6. **Linking conventions**: How to create wiki links, when to link
7. **Tagging taxonomy**: Standard tags for categorization
8. **Workflows**: Step-by-step instructions for ingest, query, lint operations
9. **Rules**: Hard constraints (never modify `raw/`, always update index, etc.)

**Example structure from sources:**

```markdown
# Purpose
LLM-maintained knowledge base on [topic]. LLM writes/maintains wiki/, human curates raw/.

# Directory Layout
- raw/ — Immutable sources
- wiki/index.md — Master catalog
- wiki/log.md — Activity log
- wiki/concepts/ — Concept pages
- wiki/entities/ — Entity pages
- wiki/summaries/ — Source summaries

# Page Format
Every page has frontmatter: title, type, tags, dates, sources, confidence

# Workflows
[Detailed ingest workflow steps]
[Detailed query workflow steps]
[Detailed lint workflow steps]
```

## Key Parameters

- **Abstraction level**: How prescriptive vs. flexible
  - Rigid: Exact formats, required fields, strict workflows
  - Flexible: Guidelines and principles, adapt to context

- **Domain specificity**: Generic vs. tailored
  - Generic: Works for any knowledge domain
  - Specific: Optimized for research, business, personal, etc.

- **Evolving vs. static**: Whether schema co-evolves with wiki
  - Static: Set once, rarely changed
  - Dynamic: Refined based on what works in practice

- **Workflow detail**: How step-by-step to be
  - High-level: Principles and goals
  - Detailed: Exact commands and sequence

## When To Use

**Schema file is essential because:**

- **Consistency**: Ensures all pages follow same format
- **Completeness**: LLM knows what sections to include
- **Correctness**: Rules prevent common errors (modifying raw/, forgetting index updates)
- **Quality**: Standards like confidence levels and cross-linking maintain quality
- **Maintainability**: Future sessions can understand and work with existing structure
- **Collaboration**: Multiple humans or LLMs can work with same conventions

**Without schema:**

- LLM uses generic wiki conventions (may not fit your needs)
- Inconsistent page formats make navigation harder
- Important workflows (like updating index) may be forgotten
- Quality degrades over time as structure drifts

**Schema co-evolution:**

You and LLM refine schema over time as you discover what works:
- Initial: Start with template or adapt from idea file
- Learning: Try workflows, see what's clunky or missing
- Refinement: Update schema based on experience
- Stabilization: Eventually settles on conventions that work

## Risks & Pitfalls

- **Over-specification**: Too rigid schema constrains natural evolution
- **Under-specification**: Too vague, LLM makes inconsistent choices
- **Premature optimization**: Defining elaborate structure before understanding domain
- **Schema drift**: Schema file out of sync with actual wiki conventions
- **Compatibility issues**: Schema specific to one AI harness may not work with others
- **Maintenance burden**: Complex schema harder to evolve and maintain

## Related Concepts

- [[concepts/llm-knowledge-base]] — System that schema configures
- [[concepts/wiki-maintenance]] — Workflows that schema defines
- [[concepts/ingest-workflow]] — Key workflow documented in schema
- [[concepts/persistent-artifact]] — What schema helps maintain

## Sources

- [[summaries/llm-wiki]] — Schema as third layer of architecture
