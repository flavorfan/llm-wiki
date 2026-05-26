---
title: "Prompt Engineering"
type: concept
tags: [prompt-engineering, llm-agents, ai-coding, foundational, well-established]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Prompt engineering is the discipline of crafting instructions that guide language models to produce desired outputs. It encompasses writing clear role definitions, specifying constraints, structuring information hierarchically, and iteratively refining prompts based on evaluation results.

## How It Works

**Foundational Hierarchy**:
1. **Role definition** — Who/what is the model? (e.g., "You are a customer service bot")
2. **General guidelines** — Broad behavioral rules, reasoning approach
3. **Policies** — Business logic, constraints, rules that must be followed
4. **Tone & style** — How to communicate with the user
5. **Output contract** — Exact format expected from the model

**Hygiene Principles** (apply before deep debugging):
- Use XML tags to structure different sections visibly
- Remove redundant/copied information
- Define output format explicitly
- Apply stop sequences to enforce structure
- If you can't distinguish sections by reading, neither can the model

**Iteration Process**:
1. Create baseline prompt with clear structure
2. Build [[concepts/evaluation-frameworks]] to test outputs
3. Identify failure patterns systematically
4. Address each failure with targeted changes
5. Verify improvements with fresh evaluations

## Key Parameters

**Prompt Components**:
- **Role statement** — Clear, specific identity for the model
- **Context data** — Information the model needs (customer info, policies, examples)
- **Instructions** — Explicit steps or behaviors
- **Constraints** — Rules, exceptions, boundaries
- **Output format** — Expected structure (JSON, XML, prose with formatting)

**Effectiveness factors**:
- Clarity and lack of ambiguity
- Proper separation of concerns
- Balance in presenting trade-offs (don't hide downsides)
- Version control on defensive patches

## When To Use

- Building new [[concepts/autonomous-agents]] systems
- Debugging underperforming models after migration
- Maintaining complex prompts in production
- Improving consistency of model outputs
- Teaching models new reasoning approaches

## Risks & Pitfalls

### Anti-Patterns to Avoid

- **Over-defensive instructions** — Rules added to patch previous model versions become counter-productive with newer models
  - Example: "Never give wrong plan details" → model withholds correct information it has access to
  - Fix: Track why each defensive instruction was added; re-evaluate with each model update

- **Instruction-only solutions for capability gaps** — Telling a model to "always calculate accurately" doesn't improve its math
  - Fix: Provide actual [[concepts/tool-use-patterns]] for calculations; model will use them reliably

- **Mixing instruction types** — Large paragraphs without clear boundaries
  - Models struggle to distinguish policies from guidelines from tone
  - Fix: Use XML tags, sections, bullet points to separate concerns

- **Imbalanced trade-off descriptions** — Stating only costs, not benefits, causes over-optimization
  - Example: "Escalation costs $8" without mentioning benefits of accuracy
  - Fix: Present both sides of decisions so model balances them appropriately

- **Overly rigid output formats** — Too strict can cause model to constrain important information
  - Fix: Use [[concepts/output-contracts]] but leave room for context

### Model Capability vs. Behavior

When migrating to new models:
- **Capability issue** — New model lacks the ability; no prompt fix helps
- **Behavior issue** — New model has ability but different approach; prompting can redirect

Use [[concepts/evaluation-frameworks]] to distinguish between these cases.

## Related Concepts

- [[concepts/evaluation-frameworks]] — Essential for testing prompt changes
- [[concepts/tool-use-patterns]] — When prompts need to be paired with tools
- [[concepts/output-contracts]] — Structuring what the model should return
- [[concepts/agentic-loops]] — Multi-step prompting patterns
- [[concepts/instruction-following-limits]] — Why some instructions don't work
- [[concepts/adaptive-thinking]] — Enabling deeper reasoning in models
- [[concepts/agent-skills]] — Encapsulating domain-specific prompts

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Chinese translation of Margot Vanlar's conference talk on prompt maintenance and new agent building
