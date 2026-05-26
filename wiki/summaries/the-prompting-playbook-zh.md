---
title: "提示词手册：维护与构建智能体的最佳实践"
type: summary
tags: [prompt-engineering, agent-design, evaluation, chinese-content]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Key Points

### Scenario 1: Maintaining Existing Prompts (Customer Service Bot)

- **General hygiene cleanup** provides immediate performance improvements:
  - Add XML tags to structure different sections (role, policies, guidelines, tone)
  - Remove redundant/copied information
  - Define clear output contracts with stop sequences
  - Apply these before deep debugging

- **Information hiding problem**: Models can over-optimize defensive instructions meant for previous model versions, actively hiding accessible information instead of revealing it
  - Example: Overly restrictive instruction to "never give wrong plan details" caused model to withhold correct information from customer data
  - Fix: Balance instructions to mention both costs and benefits of decisions

- **Tool integration for capabilities**: Instructions alone cannot add capabilities
  - Model told to "always calculate prorated amounts accurately" still performed poor mental math
  - Solution: Provide actual tools/functions for calculations; model will use them reliably

- **Balancing trade-offs**: When models become more sophisticated, they optimize trade-offs better
  - Instructions stating only downside (cost of escalation) cause over-optimization
  - Fix: Present both sides of trade-offs so model can decide appropriately

### Scenario 2: Building New Agentic Systems (Employee Scheduling)

- **Three approaches tested**:
  1. **Simple model + simple prompt** (Sonnet 4.6): All test cases failed
  2. **Larger model** (Opus 4.7): Reduced violations significantly but still failed
  3. **Adaptive thinking enabled**: Reliable output but 3x tokens/latency cost
  4. **Optimized prompt + smaller model**: Some passes but hit token limits
  5. **Agentic loop** (generate-evaluate-fix): All tests pass, lowest tokens, lowest latency ✓

- **Agentic loop approach** (best for this problem):
  - Generator prompt: Creates initial schedule
  - Evaluator prompt: Identifies specific violations with evidence
  - Fixer prompt: Makes targeted repairs based on reported violations
  - Benefits: Uses fewer tokens, lower latency, allows runtime soft constraints

- **Key insight**: Splitting complex tasks into separate simpler prompts, run sequentially, often outperforms single large prompt trying to do everything

### General Principles

- **Evaluations are foundational**: Needed to ensure prompt changes correlate with performance improvements, distinguish three case types (control, edge cases, capability boundaries)
- **Separate concerns**: If you can't distinguish guidelines/policies/data in a prompt, neither can the model
- **Version control on patches**: Track why defensive changes were added; they may become counter-productive with newer models
- **Structured output**: Use stop sequences and output formats to ensure consistency
- **Cost-latency trade-offs**: Larger models with adaptive thinking vs optimized prompts with smaller models are both valid depending on constraints

## Relevant Concepts

- [[prompt-engineering]]
- [[evaluation-frameworks]]
- [[agentic-loops]]
- [[tool-use-patterns]]
- [[model-selection]]
- [[agent-skills]]
- [[adaptive-thinking]]
- [[output-contracts]]

## Source Metadata

**Type**: Video transcript (conference talk)
**Author**: Margot Vanlar, Applied AI Engineer at Anthropic
**Date**: 2026-05-22
**Source URL**: https://www.youtube.com/watch?v=G2B0YWuJUgI&list=PLmWCw1CzcFilPJdvw6scjHjbBripZWFps&index=5
**Original Title**: The Prompting Playbook (Chinese translation)
