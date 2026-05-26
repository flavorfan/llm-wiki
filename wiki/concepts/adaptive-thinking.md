---
title: "Adaptive Thinking"
type: concept
tags: [reasoning, model-capabilities, inference, extended-computation, well-established]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Adaptive thinking is a capability where language models allocate computational budget dynamically based on problem difficulty. Instead of fixed-depth reasoning, the model decides when it needs more reasoning steps vs. when it can answer directly. This is an API-level feature (not a prompting technique) that affects both output quality and token/latency costs.

## How It Works

**Model Behavior**:
- Model internally determines if problem requires extended reasoning
- Allocates "thinking tokens" for complex problems
- Uses fewer resources for straightforward questions
- Returns both reasoning process and final answer

**Contrasts with**:
- **Fixed reasoning** — Model always uses same reasoning depth (wasteful on easy questions)
- **Chain-of-thought prompting** — User explicitly asks "think step by step" (more coercive, less elegant)
- **Prompt optimization** — Can improve quality but inherently bounded by single pass

## How It Works

**Trade-offs in Employee Scheduling Example**:

| Approach | Accuracy | Tokens | Latency | Cost |
|----------|----------|--------|---------|------|
| Sonnet 4.6 (simple) | 0/5 pass | baseline | baseline | baseline |
| Sonnet 4.6 (optimized) | 2/5 pass | baseline | baseline | baseline |
| Opus 4.7 | 4/5 pass | 1.5x | 1.5x | 1.5x |
| **Opus 4.7 + adaptive** | **5/5 pass** | **3x** | **3x** | **3x** |
| Agentic loop | 5/5 pass | 1.2x | 1.1x | 1.2x |

Adaptive thinking improved accuracy but at significant cost increase.

## Key Parameters

- **Budget allocation** — How much computational budget to allocate to thinking
- **Problem complexity detection** — How does model determine if problem needs deep reasoning?
- **Token limit** — Maximum thinking tokens allowed per request
- **Output detail** — Whether to expose reasoning process to user

## When To Use

- **Complex reasoning tasks** — Multi-step logic, constraint satisfaction, strategy
- **When accuracy >> cost** — Medical diagnosis, legal review, high-stakes decisions
- **When latency is flexible** — Not real-time constrained
- **Exploratory phases** — Early development when finding right approach matters more than optimization
- **Comparison baseline** — When deciding between approaches, use adaptive thinking as upper bound

## When NOT to Use

- **Real-time systems** — 3x latency is unacceptable
- **High-volume operations** — 3x token cost is prohibitive
- **Simple factual lookup** — Wasteful to enable deep reasoning for straightforward questions
- **Cost-constrained scenarios** — Tight budget suggests optimization over capability increase
- **Decision already made** — If agentic loop or optimized prompts are already working

## Risks & Pitfalls

- **Token cost explosion** — Easy to exceed budget if reasoning gets stuck in loops
- **False confidence** — More reasoning doesn't always mean better answers
- **Latency unacceptability** — 100+ second responses unworkable for interactive systems
- **Over-reliance** — Team defaults to "just use adaptive thinking" instead of proper design

## Architectural Role

Usually one of several options in tech stack:

1. **Lightweight inference** — Optimized prompt + smaller model (e.g., Sonnet)
2. **Balanced** — Standard model (e.g., Opus without adaptive thinking)
3. **High-quality** — Larger model with adaptive thinking enabled
4. **Agentic** — Multiple simpler prompts chained together

Choose based on quality requirements vs. cost/latency constraints.

## Related Concepts

- [[concepts/model-selection]] — Adaptive thinking is one aspect of model choice
- [[concepts/prompt-engineering]] — Optimized prompts often outperform relying on adaptive thinking alone
- [[concepts/agentic-loops]] — Can achieve high quality with lower cost/latency than adaptive thinking
- [[concepts/token-optimization]] — Tension between reasoning depth and budget
- [[concepts/instruction-following-limits]] — Models with more reasoning can sometimes follow instructions better

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Employee scheduling comparison: Opus 4.7 with adaptive thinking vs optimized Sonnet 4.6 with agentic loop
