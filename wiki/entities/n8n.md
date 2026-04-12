---
title: "n8n"
type: entity
tags: [tools, automation, workflow, no-code]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian CLI.md", "raw/Obsidian 官方 CLI 命令全景速查表.md"]
confidence: high
---

## Overview

n8n is a workflow automation tool (similar to Zapier or Make) that can be self-hosted and integrated with [[concepts/obsidian-cli]] to build automated knowledge management workflows.

## Characteristics

**Deployment Models**:
- **Local installation**: Required for Obsidian CLI integration (Docker versions can't access local file system)
- **Self-hosted**: Full control over data and workflows
- **Cloud**: Also available as SaaS, but local is required for Obsidian integration

**Architecture**:
- Node-based visual workflow builder
- Execute Command node: Can run CLI commands including `obsidian` commands
- Webhook support: Can receive external triggers
- Scheduled triggers: Cron-like time-based automation

**Security Model**:
- v2.x disables file system and shell nodes by default for safety
- Override required for Obsidian workflows: `set NODES_EXCLUDE=[] && n8n start`

## Common Use Cases with Obsidian

**Inbox Sorting** ([[summaries/obsidian-cli-command-reference]] Workflow 3):
- Scheduled task reads files in Inbox folder
- AI agent analyzes content
- Normalizes YAML properties
- Moves files to correct folders (preserving wikilinks)

**External Data Integration** (Workflow 5):
- Receives webhook (e.g., bank transaction SMS)
- Parses data fields
- Creates Obsidian Bases record via CLI
- Sets typed properties (numbers, dates)

**Media Processing** (Workflow 2):
- Monitors YouTube/podcast RSS feeds
- Extracts transcripts/metadata
- Creates notes using templates
- Inserts action items into daily notes

**Scheduled Review** (Workflow 6):
- Daily trigger at specific time
- Fetches random old note (>1 year ago)
- AI generates cross-links with recent tags
- Prepends insight to today's daily note

## Setup for Obsidian Integration

**1. Install n8n locally**:
```bash
npm install n8n -g
```

**2. Enable all nodes** (required for shell commands):
```bash
set NODES_EXCLUDE=[] && n8n start
```

**3. Configure Execute Command node**:
```
Command: python
Arguments: C:\path\to\script.py
# or
Command: obsidian
Arguments: daily:append content="Test"
```

**4. Handle encoding** (Windows UTF-8 issues):
```bash
set PYTHONIOENCODING=utf-8 && n8n start
```

## When To Use

**n8n vs. Direct Scripts**:
- **Use n8n when**: Complex multi-step workflows, need visual debugging, external webhook triggers, multiple integrations (email + Obsidian + database)
- **Use direct scripts when**: Simple scheduled tasks, one-off operations, already comfortable with cron/Task Scheduler

**n8n vs. Agent Skills**:
- **n8n**: Deterministic, scheduled, same operation repeatedly (daily inbox sort)
- **Agent Skills**: Dynamic, context-dependent, different each time (AI decides what to do)

## Risks & Pitfalls

**Local Requirement**: Must be installed locally to access file system and execute Obsidian CLI. Docker deployments cannot interact with local Obsidian.

**UTF-8 Encoding**: Windows users may encounter encoding errors with Chinese/special characters. Must set `PYTHONIOENCODING=utf-8` environment variable.

**Resource Usage**: n8n runs continuously when active, consuming system resources. Consider startup scripts for on-demand use.

**Complexity Overhead**: For simple tasks (one command), n8n adds unnecessary complexity. Direct cron/Task Scheduler more appropriate.

**Security**: Disabling node restrictions (`NODES_EXCLUDE=[]`) removes safety guardrails. Only do this if you trust all workflows.

## Related Concepts

- [[concepts/obsidian-cli]] — Primary integration point
- [[concepts/automation-workflows]] — Pattern n8n implements
- [[concepts/llm-knowledge-base]] — Can automate maintenance workflows

## Related Entities

- [[entities/obsidian]] — Target of automation
- [[entities/claude-code]] — Alternative approach (AI agent vs deterministic workflow)

## Sources

- [[summaries/obsidian-cli-core-principles]] — Integration examples
- [[summaries/obsidian-cli-command-reference]] — Workflow patterns
