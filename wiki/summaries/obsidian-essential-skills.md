---
title: "Obsidian Essential Skills"
type: summary
tags: [obsidian, skills, ai-agents, claude-code, plugins]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian 必装 Skills.md"]
confidence: high
---

## Key Points

- **Skills overview**: Curated catalog of essential Skills for AI agents working with Obsidian
- **Two skill paradigms**:
  - **Official CLI-based** (kepano): Skills that call Obsidian CLI (modern, token-efficient, recommended)
  - **Direct file I/O** (OpenClaw legacy): Skills that manipulate files directly (deprecated, token-heavy)
- **Installation methods**: BRAT (Beta Reviewers Auto-updater Tool) for auto-updates, or manual installation
- **Plugin ecosystem**: Complementary plugins (Claudian, obsidian-agent-client) enable richer AI interactions

## Essential Skills by Author

### Obsidian CEO (kepano/Steph Ango)

GitHub: `kepano/obsidian-skills`

| Skill | Status | Function |
|-------|--------|----------|
| **defuddle** | ✅ Recommended | Web scraping to clean Markdown, removes ads/navigation, saves tokens. Supports YouTube transcripts via official API |
| **obsidian-cli** | ✅ Recommended | Enables AI agents to call Obsidian CLI for CRUD operations, task management, plugin debugging |
| **obsidian-bases** | ✅ Recommended | Create/edit .base files (Notion-like database views with filters, formulas, summaries) |
| **obsidian-markdown** | ⚠️ Use with caution | Write Obsidian-flavored Markdown (wikilinks, embeds, callouts, properties). Customizable for personal style |
| **json-canvas** | ❌ Deprecated | Create .canvas whiteboard files. Superseded by improved alternatives |

### Axton (axtonliu)

GitHub: `axtonliu/axton-obsidian-visual-skills`

| Skill | Status | Function |
|-------|--------|----------|
| **obsidian-canvas-creator** | ✅ Recommended | Enhanced canvas creation solving node overlap issues. Supports MindMap and freeform layouts with automatic coordinate calculation |
| **mermaid-visualizer** | ✅ Recommended | Text → Mermaid diagrams with Obsidian syntax error correction |
| **excalidraw-diagram** | ✅ Recommended | Text → hand-drawn Excalidraw diagrams. Supports Obsidian .md, standard .excalidraw, animated modes |

### RoundTable02

GitHub: `RoundTable02/tutor-skills`

| Skill | Status | Function |
|-------|--------|----------|
| **tutor-setup + tutor** | ✅ Recommended | Complete learning system: converts documents/code → Obsidian StudyVault with quizzes. Tracks knowledge gaps and learning progress |

### EESJGong

GitHub: `EESJGong/scholar-skill`

| Skill | Status | Function |
|-------|--------|----------|
| **scholar-skill** | ✅ Recommended | Academic research workflow: L1-L3 tiered paper reading (fast scan → standard → deep analysis). Auto-generates structured notes with memory/conflict tracking. **WARNING**: Extremely token-intensive (2.5+ hour L3 loops), uses direct file I/O (risk of data corruption during sync) |

### OpenClaw (legacy)

GitHub: `openclaw/openclaw/skills/obsidian`

| Skill | Status | Function |
|-------|--------|----------|
| **obsidian-skill** | ❌ Deprecated | Direct file system I/O. Obsolete now that official CLI exists. High token cost |

## Core Plugins

### Claudian

- **Repo**: `YishenTu/claudian`
- **Status**: Third-party, not in official marketplace yet
- **Function**: Native Claude integration in Obsidian
- **Installation**: Via BRAT or manual
- **Configuration**: Supports custom models (智谱GLM, DeepSeek) via Anthropic-compatible API endpoints

### obsidian-agent-client

- **Repo**: `RAIT-09/obsidian-agent-client`
- **Status**: Third-party, not in official marketplace
- **Function**: Multi-agent support (Claude Code, Codex, Gemini CLI, OpenCode, Qwen Code)
- **Setup**: Configure agent path and arguments (including CWD to vault path)

## Skill Dependencies

**defuddle**: Requires Node.js + `npm install -g defuddle`

**obsidian-bases**: Requires Maps plugin for map view support

**excalidraw-diagram**: Requires Excalidraw plugin installed

**scholar-skill**: Requires Python, OpenClaw framework, and multiple dependent Skills (obsidian-direct, arxiv-watcher, durable-task-runner)

## Usage Notes

- **Token consumption**: CLI-based skills (~100 tokens) vs file I/O skills (scan entire vault, millions of tokens)
- **Customization**: obsidian-markdown skill can embed personal formatting preferences
- **Risk awareness**: scholar-skill can cost $100+ per deep paper analysis if using frontier models
- **Installation**: BRAT recommended for skills under active development (auto-updates)

## Relevant Concepts

- [[concepts/agent-skills]] — Skill system architecture
- [[concepts/obsidian-cli]] — Underlying CLI these skills use
- [[concepts/defuddle]] — Web scraping tool
- [[concepts/tutor-system]] — Learning loop with quizzes
- [[concepts/scholar-workflow]] — Academic research automation

## Source Metadata

- **Type**: Curated catalog / installation guide
- **Language**: Chinese
- **Author**: Anonymous/community (appears to be user documentation)
- **Date**: ~2026 (references current tool ecosystem)
- **Audience**: Users setting up Claude Code or OpenCode with Obsidian
