---
title: "Obsidian"
type: entity
tags: [tools, markdown, knowledge-management]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# Obsidian

## Overview

Obsidian is a markdown-based knowledge management application that serves as the primary "IDE frontend" for [[concepts/llm-knowledge-base]] systems. It provides viewing, navigation, and visualization capabilities for LLM-maintained wikis through features like graph view, vault management, and extensive plugin ecosystem.

## Characteristics

**Core features:**
- **Vault system**: Isolated collections of markdown files and assets
- **[[concepts/graph-view]]**: Visual representation of page interconnections
- **Wiki links**: `[[page-name]]` syntax for cross-referencing
- **Live preview**: Real-time rendering of markdown
- **Local-first**: All data stored on device, no cloud dependency (unless opted in)
- **File system based**: Direct access to markdown files, git-compatible

**Extensions:**
- **[[concepts/obsidian-web-clipper]]**: Chrome extension to capture web articles as markdown
- **Marp plugin**: Render slide decks from markdown
- **Dataview plugin**: Query over page frontmatter and metadata
- **Image handling**: Hotkey to download remote images to local directory
- **Mobile app**: Sync vaults across devices (paid tier)

**Settings for LLM wikis:**
- Set attachment folder path to fixed directory (e.g., `raw/assets/`)
- Configure web clipper to store in `raw/` directory
- Bind hotkey for "Download attachments for current file" (e.g., Ctrl+Shift+D)

## Common Strategies

**As LLM Wiki IDE:**
1. **Human role**: Read and browse wiki, view visualizations, navigate graph
2. **LLM role**: Write and maintain all wiki files
3. **Collaboration model**: LLM edits on one side, human views in Obsidian on other

**Vault organization:**
- `raw/` — Source documents and assets (immutable)
- `wiki/` — LLM-maintained structured knowledge
- `outputs/` — Query results, reports, generated content

**Workflow integration:**
- Web clipper for rapid capture → `raw/`
- Mobile notes sync to vault
- [[concepts/loop-automation]] can monitor vault and auto-ingest
- Git repo for version control and collaboration

**Graph view usage:**
- Identify orphan pages (no connections)
- See knowledge clusters and hubs
- Visualize how new sources connect to existing knowledge
- Spot missing cross-references

## Related Entities

- [[entities/andrej-karpathy]] — Popularized Obsidian for LLM wikis
- [[entities/claude-code]] — AI harness that edits Obsidian vaults
- [[entities/peter-levels]] — Creator of summarize tool (web clipper alternative)
- [[entities/marp]] — Slide deck format with Obsidian plugin

## Sources

- [[summaries/llm-wiki]] — Obsidian as IDE concept and tips/tricks
- [[summaries/karpathy-x]] — Real-world Obsidian usage in workflow
- [[summaries/claude-karpathy-second-brain-video]] — Obsidian setup demonstration
