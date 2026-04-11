---
title: "qmd"
type: entity
tags: [tools, search, markdown, local-first, shopify]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/LLM Wiki：让大模型替你打理知识库的完整指南.md"]
confidence: medium
---

# qmd

## Overview

qmd is a local markdown search engine created by Tobi Lutke, CEO of Shopify. It provides fast, intelligent search across markdown files using a hybrid approach: BM25 full-text search + vector semantic search + LLM reranking. Designed to run entirely locally without cloud APIs, it offers both CLI and MCP (Model Context Protocol) Server interfaces, making it accessible to both humans and LLM agents.

## Characteristics

- **Creator**: Tobi Lutke (Shopify CEO)
- **Purpose**: Local markdown search for wikis and knowledge bases
- **Search approach**: Hybrid three-stage pipeline
- **Privacy**: Fully local - no cloud APIs required
- **Interfaces**: CLI (human use) and MCP Server (LLM agent use)
- **Use case**: When LLM wiki scales beyond ~100 sources and simple index.md navigation

## How It Works

### Three-Stage Search Pipeline

1. **BM25 full-text search**: Traditional keyword matching, fast and precise
2. **Vector semantic search**: Embedding-based similarity for concept matching
3. **LLM reranking**: Local model re-orders results by relevance to query

**Advantage**: Combines precision of keywords with semantic understanding, all running on user's machine.

## When To Use

**Consider qmd when:**
- Wiki grows beyond a few hundred pages (~100+ sources as rough threshold)
- index.md becomes unwieldy to scan manually
- Need to search by concept/meaning not just exact keywords
- Want to preserve local-first, no-cloud philosophy
- LLM agent needs tool for targeted wiki search

**Stick with index.md when:**
- Wiki still small to medium (<100 sources, few hundred pages)
- You know roughly where things are via links and structure
- Simpler is better - fewer moving parts
- Don't want to manage additional search infrastructure

## Common Strategies

- **CLI usage**: `qmd "query string"` returns ranked markdown results
- **MCP Server mode**: LLM agent calls qmd as tool during query workflow
- **Integration with wiki**: Point qmd at wiki/ directory, search across all pages
- **Supplement, don't replace**: Use alongside [[concepts/index-files]] and [[concepts/knowledge-graph]] navigation

## Related Entities

- [[entities/andrej-karpathy]] - Mentioned qmd as tool for scaling LLM wiki
- [[entities/obsidian]] - Works alongside Obsidian's native search
- [[entities/claude-code]] - Can use qmd via MCP Server interface

## Related Concepts

- [[concepts/llm-knowledge-base]] - qmd helps scale wiki search as corpus grows
- [[concepts/index-files]] - Simpler alternative for small-to-medium wikis
- [[concepts/query-workflow]] - qmd enhances query step when wiki is large
- [[concepts/rag]] - qmd provides RAG-like search but over pre-compiled wiki, not raw sources

## Comparison to RAG Infrastructure

| Dimension | qmd | Traditional RAG |
|-----------|-----|-----------------|
| Scope | Local markdown files | Vector database of chunked documents |
| Deployment | Single tool, local binary | Infrastructure (embedding service, vector DB, API) |
| Search target | Wiki pages (pre-compiled) | Raw document chunks |
| Privacy | Fully local | Typically cloud-based |
| Complexity | Low - one tool | High - multiple components |
| LLM integration | MCP Server interface | Custom API integration |

**qmd philosophy**: Keep it simple and local, but add smart search when needed.

## Limitations

- **Requires local LLM**: For reranking stage, needs model running on user's machine
- **Initial setup**: More complex than just using text search in Obsidian
- **Markdown-specific**: Won't search PDFs, images, or other formats directly
- **Scale ceiling**: Eventually even qmd may struggle with 10,000+ page wikis

## Sources

- [[summaries/chinese-comprehensive-guide]] - "Tool Chain" section mentions qmd as optional scaling tool

## Context in LLM Wiki Ecosystem

qmd sits at the **scaling transition point**:
- Start simple: index.md + manual link following
- Medium scale: index.md + qmd for targeted search
- Large scale: qmd + potentially custom RAG over wiki

Most personal wikis never need qmd - hundreds of pages remain navigable via index + links. But having the option preserves the **local-first** principle even as scale grows, avoiding pressure to move to cloud-based search infrastructure.
