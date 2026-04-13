---
title: "Claude Skills"
type: concept
tags: [claude-code, foundational, automation, instructions, workflow]
created: 2026-04-13
updated: 2026-04-13
sources: ["raw/claude-skills-2-how-to-use-skill-creator.md"]
confidence: high
---

# Claude Skills

## Definition

Claude skills are markdown-based instruction files that teach Claude Code how to complete specific tasks in a repeatable way. They are essentially structured prompts packaged as reusable workflows.

## How It Works

### File Structure

A Claude skill is a markdown file with two essential parts:

1. **Front matter** (between `---` markers):
   - Metadata about the skill
   - Trigger conditions (when to use the skill)
   - Installation scope
   - Tags and categorization

2. **Markdown content**:
   - Step-by-step workflow
   - Actions Claude should perform
   - Context and examples
   - Expected outputs

### Invocation

Skills can be triggered:
- By command: `/skill-name` in the prompt
- By context: When Claude detects relevant trigger conditions
- Manually: User explicitly asks to use a specific skill

### Storage and Management

- Stored in `.claude/skills/` directory
- Can be installed per-project or globally
- Managed via `manage plugins` command
- Listed with `show skills` command

## Key Parameters

- **Scope**: Per-project vs global ("for you")
- **Complexity**: Simple single-step vs complex multi-stage workflows
- **Trigger conditions**: Explicit invocation vs automatic detection
- **Quality**: Manual creation vs [[entities/skill-creator]] automated generation

## When To Use

- **Repetitive tasks**: Actions you perform frequently with similar steps
- **Complex workflows**: Multi-step processes that need to be repeatable
- **Consistent quality**: Tasks where you want standardized output
- **Team collaboration**: Sharing best practices and workflows with others
- **Domain expertise**: Packaging specialized knowledge for reuse

## Skills 2.0

The community term for the improved skill creation process using [[entities/skill-creator]]:

**Traditional approach** (Skills 1.0):
- Manual markdown file creation
- Trial and error refinement
- No systematic testing

**Skills 2.0 approach**:
- Automated generation via [[entities/skill-creator]]
- Built-in testing and evaluation
- Iterative improvement based on test results
- Significantly higher quality output

## Risks & Pitfalls

- **Over-specification**: Too rigid skills that don't adapt to context variations
- **Under-specification**: Vague instructions that produce inconsistent results
- **Scope creep**: Skills that try to do too much, better split into multiple skills
- **Staleness**: Skills that reference outdated tools or APIs
- **Poor triggers**: Skills that activate when not needed or fail to activate when needed

## Related Concepts

- [[concepts/meta-skills]] — Skills that operate on other skills
- [[concepts/skill-testing]] — Evaluation and improvement methodology
- [[concepts/automation-workflows]] — Broader automation context
- [[concepts/agent-skills]] — Related skill concept in AI agents
- [[entities/skill-creator]] — Tool for creating Skills 2.0
- [[entities/claude-code]] — Platform that executes skills

## Sources

- [[summaries/claude-skills-2-skill-creator]] — Comprehensive tutorial on Skills 2.0
- [[summaries/obsidian-essential-skills]] — Catalog of essential skills
