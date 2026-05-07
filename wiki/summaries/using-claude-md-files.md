---
title: "Using CLAUDE.MD files: Customizing Claude Code for your codebase"
type: summary
tags: [claude-code, official-documentation, best-practices, configuration, workflows]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Using CLAUDE.MD files Customizing Claude Code for your codebase.md"]
confidence: high
---

## Key Points

- **Purpose**: CLAUDE.md gives Claude persistent context about project structure, coding standards, and workflows without repeating yourself
- **Getting started with /init**: Automated analysis generates starter configuration by examining package files, documentation, and code structure
- **File locations**: Repository root (shared with team), parent directories (monorepos), home folder (universal), `.local.md` (gitignored personal settings)
- **Give Claude a map**: Include project summary and high-level directory structure tree for orientation
- **Connect to tools**: Document custom utilities, MCP servers, and tool usage patterns. Claude functions as MCP client and inherits complete environment
- **Define workflows**: Establish standard processes (explore-plan-code-commit, TDD) with four questions before changes: investigation needed? plan required? missing info? how to test?
- **Keep context fresh**: Use `/clear` between distinct tasks to reset context window while preserving CLAUDE.md
- **Use subagents for distinct phases**: Isolated context prevents debugging details from interfering with security review, implementation from affecting analysis
- **Create custom commands**: Store repeated prompts as markdown files in `.claude/commands/` directory, support arguments via `$ARGUMENTS` or `$1`, `$2`
- **Start simple, expand deliberately**: Don't create comprehensive CLAUDE.md upfront. Add based on actual friction points, keep concise
- **Security**: Never include API keys, credentials, database connection strings, or vulnerability details. CLAUDE.md becomes part of system prompt

## Relevant Concepts

- [[concepts/claude-md-configuration]] - Core configuration concept
- [[concepts/progressive-disclosure]] - Reference separate files instead of embedding
- [[concepts/context-window-management]] - Why `/clear` matters
- [[concepts/claude-skills]] - Custom slash commands
- [[concepts/mcp-servers]] - Model Context Protocol integration
- [[concepts/subagents]] - Isolated context for different work phases
- [[concepts/context-engineering]] - Principles for effective AI context

## Source Metadata

- **Type**: Official blog article
- **Publisher**: Anthropic (Claude.com)
- **Published**: 2001-11-25 (likely date error, actual 2025+)
- **URL**: https://claude.com/blog/using-claude-md-files
- **Target audience**: Claude Code users, development teams
- **Tone**: Educational, practical implementation guide
