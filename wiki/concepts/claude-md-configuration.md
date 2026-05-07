---
title: "CLAUDE.md Configuration"
type: concept
tags: [claude-code, configuration, best-practices, foundational, llm-agents]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md", "raw/Using CLAUDE.MD files Customizing Claude Code for your codebase.md", "raw/Writing a good CLAUDE.md"]
confidence: high
---

## Definition

CLAUDE.md is a special markdown configuration file that provides Claude Code with persistent project-specific context. It is automatically read at the start of every session and becomes part of Claude's system prompt, eliminating the need to repeatedly explain project structure, coding standards, and workflows.

## How It Works

CLAUDE.md files work through a hierarchical discovery system:

1. **Automatic loading**: Claude searches for CLAUDE.md in the current directory, parent directories (for monorepos), and user home directory
2. **Context injection**: File contents are added to Claude's system prompt at session start
3. **Scoped variants**: Use `.claude/settings.local.json` for personal overrides or home directory for global settings
4. **Stateless nature**: Since LLMs don't learn between sessions, CLAUDE.md provides the only persistent context that carries across conversations

The file uses standard markdown format with no required structure, though best practices suggest specific sections.

## Key Parameters

### Size Constraints
- **Target length**: Under 300 lines, shorter is better
- **Instruction limit**: LLMs follow ~150-200 instructions reliably; Claude Code system prompt uses ~50
- **Quality degradation**: More instructions = uniformly worse instruction-following across all instructions
- **Token efficiency**: Every line uses context window space in every conversation

### Essential Components
1. **Project one-liner**: Framework, purpose, and type (e.g., "FastAPI REST API for user authentication")
2. **Key commands**: Most important bash commands (test, build, lint, deploy)
3. **Project caveats**: Non-obvious warnings and constraints that prevent errors

### Optional Sections
- Architecture overview and directory structure
- Testing requirements and standards
- Common workflows (feature development, PR process)
- Tool configurations and custom utilities
- Domain-specific patterns

## When To Use

Use CLAUDE.md when you need to:
- Onboard Claude to a new codebase quickly
- Share project conventions across team members
- Eliminate repetitive context explanations
- Provide environment-specific configuration
- Document architectural decisions that aren't obvious from code

Start with basics and expand based on actual friction points. Don't write comprehensive documentation upfront.

## Risks & Pitfalls

### Anti-Patterns
1. **Auto-generation with /init**: Creates verbose, generic content that bloats context
2. **Code style instructions**: Use linters/formatters instead; Claude derives style from existing code
3. **Exhaustive documentation**: Including every possible command or edge case degrades performance
4. **Theoretical guidelines**: Adding instructions for hypothetical scenarios rather than actual problems
5. **Stale information**: Forgetting to update as codebase evolves

### Technical Limitations
- **Selective attention**: Claude Code adds system reminder that CLAUDE.md "may or may not be relevant," causing Claude to ignore irrelevant content
- **Positional bias**: Instructions at file start (high priority) and end of conversation (recency) matter most; middle content gets neglected
- **No learning**: Changes to CLAUDE.md only apply to new sessions; doesn't affect current conversation
- **Instruction interference**: Bad instructions affect every subsequent prompt and action

## Related Concepts

- [[concepts/progressive-disclosure]] - Technique for conditional context loading
- [[concepts/path-specific-rules]] - Load instructions only for matching file paths
- [[concepts/hooks]] - Automate workflows without instructions
- [[concepts/instruction-following-limits]] - LLM capacity constraints
- [[concepts/context-window-management]] - Managing token budget
- [[concepts/claude-skills]] - Reusable capabilities beyond static configuration

## Sources

- "Stop Writing Bad CLAUDE.md Files" (camelCase video, 2026-02-04)
- "Using CLAUDE.MD files: Customizing Claude Code for your codebase" (Anthropic blog, 2001-11-25)
- "Writing a good CLAUDE.md" (HumanLayer blog, 2025-11-25)
