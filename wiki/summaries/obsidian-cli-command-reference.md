---
title: "Obsidian CLI Command Reference"
type: summary
tags: [obsidian, cli, reference, commands, documentation]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian 官方 CLI 命令全景速查表.md"]
confidence: high
---

## Key Points

- **Comprehensive command catalog**: Complete reference of Obsidian CLI commands (v1.12+) organized by functional module
- **Syntax rules**:
  - Basic format: `obsidian <command> param=value flags`
  - Values with spaces require double quotes: `content="Hello world"`
  - Flag parameters (like `open`, `inline`, `total`) don't need values - presence enables them
- **Command modules**: 25+ functional areas from basic file operations to developer tools

## Command Categories

**Core Operations**: `help`, `version`, `reload`, `restart`

**Files & Folders**: `create`, `read`, `append`, `prepend`, `move`, `rename`, `delete`, `open`, `files`, `folders`

**Daily Notes**: `daily`, `daily:path`, `daily:read`, `daily:append`, `daily:prepend`

**Search**: `search`, `search:context`, `search:open` (full-text retrieval with context)

**Links & Graph**: `backlinks`, `links`, `unresolved`, `orphans`, `deadends`

**Properties (YAML)**: `properties`, `property:set`, `property:remove`, `property:read`, `aliases`

**Databases (Bases)**: `bases`, `base:views`, `base:create`, `base:query`

**Tasks**: `tasks`, `task` (query and toggle task states)

**Plugins**: `plugins`, `plugin:enable`, `plugin:disable`, `plugin:install`, `plugin:uninstall`, `plugin:reload`

**History**: `history`, `history:read`, `history:restore`, `diff`

**Sync**: `sync`, `sync:status`, `sync:history`, `sync:restore` (official Obsidian Sync)

**Publish**: `publish:site`, `publish:list`, `publish:status`, `publish:add`, `publish:remove`

**Workspace**: `workspace`, `tabs`, `tab:open`, `recents`, `bookmarks`, `bookmark`

**Templates**: `templates`, `template:read`, `template:insert`

**Themes & Appearance**: `themes`, `theme:set`, `theme:install`, `snippets`

**Developer Tools**: `devtools`, `dev:debug`, `dev:cdp`, `dev:screenshot`, `dev:console`, `dev:dom`, `dev:mobile`, `eval`

**Other**: `tags`, `outline`, `wordcount`, `random`, `unique` (Zettelkasten timestamp), `web` (embedded browser), `commands`, `hotkeys`

## Automation Workflow Examples

**Workflow 1 - Flash Capture**: Bind `obsidian daily:append` to launcher (Raycast/Alfred) for instant note capture without opening UI

**Workflow 2 - Media Knowledge Extraction**: AI extracts YouTube captions → creates note with template → inserts action items into daily note

**Workflow 3 - AI Inbox Sorting**: n8n scheduled task → AI reads Inbox files → normalizes YAML properties → moves files safely (preserving wikilinks)

**Workflow 4 - Local RAG Assistant**: AI uses `search:context` + `backlinks` + `read` to construct context without vector database or embeddings

**Workflow 5 - Database Integration**: External webhooks → CLI creates Bases records with typed fields (numbers, dates)

**Workflow 6 - Historical Review**: Daily script → `random:read` from >1 year ago → AI cross-links with recent tags → prepend to daily note

**Workflow 7 - Bulk Metadata Cleaning**: AI script traverses folders → reads properties → normalizes values → batch `property:set` updates

## Relevant Concepts

- [[concepts/obsidian-cli]] — Architecture and principles
- [[concepts/automation-workflows]] — Practical applications
- [[concepts/agent-skills]] — How AI agents use these commands

## Source Metadata

- **Type**: Reference documentation / cheat sheet
- **Language**: Chinese
- **Author**: Anonymous/community
- **Format**: Comprehensive table with 90+ command examples
- **Audience**: Developers and power users building CLI automation
