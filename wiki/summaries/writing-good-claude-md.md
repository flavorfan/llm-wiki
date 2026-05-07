---
title: "Writing a good CLAUDE.md"
type: summary
tags: [claude-code, best-practices, context-engineering, agents-md, 12-factor-agents]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Writing a good CLAUDE.md"]
confidence: high
---

## Key Points

- **LLMs are stateless**: Weights frozen at inference time, don't learn over time. CLAUDE.md is the only file that goes into every single conversation
- **Onboard Claude to your codebase**: Cover WHAT (tech stack, structure), WHY (project purpose, function), HOW (commands, workflows, verification)
- **Claude often ignores CLAUDE.md**: Harness injects system reminder "this context may or may not be relevant to your tasks" - Claude ignores content it deems irrelevant
- **Less instructions is more**: Frontier thinking LLMs follow ~150-200 instructions. As count increases, instruction-following degrades uniformly across all instructions, not selectively
- **Claude Code uses ~50 instructions** already in system prompt - nearly 1/3 of capacity before user writes anything
- **Model-specific decay patterns**: Smaller models exhibit exponential decay in instruction-following, frontier thinking models show linear decay
- **CLAUDE.md should be universally applicable**: File goes into every session, so contents must be relevant across all tasks. HumanLayer's root CLAUDE.md is under 60 lines
- **Progressive Disclosure**: Keep task-specific instructions in separate files with self-descriptive names. List them in CLAUDE.md for Claude to read when needed
- **Prefer pointers to copies**: Don't include code snippets (go stale quickly). Use `file:line` references instead
- **Claude is not an expensive linter**: Never use LLM for code style. LLMs are slow and non-deterministic. Use actual linters/formatters
- **Don't auto-generate CLAUDE.md**: It's the highest leverage point of harness - affects every artifact. Carefully craft every line
- **Use hooks and slash commands**: Separate formatting enforcement (hooks) from implementation (instructions) for better results on both

## Relevant Concepts

- [[concepts/claude-md-configuration]] - Core configuration file
- [[concepts/instruction-following-limits]] - Research on ~150-200 instruction capacity
- [[concepts/progressive-disclosure]] - Technique for conditional context loading
- [[concepts/stateless-llms]] - Why persistent configuration is necessary
- [[concepts/hooks]] - Event-driven automation instead of instructions
- [[concepts/code-style-automation]] - Using linters over LLM instructions
- [[concepts/context-engineering]] - 12-factor-agents best practices
- [[concepts/leverage-points]] - Why CLAUDE.md is highest-leverage harness config

## Source Metadata

- **Type**: Blog article / best practices guide
- **Author**: Kyle (HumanLayer)
- **Publisher**: HumanLayer.dev
- **Published**: 2025-11-25
- **URL**: https://www.humanlayer.dev/blog/writing-a-good-claude-md
- **Also applicable to**: AGENTS.md (OpenCode, Zed, Cursor, Codex)
- **Framework**: 12-factor-agents context engineering principles
- **Target audience**: Agent-enabled software engineering practitioners
