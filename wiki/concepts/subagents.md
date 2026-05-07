---
title: "Subagents"
type: concept
tags: [claude-code, agents, context-isolation, workflow, foundational]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Using CLAUDE.MD files Customizing Claude Code for your codebase.md"]
confidence: high
---

## Definition

Subagents in Claude Code are isolated Claude instances spawned for distinct phases of work, maintaining their own context separate from the main conversation. This prevents information from earlier tasks from interfering with fresh analysis and enables parallel work on independent problems.

## How It Works

### Context Isolation
1. **Fresh context**: Subagent starts with empty conversation history
2. **Shared configuration**: Inherits CLAUDE.md and project settings
3. **Independent analysis**: Previous debugging details don't color new security review
4. **Result synthesis**: Subagent's conclusions return to main conversation

### Invocation Pattern
User explicitly requests subagent:
```
Tell Claude to use a sub-agent to perform a security review of that code
```

Claude spawns isolated instance, passes relevant context, receives results.

### Context Window Benefits
- Long debugging session doesn't pollute security audit context
- Implementation details don't interfere with performance analysis
- Multiple subagents can work in parallel on independent queries
- Main context window preserved for primary workflow

## Key Parameters

### When To Use Subagents
- **Phase transitions**: Implementation → security review → performance audit
- **Parallel analysis**: Multiple independent questions about same code
- **Fresh perspective**: Need unbiased review of previous work
- **Context overflow**: Main conversation too long, need clean slate
- **Specialized tasks**: Domain-specific analysis requiring focused context

### Subagent Types
Available in Claude Code:
- **general-purpose**: Default subagent for unspecialized work
- **Explore**: Fast codebase exploration and search
- **Plan**: Software architecture and implementation planning
- **Custom agents**: Project-specific subagent types

### Context Sharing
- **Input**: Explicit context passed when spawning
- **Output**: Subagent's findings return to main conversation
- **CLAUDE.md**: Shared with all subagents
- **History**: Not shared - each subagent starts fresh

## When To Use

Use subagents when:
- Switching between distinct phases (implement → review → optimize)
- Need unbiased analysis of code you just wrote
- Main conversation too long and cluttered
- Multiple independent queries could run in parallel
- Task requires specialized agent type (Explore, Plan)

Don't use subagents for:
- Continuation of current task
- When context from main conversation is essential
- Simple questions that don't justify overhead
- Tasks requiring iterative back-and-forth

## Risks & Pitfalls

### Common Issues
1. **Context loss**: Important details from main conversation don't transfer
2. **Redundant work**: Subagent re-analyzes things main conversation already covered
3. **Overhead**: Spawning subagent takes time vs continuing main conversation
4. **Fragmentation**: Too many subagents make it hard to track overall progress
5. **Over-isolation**: Sometimes previous context is actually valuable

### Best Practices
- **Explicit context transfer**: Tell Claude what information subagent needs
- **Clear task boundaries**: Use for distinct phases, not minor subtasks
- **Result integration**: Have main agent synthesize subagent findings
- **Judicious use**: Don't spawn subagent for every subtask

### Comparison to /clear
- **Subagent**: Returns results to main conversation, parallel-capable
- **/clear**: Destroys main context, starts over completely
- **Use subagent**: When you want fresh analysis but need to preserve main workflow
- **Use /clear**: When entire conversation is no longer relevant

## Related Concepts

- [[concepts/context-window-management]] - Why context isolation matters
- [[concepts/context-engineering]] - Principles for managing context effectively
- [[concepts/claude-md-configuration]] - Shared configuration across agents
- [[concepts/specialized-agents]] - Purpose-built agent types (Explore, Plan)
- [[concepts/parallel-processing]] - Using multiple subagents concurrently

## Sources

- "Using CLAUDE.MD files: Customizing Claude Code for your codebase" (Anthropic blog, 2001-11-25)
