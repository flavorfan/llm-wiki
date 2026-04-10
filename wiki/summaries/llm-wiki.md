---
title: "LLM Wiki Pattern - Idea File"
type: summary
tags: [foundational, knowledge-synthesis, llm-agents, obsidian, markdown]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md"]
confidence: high
---

# LLM Wiki Pattern - Idea File

## Key Points

- **Core innovation**: LLMs incrementally build and maintain a persistent wiki rather than retrieving from raw documents on every query. Knowledge is compiled once and kept current, not re-derived each time.
- **Three-layer architecture**: Raw sources (immutable), the wiki (LLM-maintained markdown), and the schema (instructions for the LLM on structure and workflows).
- **Key workflows**: Ingest (process new sources), Query (ask questions and file answers back), Lint (health-check for contradictions and gaps).
- **Persistent artifact**: The wiki compounds over time. Cross-references are already there, contradictions flagged, synthesis evolves with each source.
- **Human-LLM collaboration**: Humans curate sources and ask questions; LLMs handle all the tedious bookkeeping, cross-referencing, and maintenance.
- **Works at moderate scale**: With index files and brief summaries, LLMs can navigate ~100 sources and ~400K words without needing RAG infrastructure.
- **Versatile applications**: Personal knowledge, research, reading companion wikis, business intelligence, competitive analysis, course notes.
- **Obsidian as IDE**: View raw data, compiled wiki, and visualizations. The LLM writes/maintains; humans read and direct.
- **Git-compatible**: The wiki is just markdown files, so version control, branching, and collaboration work naturally.
- **Inspired by Memex**: Related to Vannevar Bush's 1945 vision of personal, curated knowledge stores with associative trails between documents.

## Relevant Concepts

- [[concepts/llm-knowledge-base]]
- [[concepts/wiki-maintenance]]
- [[concepts/knowledge-compilation]]
- [[concepts/ingest-workflow]]
- [[concepts/query-workflow]]
- [[concepts/lint-workflow]]
- [[concepts/persistent-artifact]]
- [[concepts/index-files]]
- [[concepts/schema-file]]

## Source Metadata

- **Type**: Idea file / pattern documentation
- **Author**: Andrej Karpathy (implied, based on pattern origination)
- **Date**: 2026 (approximate, based on references)
- **Format**: Markdown documentation
- **Purpose**: Abstract description of LLM Wiki pattern for copy-pasting to LLM agents
- **Scope**: Intentionally abstract - describes idea, not specific implementation
