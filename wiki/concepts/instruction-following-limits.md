---
title: "Instruction-Following Limits"
type: concept
tags: [llm-research, limitations, foundational, prompt-engineering, context-engineering]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Stop Writing Bad CLAUDE.md Files.md", "raw/Writing a good CLAUDE.md"]
confidence: high
---

## Definition

Instruction-following limits refer to the empirically observed constraint that large language models can reliably follow approximately 150-200 discrete instructions simultaneously. Beyond this threshold, instruction-following quality degrades uniformly across all instructions rather than selectively ignoring overflow instructions.

## How It Works

### Capacity Constraints
Research indicates that:
- **Frontier thinking models** (Claude Opus 4.5+): Can follow ~150-200 instructions with reasonable consistency, exhibiting linear decay in performance
- **Smaller models**: Follow significantly fewer instructions with exponential performance decay
- **Non-thinking models**: Have lower instruction capacity than thinking models

### Degradation Pattern
When instruction count exceeds capacity:
1. **Uniform degradation**: All instructions are followed worse, not just the ones added last
2. **No selective ignoring**: The LLM doesn't simply ignore instruction 151+; quality drops across the board
3. **Non-linear effects**: Small increases in instruction count beyond threshold can cause large quality drops in smaller models

### Context Budget Allocation
For Claude Code specifically:
- **System prompt**: ~50 instructions already consumed
- **CLAUDE.md**: Your project instructions
- **Skills/plugins**: Additional instructions when active
- **User messages**: Recent conversation context
- **Total available**: ~150-200 instruction budget for frontier models

This means a 100-line CLAUDE.md file (which often contains multiple instructions per line) can easily exceed the remaining budget after system prompt overhead.

## Key Parameters

### Instruction Counting
One line doesn't equal one instruction:
- "Use TypeScript for all new files" = 1 instruction
- "Use TypeScript for all new files. Prefer interfaces over types. Enable strict mode." = 3 instructions
- A paragraph explaining project structure might contain 5-10 instructions

### Model-Specific Behavior
- **Claude Opus 4.5**: Best instruction-following capacity, linear degradation
- **Smaller models**: Exponential decay, much lower thresholds
- **Thinking vs non-thinking**: Thinking models handle more instructions

### Positional Bias
LLMs prioritize instructions at:
1. **Very beginning** of prompt (CLAUDE.md top, system message)
2. **Very end** of prompt (most recent user messages)
3. **Middle content** gets neglected most

## When To Apply

This knowledge matters for:
- Writing CLAUDE.md files (keep under 300 lines)
- Deciding what to put in base config vs [[concepts/progressive-disclosure]]
- Choosing between instructions and [[concepts/hooks]] for enforcement
- Debugging why Claude ignores certain instructions
- Evaluating whether to use smaller/faster models

## Risks & Pitfalls

### Common Mistakes
1. **Instruction bloat**: Adding "just one more thing" repeatedly until quality collapses
2. **False sense of control**: Assuming more instructions = better control
3. **Ignoring tradeoffs**: Not recognizing that adding one instruction makes all others work slightly worse
4. **Verbal instructions**: Giving verbose instructions that could be enforced by tools
5. **Hypothetical coverage**: Adding instructions for edge cases that rarely occur

### Measurement Challenges
- Hard to count "instructions" precisely in natural language
- Interaction effects between instructions
- Model-specific and prompt-specific variations
- Dynamic instruction count as context evolves

## Related Concepts

- [[concepts/claude-md-configuration]] - Primary configuration file affected by these limits
- [[concepts/progressive-disclosure]] - Technique to stay within limits
- [[concepts/context-window-management]] - Broader resource management strategy
- [[concepts/hooks]] - Alternative to instructions for enforcement
- [[concepts/code-style-automation]] - Using deterministic tools instead of instructions

## Sources

- "Stop Writing Bad CLAUDE.md Files" (camelCase video, 2026-02-04): Cites ~150-200 instruction capacity
- "Writing a good CLAUDE.md" (HumanLayer blog, 2025-11-25): References research showing linear vs exponential decay, positional bias
