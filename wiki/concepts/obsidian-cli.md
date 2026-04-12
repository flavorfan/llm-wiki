---
title: "Obsidian CLI"
type: concept
tags: [obsidian, cli, tools, ai-agents, token-optimization]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian CLI.md", "raw/Obsidian 官方 CLI 命令全景速查表.md"]
confidence: high
---

## Definition

Obsidian CLI is the official command-line interface for [[entities/obsidian]] (v1.12+), designed to allow AI agents and automation tools to interact with Obsidian vaults through the running Obsidian process rather than direct file system access.

## How It Works

**Architecture**: Instead of reading/writing Markdown files directly on disk, the CLI communicates with a running Obsidian process via inter-process communication. This gives access to Obsidian's internal:
- Knowledge graph index
- Backlink database
- Plugin state and APIs
- File metadata cache
- Zettelkasten unique ID system

**Token Efficiency**: The key innovation is that AI agents can query Obsidian's pre-built indices with ~100 tokens instead of scanning entire vault contents (potentially millions of characters). Example:
- Traditional approach: Agent reads all files to find backlinks → 50,000+ tokens
- CLI approach: `obsidian backlinks file=Note` → ~100 tokens

**Setup Process**:
1. Update Obsidian to v1.12 or higher
2. Settings → General → Command line interface (toggle on)
3. Confirm PATH registration
4. Keep Obsidian running (will auto-start if closed)
5. Test: `obsidian daily` should open/create today's daily note

**Command Syntax**:
```bash
obsidian <command> param=value flags
```
- Values with spaces need quotes: `content="Hello world"`
- Flag parameters don't need values: `open`, `inline`, `total`

## Key Command Categories

**File Operations**: `create`, `read`, `append`, `prepend`, `move`, `rename`, `delete`

**Daily Notes**: `daily`, `daily:read`, `daily:append` (fastest way to capture thoughts)

**Search**: `search`, `search:context` (full-text with surrounding lines)

**Graph Navigation**: `backlinks`, `links`, `unresolved`, `orphans`, `deadends`

**Properties**: `property:set`, `property:read`, `property:remove` (atomic YAML updates)

**Databases**: `base:create`, `base:query` (Obsidian Bases feature)

**Developer Tools**: `eval`, `dev:screenshot`, `dev:dom`, `dev:console` (debugging)

Full reference: [[summaries/obsidian-cli-command-reference]]

## When To Use

**Ideal for**:
- AI agent integration (Claude Code, OpenCode, Gemini CLI)
- Scheduled automation (Python scripts, cron jobs)
- Workflow tools (n8n, Zapier, Make)
- Flash capture (launcher shortcuts)
- Bulk metadata operations (normalizing YAML across vault)
- Avoiding broken wikilinks (CLI auto-updates all references when files move)

**Not suitable for**:
- Offline vault manipulation (requires running Obsidian process)
- Server-side processing without GUI environment
- Situations where you want to avoid starting Obsidian

## Risks & Pitfalls

**Requires Running Process**: All commands need Obsidian to be running. For automated scripts on headless servers, this may be problematic.

**Version Dependency**: Only works with Obsidian 1.12+. Earlier versions don't have CLI support.

**Platform Differences**: Command availability and behavior may differ slightly between desktop platforms (Windows/Mac/Linux).

**Learning Curve**: Requires understanding which commands preserve graph integrity vs. which are destructive. Example: `delete permanent` bypasses trash - data unrecoverable.

**Concurrency**: If vault is being modified by multiple processes (CLI + manual edits + sync), race conditions possible. Use git versioning for safety.

## Related Concepts

- [[concepts/agent-skills]] — Skills that wrap CLI commands for AI agents
- [[concepts/token-optimization]] — How CLI reduces API costs dramatically
- [[concepts/automation-workflows]] — Practical automation patterns
- [[concepts/llm-knowledge-base]] — Pattern this tooling enables

## Sources

- [[summaries/obsidian-cli-core-principles]] — Architecture and integration
- [[summaries/obsidian-cli-command-reference]] — Complete command catalog
- [[summaries/obsidian-essential-skills]] — Skills that use CLI
