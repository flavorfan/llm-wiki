---
title: "Stop Writing Bad CLAUDE.md Files"
type: summary
tags: [claude-code, best-practices, prompt-engineering, configuration, documentation]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md"]
confidence: high
---

## Key Points

- **Size is critical**: Claude MD should be as short as possible, ideally under 300 lines. LLMs can follow ~150-200 instructions with reasonable consistency; Claude Code's system prompt already contains ~50 instructions
- **Avoid /init command**: Auto-generated CLAUDE.md files tend to be verbose, vague, and contain unnecessary instructions that negatively impact every prompt
- **Don't specify code style**: Use linters and formatters instead of wasting instructions on formatting rules. Claude naturally derives style from existing code
- **Start with three essentials**: (1) One-liner describing the project, (2) Key commands (test, build, lint), (3) Project-specific caveats and warnings
- **Progressive disclosure**: Store detailed instructions in separate docs/ files and reference them in CLAUDE.md so Claude reads them only when needed
- **Path-specific rules**: Use `.claude/rules/` folder with path specifications to load instructions only when working on matching files
- **Instructions at edges matter more**: LLMs prioritize instructions at the beginning (Claude MD start) and end (recent user messages). Middle instructions get neglected
- **Emphasize important items**: Use capitalized "IMPORTANT" or "YOU MUST" with exclamation marks to increase likelihood of compliance
- **Keep it updated**: Claude MD should be a living document. Use GitHub integration to tag Claude in PRs for automatic updates
- **Multiple location options**: Project root, parent directories (for monorepos), `.local.md` for personal settings, home directory for global preferences
- **Hooks for automation**: Use post-tool-use hooks for formatting/linting instead of instructions

## Relevant Concepts

- [[concepts/claude-md-configuration]] - Core configuration file for Claude Code
- [[concepts/progressive-disclosure]] - Technique for selectively loading context
- [[concepts/path-specific-rules]] - Conditional instruction loading based on file paths
- [[concepts/instruction-following-limits]] - LLM capacity constraints (150-200 instructions)
- [[concepts/hooks]] - Automation workflow events
- [[concepts/context-window-management]] - Managing LLM context effectively
- [[concepts/code-style-automation]] - Using deterministic tools for formatting

## Source Metadata

- **Type**: Video transcript
- **Author**: camelCase (YouTube channel)
- **Published**: 2026-02-04
- **URL**: https://www.youtube.com/watch?v=lJNjDoJi6hQ
- **Sponsor**: G2I (hiring platform)
- **Target audience**: Claude Code users, applicable to Cursor, Codex, and other AI coding tools
