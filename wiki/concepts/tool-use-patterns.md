---
title: "Tool Use Patterns"
type: concept
tags: [tools, prompting, capabilities, design-patterns, llm-agents, well-established]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Tool use patterns are strategies for augmenting language models with external functions to perform tasks they cannot do reliably alone. The key insight: **instructions cannot add capabilities**. Telling a model to calculate accurately doesn't improve its mental math; giving it a calculator does.

## How It Works

**Three Components Required**:

1. **Tool Definition** — Tell the model what tool exists
   ```
   You have access to: calculate_prorated_amount(base_price, days_used, total_days)
   Use this whenever you need to calculate any prorated amounts.
   ```

2. **Prompt Integration** — Embed tool availability into [[concepts/prompt-engineering]]
   ```xml
   <instructions>
     When the customer asks about prorated billing, 
     use the calculate_prorated_amount tool instead of doing mental math.
   </instructions>
   ```

3. **Implementation** — Actual function that executes
   ```python
   def calculate_prorated_amount(base_price, days_used, total_days):
       return (base_price / total_days) * days_used
   ```

**Critical Principle**: Model still needs to understand *when* to use the tool and *how to interpret* results. Prompting handles the "when"; implementation handles the "how."

## Key Parameters

- **Tool definition clarity** — Model must understand what the tool does
- **Tool signature** — Input/output types, required vs optional parameters
- **Error handling** — What happens if tool fails or returns unexpected format
- **Invocation semantics** — How does model request tool use (function calling, plugin syntax, etc.)
- **Context inclusion** — Can model see tool outputs to reason further?

## When To Use

- **Deterministic calculations** — Math, date arithmetic, unit conversion
- **Database lookups** — Retrieve facts, policies, customer records
- **System integration** — Call APIs, webhooks, external services
- **Complex logic** — Decision trees, rule evaluation
- **Capability boundaries** — Tasks where model accuracy matters critically

## Anti-Patterns to Avoid

### ❌ Pure Instruction Approach
"Always calculate prorated amounts accurately."
- Result: Model attempts mental math, makes errors
- Problem: Instructions don't add capabilities

### ✓ Tool-Based Approach
Provide `calculate_prorated_amount()` function
- Result: Model calls tool, gets accurate answer
- Benefit: Deterministic, testable, maintainable

### ❌ Missing Integration
Tool exists in system but prompt doesn't mention it
- Result: Model doesn't know to use it
- Problem: Model still does mental math

### ✓ Explicit Prompt Integration
Prompt clearly states: "Use calculate_prorated_amount for all prorated amounts"
- Result: Model reliably uses tool

## Failure Modes

- **Over-fetching** — Model calls tool when it could reason (waste of latency/tokens)
- **Under-utilization** — Tool available but model doesn't know or doesn't use it
- **Tool errors** — Function fails, crashes, or returns invalid data
- **Ambiguous invocation** — Model unsure how to call or interpret results
- **Hallucination** — Model invents tool names that don't exist

## Related Concepts

- [[concepts/prompt-engineering]] — Prompt must explain what tools are available
- [[concepts/evaluation-frameworks]] — Test that tool use is both attempted and successful
- [[concepts/agentic-loops]] — Each stage may call different tools
- [[concepts/langgraph]] — Implements tool use in state machine workflows
- [[concepts/mcp-servers]] — Model Context Protocol for tool standardization

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Prorated billing calculation example: model failed with mental math until tool was provided
