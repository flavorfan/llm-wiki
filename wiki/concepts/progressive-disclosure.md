---
title: "Progressive Disclosure"
type: concept
tags: [context-engineering, claude-code, best-practices, token-optimization, foundational]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md", "raw/Writing a good CLAUDE.md"]
confidence: high
---

## Definition

Progressive disclosure is a context engineering technique where detailed information is stored in separate files and loaded only when relevant, rather than placing everything in CLAUDE.md. This keeps the base context small while making specialized knowledge available on demand.

## How It Works

### Reference-Based Approach
Instead of embedding full instructions in CLAUDE.md, store them in descriptively-named files and provide pointers:

```markdown
## Further Documentation
- Database: read docs/schema.md when modifying models
- Testing: read docs/testing-guide.md for test conventions  
- Security: read docs/security-requirements.md before auth changes
```

Claude decides whether to read these files based on the current task. The matcher can be explicit instructions or self-descriptive file names.

### Path-Specific Rules
A more advanced form uses `.claude/rules/` folder with path specifications in file frontmatter:

```markdown
---
paths: ["**/*.spec.ts"]
---
Testing conventions for TypeScript spec files...
```

Claude Code automatically loads this file only when working on `.spec.ts` files, keeping it out of context otherwise.

### Skill-Based Loading
[[concepts/claude-skills]] can encapsulate domain-specific instructions and load conditionally based on task requirements.

## Key Parameters

### File Organization
- **Location**: `docs/`, `.claude/rules/`, or project-specific directories
- **Naming**: Use descriptive names that indicate when to load (e.g., `database-schema.md`, `testing-guide.md`)
- **Size**: Keep individual files focused; split large documents into modules

### Loading Triggers
- **Manual reference**: "Read X when doing Y" in CLAUDE.md
- **Path patterns**: Automatic loading based on file path matches
- **Skill invocation**: Load via slash commands or automatic skill triggers
- **MCP tools**: Custom tools that fetch context from external sources

### Content Types
Suitable for progressive disclosure:
- Database schemas and ER diagrams
- API specifications and endpoint documentation
- Test frameworks and conventions
- Security requirements and compliance rules
- Domain-specific business logic
- Tool-specific configuration details

Not suitable (keep in CLAUDE.md):
- Project one-liner and essential context
- Most frequently used commands
- Universal caveats and warnings

## When To Use

Use progressive disclosure when:
- Your CLAUDE.md exceeds 300 lines
- Different parts of the codebase need different context
- Detailed specifications would overwhelm the main config
- Information applies only to specific file types or directories
- Team members work in specialized domains
- You want to preserve context budget for actual work

Don't use progressive disclosure for:
- Instructions needed in >80% of conversations
- The three essentials (project description, key commands, caveats)
- Critical safety requirements that always apply

## Risks & Pitfalls

### Failure Modes
1. **Over-fragmentation**: Too many small files creates cognitive overhead finding the right document
2. **Unclear triggers**: Vague file names or instructions make it hard for Claude to know when to load
3. **Circular references**: File A references B which references C, loading everything anyway
4. **Stale pointers**: Referenced files are moved/renamed but CLAUDE.md isn't updated
5. **Anticipatory loading**: Claude reads files "just in case" rather than when actually needed

### Trade-offs
- **Precision vs Coverage**: Narrow path patterns may miss relevant cases; broad patterns load too often
- **Automation vs Control**: Automatic path-based loading is convenient but less predictable than explicit references
- **Duplication vs DRY**: Sometimes duplicating critical info in CLAUDE.md is better than relying on references

## Related Concepts

- [[concepts/claude-md-configuration]] - The base configuration file
- [[concepts/path-specific-rules]] - Automatic loading based on file paths
- [[concepts/context-window-management]] - Managing token budget
- [[concepts/token-optimization]] - Efficient use of context window
- [[concepts/claude-skills]] - Reusable capabilities with embedded context
- [[concepts/instruction-following-limits]] - Why minimizing loaded instructions matters

## Sources

- "Stop Writing Bad CLAUDE.md Files" (camelCase video, 2026-02-04)
- "Writing a good CLAUDE.md" (HumanLayer blog, 2025-11-25)
