---
title: "Karpathy's Tweet on LLM Knowledge Bases"
type: summary
tags: [knowledge-synthesis, llm-agents, obsidian, retrieval, indexing]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/karpathy-x.md"]
confidence: high
---

# Karpathy's Tweet on LLM Knowledge Bases

## Key Points

- **Token shift**: Andrej Karpathy's recent token throughput going less into manipulating code, more into manipulating knowledge (markdown and images).
- **Five-stage workflow**: Data ingest → IDE (Obsidian) → Q&A → Output → Linting
- **Data ingest**: Index sources into raw/ directory, LLM compiles wiki with summaries, backlinks, categorization into concepts with linked articles.
- **Obsidian as IDE**: Frontend for viewing raw data, compiled wiki, and visualizations. LLM writes/maintains wiki; human rarely touches directly.
- **Q&A at scale**: Once wiki reaches ~100 articles and ~400K words, can ask complex questions. LLM auto-maintains index files and summaries - works without fancy RAG at this scale.
- **Output formats**: Markdown files, slide shows (Marp), matplotlib images - all viewable in Obsidian. Outputs can be filed back into wiki to enhance it for further queries.
- **Linting**: LLM health checks find inconsistent data, impute missing data with web search, find connections for new article candidates, enhance data integrity.
- **Extra tools**: Developing custom tools like naive search engines over wiki (web UI + CLI for LLM).
- **Future**: Natural desire for synthetic data generation + finetuning to have LLM "know" data in weights instead of context windows.
- **Web Clipper**: Uses Obsidian Web Clipper extension to convert web articles to markdown.
- **Explorations compound**: Own queries always "add up" in the knowledge base rather than disappearing into chat history.

## Relevant Concepts

- [[concepts/llm-knowledge-base]]
- [[concepts/ingest-workflow]]
- [[concepts/query-workflow]]
- [[concepts/lint-workflow]]
- [[concepts/obsidian-web-clipper]]
- [[concepts/output-formats]]
- [[concepts/search-engines]]
- [[concepts/knowledge-compilation]]

## Source Metadata

- **Type**: Social media post (X/Twitter)
- **Author**: Andrej Karpathy
- **Date**: Recent (exact date not specified in source)
- **Format**: Text post
- **Context**: Description of personal workflow for building knowledge bases with LLMs
- **Scale mentioned**: ~100 articles, ~400K words in example research wiki
