---
title: "Agentic Loops"
type: concept
tags: [agents, workflow, autonomous-agents, multi-step-reasoning, design-patterns, well-established]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Agentic loops are multi-step workflows where separate prompts handle discrete responsibilities that feed into each other iteratively. Rather than asking a single large prompt to do everything, the system breaks complex tasks into smaller prompts that run sequentially, each focused on one job: generate → evaluate → refine.

## How It Works

**Three-Stage Example** (employee scheduling):

```
┌─────────────────────────────────────────┐
│ GENERATOR: Create initial schedule      │
│ Input: Employee availability, rules     │
│ Output: First-draft schedule (JSON)     │
└────────────────┬────────────────────────┘
                 │
                 ↓
┌─────────────────────────────────────────┐
│ EVALUATOR: Check for violations         │
│ Input: Schedule, rules, constraints     │
│ Output: List of violations w/ evidence  │
└────────────────┬────────────────────────┘
                 │
                 ↓
┌─────────────────────────────────────────┐
│ FIXER: Repair specific violations       │
│ Input: Schedule, violation report       │
│ Output: Corrected schedule              │
└────────────────┬────────────────────────┘
                 │
                 ↓ (if violations found, loop back to EVALUATOR)
            ✓ Valid / Done
```

**Key Design Principle**: Each prompt is simpler and more focused than trying to solve everything in one massive prompt.

## How It Works

**Advantages over monolithic prompts**:
- **Easier debugging** — Isolate which stage is failing
- **Better token efficiency** — Each stage does focused work; doesn't repeat context across all reasoning
- **Lower latency** — Can optimize each stage independently instead of one slow multi-task prompt
- **Runtime flexibility** — Add soft constraints (e.g., "Harry prefers not to work with Sally") without changing underlying Python/system logic
- **Composability** — Stages can be mixed/matched for different scenarios

**Cost-Latency Trade-offs**:
- **Option A** — Single [[concepts/adaptive-thinking]] enabled prompt: High accuracy, but 3x tokens, 3x latency
- **Option B** — Agentic loop with smaller model: Slightly lower accuracy, but better tokens/latency ratio
- **Option C** — Monolithic optimized prompt: May hit token limits or fail on edge cases

In the playbook example, the agentic loop **outperformed** both alternatives in tokens and latency while maintaining accuracy.

## Key Parameters

- **Number of stages** — Usually 3-5 (generator, evaluator, fixer, validator)
- **Feedback mechanism** — How does each stage know what to improve on?
- **Termination criteria** — When does the loop stop (all constraints met, max iterations, etc.)?
- **State passing** — What context carries forward between stages?
- **Error handling** — What if a stage fails or enters infinite loop?

## When To Use

- **Complex multi-constraint problems** — Scheduling, planning, multi-step workflows
- **When output quality matters more than latency** — Content generation, code review, compliance checking
- **Iterative refinement needed** — Tasks where first attempt often has issues to fix
- **Token budget concerns** — Agentic approach often cheaper than one large prompt
- **Soft constraints** — Runtime rules that shouldn't be baked into system logic

## Risks & Pitfalls

- **Infinite loops** — Evaluator/fixer can cycle indefinitely if constraints are contradictory or impossible
  - Fix: Set max iteration limit, monitor for non-progress
  
- **Lost context** — Each stage sees only what previous stage output; might miss important context
  - Fix: Pass full problem context, not just diffs
  
- **Compounding errors** — Mistakes in early stage propagate and are hard to fix downstream
  - Fix: Heavy validation in evaluator stage, fail fast
  
- **Overhead** — Extra LLM calls add latency if not structured carefully
  - Fix: Batch operations, use cheaper models for filtering stages
  
- **Prompt brittleness** — Each stage's instructions must be crystal clear or failures cascade
  - Fix: Heavy use of examples, clear input/output contracts for each stage

## Architecture Patterns

### Linear Pipeline
Generator → Evaluator → Fixer → Return to user

### Feedback Loop
Generator → Evaluator → (loop if violations) → Fixer → Done

### Tree Search
Generator (multiple branches) → Evaluator ranks → Keep best

### Hierarchical
High-level planner → Delegate to specialists → Aggregate results

## Related Concepts

- [[concepts/prompt-engineering]] — Each stage is a carefully tuned prompt
- [[concepts/evaluation-frameworks]] — Evaluator stage is core to loop
- [[concepts/tool-use-patterns]] — Stages often call tools to check constraints
- [[concepts/autonomous-agents]] — Loops enable agent autonomy
- [[concepts/langraph]] — LangGraph implements agentic loops as state machines
- [[concepts/experiment-loop]] — Similar iteration pattern for research/optimization
- [[concepts/agent-skills]] — Each stage could be a separate [[concepts/agent-skills]]

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Employee scheduling example showing agentic loop outperforming monolithic approaches
