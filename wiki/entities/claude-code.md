---
title: "Claude Code"
type: entity
tags: [tools, llm-agents, claude, ai-harness, auto-research, skills-2-0]
created: 2026-04-10
updated: 2026-04-13
sources: ["raw/Claude + Karpathy's Second Brain is INSANE.md", "raw/llm-wiki.md", "raw/The only AutoResearch tutorial you'll ever need.md", "raw/Obsidian CLI.md", "raw/Obsidian 必装 Skills.md", "raw/claude-skills-2-how-to-use-skill-creator.md"]
confidence: high
---

# Claude Code

## Overview

Claude Code is Anthropic's AI agent harness (CLI tool) for software development and knowledge work. In the [[concepts/llm-knowledge-base]] context, it serves as the AI that writes and maintains wiki files, processes sources through [[concepts/ingest-workflow]], answers queries, and performs [[concepts/lint-workflow]] health checks.

## Characteristics

**Core capabilities:**
- Read and write markdown files
- Execute workflows via skills
- Maintain file structures and cross-references
- Process multiple file updates in single operation
- Access to bash, web search, and other tools

**Configuration:**
- Uses `CLAUDE.md` files for project-specific instructions
- Defines wiki schema, conventions, and workflows
- Stores memory in `.claude/` directory
- **[[concepts/agent-skills]]** stored in `.claude/skills/` directory
- Can run skills and automation loops
- Supports "bypass permissions" or "Yolo mode" for autonomous operation

**Obsidian Integration** (via [[concepts/obsidian-cli]]):
- Calls CLI commands through obsidian-cli Skill
- Extremely token-efficient (~100 tokens vs 500,000+ for file scanning)
- Preserves graph integrity (auto-updates wikilinks)
- Can trigger Obsidian operations from agent workflows

**Integration features:**
- Git integration for version control
- Loop functionality for scheduled automation
- Skill system for reusable workflows
- Compatible with Obsidian vault structures

## Common Strategies

**LLM Wiki Implementation:**

1. **Setup**: Create vault with wizard (raw/, wiki/, outputs/ structure)
2. **Ingest**: `second brain ingest` command reads raw/ files
3. **Query**: Ask questions against wiki, get cited answers
4. **Lint**: `second brain lint` reviews wiki health
5. **Loop**: Automate ingestion on schedule (e.g., every few hours)

**AutoResearch Implementation** ([[concepts/auto-research]]):
- Operates in bypass/Yolo mode for autonomous experimentation
- Runs [[concepts/experiment-loop]] continuously
- Modifies designated files based on [[concepts/three-file-architecture]]
- Commits successful experiments, resets failures
- Can run 100+ experiments overnight without human intervention
- Used in tutorial demonstrations for website optimization and code improvement

**Skill-based workflow:**
- Setup wizard for new vaults
- Ingest skill processes sources
- Query skill searches and synthesizes
- Lint skill health checks
- Built using Vercel's framework for compatibility
- Official Skills by [[entities/steph-ango]]: obsidian-cli, obsidian-bases, obsidian-markdown, defuddle

**Skills 2.0** (via [[entities/skill-creator]]):
- Meta-skill that creates other skills with automated testing
- Fully automated skill generation (~10 minutes for complex skills)
- Built-in [[concepts/skill-testing]] and iterative improvement
- Managed via `manage plugins` command
- Can install per-project or globally ("for you")
- Demonstrates [[concepts/meta-skills]] approach to skill development

**Agent agnostic design:**
- Skills work across Claude Code, Codex, Gemini CLI, Open Code, Pi
- Both CLAUDE.md and AGENTS.md files for cross-compatibility
- Can be customized to individual needs
- Directory structure: `.claude/skills/<skill-name>/SKILL.md`

**Human-AI collaboration:**
- LLM agent on one side of screen
- Obsidian on other side
- LLM makes edits, human browses results in real-time
- Transparent citation to wiki pages

## Related Entities

- [[entities/obsidian]] — Frontend IDE that Claude Code edits
- [[entities/andrej-karpathy]] — Originated pattern Claude Code implements
- [[entities/skill-creator]] — Meta-skill for Skills 2.0 methodology
- [[entities/nick-babich]] — Created Skills 2.0 tutorials
- [[entities/nick-b-zark]] — Built second brain skill for Claude Code
- [[entities/vercel]] — Framework used for skill development

## Related Concepts

- [[concepts/llm-knowledge-base]] — Primary use case for wiki maintenance
- [[concepts/claude-skills]] — Skill system and structure
- [[concepts/meta-skills]] — Skills that create other skills
- [[concepts/skill-testing]] — Automated skill evaluation
- [[concepts/auto-research]] — Used as autonomous optimization agent
- [[concepts/autonomous-agents]] — Operates autonomously in bypass mode
- [[concepts/experiment-loop]] — Executes optimization loops

## Sources

- [[summaries/claude-karpathy-second-brain-video]] — Claude Code demonstration and setup
- [[summaries/llm-wiki]] — Agent harness role in LLM wiki pattern
- [[summaries/autoresearch-tutorial]] — Claude Code in AutoResearch workflows
- [[summaries/obsidian-cli-core-principles]] — Integration architecture
- [[summaries/obsidian-essential-skills]] — Skills ecosystem
- [[summaries/claude-skills-2-skill-creator]] — Skills 2.0 methodology and Skill Creator
