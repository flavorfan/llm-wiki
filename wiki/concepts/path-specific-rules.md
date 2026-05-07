---
title: "Path-Specific Rules"
type: concept
tags: [claude-code, automation, configuration, context-engineering, advanced]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md", "raw/Hooks reference.md"]
confidence: high
---

## Definition

Path-specific rules are conditional instructions stored in `.claude/rules/` that Claude Code automatically loads only when working on files matching specified patterns. This enables context-aware instruction loading without bloating the base CLAUDE.md file.

## How It Works

### File Structure
1. Create `.claude/rules/` directory in your project
2. Add markdown files with path patterns in frontmatter:
```markdown
---
paths: ["**/*.spec.ts", "**/*.test.ts"]
---
# Testing Guidelines
Use jest for unit tests...
```

3. Claude Code monitors file operations and loads matching rules automatically

### Loading Behavior
- **Lazy loading**: Rules load only when Claude accesses a file matching the path pattern
- **Pattern syntax**: Supports glob patterns (`**/*.ts`, `src/**/*.{tsx,jsx}`)
- **Multiple patterns**: Single file can specify multiple path patterns
- **Scope isolation**: Rules apply only while working in matching paths

### Integration with Hooks
Path-specific rules complement [[concepts/hooks]] by providing instructions where hooks provide automation. A rule file for tests might say "use jest", while a hook actually runs jest after test file changes.

## Key Parameters

### Path Patterns
- **Glob syntax**: Standard glob patterns with `*`, `**`, `?`, and `{a,b}` expansions
- **File extensions**: `*.spec.ts` for TypeScript tests, `*.py` for Python files
- **Directory scope**: `src/api/**/*.ts` for API-specific rules
- **Multiple patterns**: `["**/*.test.js", "**/*.spec.js"]` for alternative naming conventions

### Rule Content
Appropriate for path-specific rules:
- Testing frameworks and conventions for test files
- Database query patterns for model files
- Security requirements for authentication code
- API conventions for route handlers
- Build requirements for configuration files

Not appropriate (belongs in main CLAUDE.md):
- Project-wide conventions
- Commands that apply everywhere
- Critical safety rules

### File Organization
```
.claude/
  rules/
    testing.md          # paths: ["**/*.test.ts"]
    api-conventions.md  # paths: ["src/api/**/*.ts"]
    security.md         # paths: ["**/auth/**/*"]
```

## When To Use

Use path-specific rules when:
- Different parts of codebase have different conventions
- Testing, API, or security guidelines apply to specific directories
- Your CLAUDE.md exceeds 200-300 lines
- Instructions are only relevant when working on certain file types
- Monorepo has multiple sub-projects with different standards

Don't use for:
- Rules needed in majority of files
- Project-wide conventions
- Information referenced across many contexts

## Risks & Pitfalls

### Common Issues
1. **Pattern mismatch**: Rule doesn't load because path pattern is too narrow
2. **Over-specific patterns**: Pattern is so specific it rarely matches
3. **Forgotten rules**: Team forgets rules exist in `.claude/rules/` directory
4. **Maintenance burden**: Many small rule files are harder to maintain than one CLAUDE.md
5. **Load timing**: Rules load after file access, might miss initial context
6. **Pattern conflicts**: Multiple rules match same file with conflicting instructions

### Design Principles
- **Prefer fewer, broader rules** over many narrow ones
- **Test patterns** with glob matching tools before committing
- **Document structure** in main CLAUDE.md so team knows rules exist
- **Consolidate similar rules** rather than creating many small files
- **Use descriptive names** that indicate when the rule applies

## Related Concepts

- [[concepts/progressive-disclosure]] - Broader technique for conditional context loading
- [[concepts/claude-md-configuration]] - Base configuration file
- [[concepts/hooks]] - Event-driven automation that complements rules
- [[concepts/context-window-management]] - Why conditional loading matters
- [[concepts/instruction-following-limits]] - LLM capacity constraints that motivate path-specific rules

## Sources

- "Stop Writing Bad CLAUDE.md Files" (camelCase video, 2026-02-04)
- "Hooks reference" (Claude Code documentation, accessed 2026-05-03)
