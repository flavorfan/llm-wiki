---
title: "Model Selection"
type: concept
tags: [model-capabilities, inference, performance, cost-optimization, trade-offs, foundational]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Model selection is the architectural decision of which language model to use for a task, considering trade-offs between accuracy, latency, token cost, and capabilities. The choice depends on whether the bottleneck is capability (model can't do the task) vs. behavior (model can but needs different prompting).

## How It Works

**Capability vs. Behavior**:

When a model produces poor output, diagnoses the root cause:

1. **Capability issue** — Model lacks the ability entirely
   - Example: Older model can't handle complex scheduling constraints
   - Solution: Upgrade to more capable model (e.g., Sonnet → Opus)
   - Prompting alone won't fix

2. **Behavior issue** — Model has ability but takes wrong approach
   - Example: Model calculates prorated billing incorrectly (mental math vs tool use)
   - Solution: Improve [[concepts/prompt-engineering]], provide [[concepts/tool-use-patterns]]
   - Doesn't require new model

**Evaluation reveals which**:
- If upgrade to better model significantly improves results → capability gap
- If better [[concepts/prompt-engineering]] fixes issue → behavior issue

## How It Works

**Hierarchy of Models** (capacity/capability):

```
Sonnet 4.6
  ↓ (more capable)
Opus 4.7
  ↓ (more capable)
Opus 4.7 + Adaptive Thinking
```

**Decision Framework**:

1. **Start with smallest capable model** (e.g., Sonnet)
2. **Optimize prompting** — Try structured prompts, [[concepts/agentic-loops]], [[concepts/tool-use-patterns]]
3. **If still insufficient** — Try [[concepts/adaptive-thinking]] for reasoning boost
4. **If still insufficient** — Upgrade model (Sonnet → Opus)
5. **If cost/latency critical** — Return to step 2 with larger model but tighter prompt optimization

## Key Parameters

- **Quality required** — How perfect must outputs be? (90% ok? 99%? 99.9%?)
- **Latency budget** — Real-time (< 1s)? Interactive (< 10s)? Batch (flexible)?
- **Token budget** — Cost per request; scales with model size
- **Capability level** — Does model have required reasoning/knowledge?
- **Behavior flexibility** — Can prompting achieve behavior change or do we need more capable model?

## When To Use Different Models

| Scenario | Best Model | Reasoning |
|----------|-----------|-----------|
| Fact lookup, summarization | Sonnet 4.6 | Low complexity, cost effective |
| General coding, content | Opus 4.7 | Good balance of capability and cost |
| Complex multi-step reasoning | Opus 4.7 + Adaptive | Maximum reasoning, cost secondary |
| Constrained cost, best effort | Sonnet + optimized | Maximize quality within tight budget |
| Specialized domain (coding, math) | Model-specific | Use task-specific capability leaders |

## Risks & Pitfalls

- **Over-upgrading** — Paying for Opus when Sonnet + better prompting works fine
- **Under-upgrading** — Stuck trying to fix capability gap through prompting alone
- **False economy** — Optimization time cost can exceed cost of using larger model
- **Feature lock-in** — Building on model-specific capabilities then unable to switch
- **Cold start problem** — Hard to tell if new model needs different prompting approach

## Trade-offs

### Quality vs. Cost
```
High Quality:     Opus 4.7 + Adaptive Thinking (3x cost, 3x latency)
Balanced:         Opus 4.7 (1.5x cost, 1.5x latency)
Cost-optimized:   Sonnet 4.6 + agentic loop (1.2x cost, 1.1x latency)
Budget:           Sonnet 4.6 with optimized prompt (1x cost, 1x latency)
```

### Architecture Coupling
- **Tightly coupled to model** — Use model-specific features (structure output, thinking)
- **Loosely coupled** — Design prompts portable across models
- **Abstraction layer** — Use [[concepts/langchain-agents]] or similar to swap models easily

## Related Concepts

- [[concepts/prompt-engineering]] — Often better ROI than model upgrade
- [[concepts/evaluation-frameworks]] — Essential for distinguishing capability vs behavior gaps
- [[concepts/adaptive-thinking]] — API feature that affects model choice equation
- [[concepts/agentic-loops]] — Can achieve high quality with cheaper model
- [[concepts/token-optimization]] — Cost optimization perspective on model choice
- [[concepts/instruction-following-limits]] — Larger models follow instructions better

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Employee scheduling: Sonnet 4.6 failed, Opus 4.7 improved, Opus 4.7 + adaptive thinking succeeded but at cost; agentic loop with Sonnet matched quality at lower cost
