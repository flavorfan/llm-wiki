---
title: "Three-File Architecture"
type: concept
tags: [auto-research, architecture, foundational, experimentation]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Three-File Architecture

## Definition

The three-file architecture is the structural pattern at the core of [[concepts/auto-research]]. It consists of exactly three files with distinct roles: one that defines the goal, one that the agent can modify, and one that evaluates the result. This separation prevents cheating and ensures objective optimization.

## How It Works

**The three files:**

1. **program.md** — The goal setter
   - Written by human
   - Defines objectives, constraints, and rules
   - **Agent cannot modify this**
   - Most important file in the system
   - Can borrow prompt engineering from Karpathy's examples

2. **train.py** — The optimization target
   - The ONE file the agent can modify
   - Can be code, config, prompt, math equation, or anything optimizable
   - Not actually required to be Python despite the name
   - Could be HTML, CSS, trading strategy, etc.
   - "Not two, not zero, one file"

3. **prepare.py** — The truth teller
   - Defines what "better" means
   - Contains the evaluation script and metric
   - **Agent absolutely cannot touch this**
   - Prevents agent from rewriting scoring function to fake results
   - Without this limitation, agent could cheat the eval

## Key Parameters

**Immutability rules:**
- program.md: Human sets once, agent never modifies
- train.py: Agent's playground, human rarely touches
- prepare.py: Human defines metric, agent never sees write access

**Separation of concerns:**
- **Goal setting** (program.md) separated from **execution** (train.py)
- **Execution** (train.py) separated from **evaluation** (prepare.py)
- This prevents the optimizer from manipulating the scoring function

**File naming flexibility:**
- Names are conventional, not rigid
- "train.py" can be any language or format
- "prepare.py" could be "benchmark.mjs" (Puppeteer example)
- "program.md" could be any instruction format

## When To Use

**Use this architecture when:**
- Building autonomous optimization loops
- Need to prevent agent from cheating metrics
- Want clear separation between goals and execution
- Implementing any [[concepts/auto-research]] workflow

**Pattern applies to:**
- ML model training (original use case)
- Web performance optimization
- Trading strategy development
- Marketing copy optimization
- Prompt engineering
- Any metric-driven optimization

## Risks & Pitfalls

**Critical mistake:**
Allowing agent write access to prepare.py → agent will optimize the scoring function instead of the actual target

**Wrong metric in prepare.py:**
Agent will confidently optimize in wrong direction with perfect scores

**Multiple modifiable files:**
Violates the "one file" principle, makes experiment comparison unclear

**No separation:**
If agent can modify both the code and the eval, the system loses objectivity

## Related Concepts

- [[concepts/auto-research]] — Framework that uses this architecture
- [[concepts/experiment-loop]] — The process that operates on these files
- [[concepts/metric-driven-optimization]] — prepare.py defines the metric
- [[concepts/git-based-rollback]] — train.py changes get committed or reset

## Related Entities

- [[entities/andrej-karpathy]] — Designed this architecture
- [[entities/david-andre]] — Explains the architecture in tutorial

## Sources

- [[summaries/autoresearch-tutorial]] — Detailed explanation of three-file pattern

## Example: Website Optimization

**program.md:**
```markdown
You are optimizing a portfolio website for load time.
Goal: Minimize median load time in milliseconds.
Constraints: Must maintain visual appearance.
Rules: Run benchmark after each change.
```

**train.py (actually index.html, style.css, server.js):**
- The website files the agent modifies
- HTML structure, CSS styling, server configuration
- Agent experiments with minification, caching, compression

**prepare.py (actually benchmark.mjs):**
- Puppeteer script measuring load time
- Launches browser, loads page, records milliseconds
- Returns single number: median load time
- Agent cannot modify this measurement logic
