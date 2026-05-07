---
title: "Code Style Automation"
type: concept
tags: [best-practices, tools, automation, linting, formatting, deterministic]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md", "raw/Writing a good CLAUDE.md"]
confidence: high
---

## Definition

Code style automation refers to using deterministic tools (linters, formatters) to enforce code style and formatting rules instead of relying on LLM instructions. This principle recognizes that LLMs are comparatively expensive, slow, and non-deterministic for tasks that traditional tools handle perfectly.

## How It Works

### Deterministic Tools
- **Linters**: ESLint, Pylint, Rubocop - identify style violations
- **Formatters**: Prettier, Black, Biome - automatically fix formatting
- **Pre-commit hooks**: Run checks before code is committed
- **CI/CD integration**: Enforce on pull requests
- **IDE integration**: Real-time feedback while editing

### Integration with Claude Code
Instead of CLAUDE.md instructions like:
```markdown
- Use 2 spaces for indentation
- Single quotes for strings
- Trailing commas in objects
```

Use [[concepts/hooks]] to run formatters:
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Edit|Write",
      "hooks": [{
        "type": "command",
        "command": "biome format --write $FILE"
      }]
    }]
  }
}
```

Or create slash command for manual formatting:
```markdown
# .claude/commands/format.md
Run biome format on all changed files
```

## Key Parameters

### Tool Selection
- **Biome**: Fast, opinionated formatter with auto-fix capabilities
- **Prettier**: Popular JavaScript/TypeScript formatter
- **Black**: Python's opinionated formatter
- **ClangFormat**: C/C++ formatting
- **RustFmt**: Rust formatting

### Execution Points
- **Post-tool-use hooks**: Automatic formatting after Edit/Write
- **Stop hooks**: Format before Claude finishes response
- **Pre-commit**: Git hooks prevent unformatted commits
- **CI/CD**: Block PRs with style violations
- **Manual commands**: Slash command when needed

### Auto-fix Strategy
- **Safe auto-fixes**: Whitespace, quotes, trailing commas
- **Manual review**: Structural changes, potential logic changes
- **Maximize coverage**: Tune rules for maximum safe auto-fix
- **Fast feedback**: IDE integration for immediate correction

## When To Use

Always prefer automated tools over LLM instructions for:
- Code formatting and indentation
- Import organization and sorting
- Trailing commas and semicolons
- Quote style (single vs double)
- Line length and wrapping
- Naming convention enforcement (when checkable)
- Comment formatting

Use LLM instructions for:
- Architectural patterns (not mechanically checkable)
- Domain-specific conventions
- Business logic patterns
- API design preferences

## Risks & Pitfalls

### Why LLMs Are Poor Linters
1. **Expensive**: API costs for formatting checks
2. **Slow**: Seconds vs milliseconds for traditional tools
3. **Non-deterministic**: Same code may format differently each time
4. **Context waste**: Formatting rules consume [[concepts/instruction-following-limits]]
5. **CI failure**: Pipeline may still fail after Claude "fixes" style
6. **Token inefficiency**: Style guidelines bloat CLAUDE.md

### Common Mistakes
- **Duplicated effort**: Having both linter rules AND CLAUDE.md instructions
- **Fighting tools**: LLM formats one way, pre-commit hook reformats differently
- **Over-specification**: Detailed style guide in CLAUDE.md that tool already enforces
- **Manual formatting**: Having Claude fix style issues that tool catches
- **Ignoring tools**: Team has linter configured but Claude doesn't know to run it

### Integration Challenges
- **Tool configuration**: Must be committed to repo
- **Team alignment**: Everyone must use same tools/versions
- **CI/CD setup**: Automated checks need infrastructure
- **Hook complexity**: May need scripting for file-type routing

## Related Concepts

- [[concepts/hooks]] - Automation mechanism for running formatters
- [[concepts/claude-md-configuration]] - What not to put in CLAUDE.md
- [[concepts/instruction-following-limits]] - Why style rules are costly
- [[concepts/deterministic-tools]] - Broader category of tool-based automation
- [[concepts/progressive-disclosure]] - Where to document formatting tool usage

## Sources

- "Stop Writing Bad CLAUDE.md Files" (camelCase video, 2026-02-04): "Don't give your AI code style instructions. That's stupid."
- "Writing a good CLAUDE.md" (HumanLayer blog, 2025-11-25): "Never send an LLM to do a linter's job"
