---
title: "Output Formats"
type: concept
tags: [query, formatting, presentation, workflow]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/karpathy-x.md"]
confidence: medium
---

# Output Formats

## Definition

Output formats are structured ways of presenting query results from an LLM wiki. Rather than free-form prose responses, the LLM can be instructed to return information in specific formats optimized for different use cases.

## How It Works

When querying an LLM wiki, the user or system can specify an output format:
- **Prose summary** — paragraph-form explanation with citations
- **Bullet points** — concise list of key facts
- **Table/comparison** — structured data comparing multiple entities or concepts
- **Code snippets** — extracted code examples with context
- **JSON/structured data** — machine-readable output for programmatic use
- **Flashcards** — Q&A pairs for spaced repetition learning
- **Diagrams** — visual representations (Mermaid, Excalidraw)

The query workflow can be templated to automatically apply the desired format.

## Key Parameters

- **Format specification** — syntax or template for the desired output
- **Citation style** — how sources are referenced (wiki links, footnotes, inline)
- **Verbosity level** — brief vs detailed responses
- **Structure enforcement** — strict schema vs flexible formatting

## When To Use

Different formats serve different purposes:
- **Learning** → flashcards, summaries with examples
- **Decision-making** → comparison tables, pros/cons lists
- **Integration** → JSON, structured data for downstream tools
- **Sharing** → polished prose, presentations, diagrams
- **Development** → code snippets with explanations

## Risks & Pitfalls

- **Over-specification** — too rigid formats may constrain useful information
- **Format drift** — LLM may not perfectly follow format instructions
- **Context loss** — highly structured formats may omit important nuance
- **Maintenance burden** — custom formats require clear documentation

## Related Concepts

- [[concepts/query-workflow]] — Uses output formats to structure responses
- [[concepts/index-files]] — Structured format for navigation
- [[wiki/presentations/]] — Marp slide decks as a specific output format

## Sources

- raw/karpathy-x.md — Mentions output format specifications in query workflow
