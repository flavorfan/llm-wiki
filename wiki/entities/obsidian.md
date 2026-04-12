---
title: "Obsidian"
type: entity
tags: [tools, markdown, knowledge-management]
created: 2026-04-10
updated: 2026-04-12
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md", "raw/Obsidian CLI.md", "raw/Obsidian 官方 CLI 命令全景速查表.md", "raw/Obsidian 必装 Skills.md"]
confidence: high
---

# Obsidian

## Overview

Obsidian is a markdown-based knowledge management application that serves as the primary "IDE frontend" for [[concepts/llm-knowledge-base]] systems. It provides viewing, navigation, and visualization capabilities for LLM-maintained wikis through features like graph view, vault management, and extensive plugin ecosystem.

**Leadership**:
- **CEO**: [[entities/steph-ango]] (kepano)
- **Co-founders**: Erica Xu, Shida Li

## Characteristics

**Core features:**
- **Vault system**: Isolated collections of markdown files and assets
- **[[concepts/graph-view]]**: Visual representation of page interconnections
- **Wiki links**: `[[page-name]]` syntax for cross-referencing
- **Live preview**: Real-time rendering of markdown
- **Local-first**: All data stored on device, no cloud dependency (unless opted in)
- **File system based**: Direct access to markdown files, git-compatible
- **[[concepts/obsidian-cli]]**: Official command-line interface (v1.12+) for AI agent integration
- **[[concepts/obsidian-bases]]**: Notion-like database views with filters, formulas, aggregations

**Extensions:**
- **[[concepts/obsidian-web-clipper]]**: Chrome extension to capture web articles as markdown
- **Marp plugin**: Render slide decks from markdown
- **Dataview plugin**: Query over page frontmatter and metadata
- **Image handling**: Hotkey to download remote images to local directory
- **Mobile app**: Sync vaults across devices (paid tier)
- **Maps plugin**: Geographic visualization for Bases map views
- **Excalidraw plugin**: Hand-drawn diagrams and sketches

**Settings for LLM wikis:**
- Set attachment folder path to fixed directory (e.g., `raw/assets/`)
- Configure web clipper to store in `raw/` directory
- Bind hotkey for "Download attachments for current file" (e.g., Ctrl+Shift+D)
- Enable CLI in Settings → General → Command line interface (v1.12+)

**Privacy Philosophy**:
- **Local-first architecture**: No mandatory cloud services
- **No forced AI integration**: Will never require cloud AI features
- **User sovereignty**: Users choose which AI frameworks to connect via CLI
- **Data ownership**: Complete control over personal data

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

- [[entities/steph-ango]] — CEO and creator of official Skills
- [[entities/andrej-karpathy]] — Popularized Obsidian for LLM wikis
- [[entities/claude-code]] — AI harness that edits Obsidian vaults
- [[entities/n8n]] — Automation tool that integrates with Obsidian CLI
- [[entities/peter-levels]] — Creator of summarize tool (web clipper alternative)
- [[entities/marp]] — Slide deck format with Obsidian plugin

## Sources

- [[summaries/llm-wiki]] — Obsidian as IDE concept and tips/tricks
- [[summaries/karpathy-x]] — Real-world Obsidian usage in workflow
- [[summaries/claude-karpathy-second-brain-video]] — Obsidian setup demonstration
- [[summaries/obsidian-cli-core-principles]] — CLI architecture and philosophy
- [[summaries/obsidian-cli-command-reference]] — Complete command catalog
- [[summaries/obsidian-essential-skills]] — Skills ecosystem
