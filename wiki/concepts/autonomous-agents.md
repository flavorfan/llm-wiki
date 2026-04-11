---
title: "Autonomous Agents"
type: concept
tags: [llm-agents, foundational, automation, well-established]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Autonomous Agents

## Definition

Autonomous agents are AI systems that can operate independently without continuous human intervention, making decisions, taking actions, and adapting based on feedback from their environment. [[concepts/auto-research]] represents "the clearest example of what AI agents actually look like in practice" - not just chatbots, but real autonomous loops doing meaningful work.

## How It Works

**Core characteristics:**
- Operate without human in the loop
- Make decisions based on objective criteria
- Take actions that modify state (code, configuration, content)
- Evaluate outcomes of their actions
- Adjust strategy based on results
- Continue running for extended periods (overnight, days, weeks)

**In AutoResearch context:**
1. Agent runs continuously in "bypass permissions" or "Yolo mode"
2. Generates hypotheses autonomously
3. Modifies designated files
4. Evaluates results using predefined metrics
5. Commits successes or resets failures
6. No human approval needed for each iteration

**Contrast with chatbots:**
- Chatbots: Respond to human prompts, wait for next instruction
- Autonomous agents: Set in motion with goals, run until completion or stopped
- "Not just chatbots, but real autonomous loops that do meaningful work"

## Key Parameters

**Degree of autonomy:**
- **Supervised**: Human approves each action
- **Semi-autonomous**: Human sets goals, agent executes within bounds
- **Fully autonomous**: Human defines metric and constraints, agent handles everything

**AutoResearch configuration:**
- Fully autonomous within [[concepts/three-file-architecture]] constraints
- Cannot modify goals (program.md) or metrics (prepare.py)
- Can run indefinitely (~100 experiments overnight)
- No human decision points in experiment loop

**Infrastructure requirements:**
- IDE with agent support ([[entities/claude-code]], [[entities/cursor]])
- Permission bypass mode for continuous operation
- Git for rollback mechanism
- Automated evaluation system

## When To Use

**Ideal scenarios:**
- **High-volume experimentation**: When you need 100+ experiments, not 10
- **Clear success criteria**: Objective metrics, no human judgment needed
- **Repetitive optimization**: Same type of task repeated with variations
- **Time-intensive tasks**: Overnight or multi-day runs
- **Exploration tasks**: Search large solution spaces systematically

**Practical applications:**
- ML hyperparameter tuning (runs while you sleep)
- Marketing A/B testing at scale (100/day vs 30/year)
- Code performance optimization (systematic testing)
- Trading strategy refinement (backtesting variations)
- Prompt engineering (testing formulations)

**Business transformation:**
> "Soon enough, the execution of any work or task will become basically free. What will become valuable is knowing what to measure, picking the right metric, and setting the right constraints."

The skill shifts from execution to goal-setting and metric-design.

## Risks & Pitfalls

**Loss of control:**
- Agents can make many changes quickly
- Need rollback mechanism (git)
- Must have immutable constraints (program.md, prepare.py)

**Bad objectives:**
- Wrong metric → confident optimization in wrong direction
- Subjective goals → agent cannot evaluate properly
- Ambiguous constraints → unpredictable behavior

**Resource consumption:**
- Can consume significant compute (API tokens, cloud resources)
- Overnight run might cost hundreds of dollars
- Need budget limits and monitoring

**Safety mechanisms needed:**
- Immutable goal definitions
- Immutable evaluation metrics
- Version control for rollback
- Resource limits and timeouts
- Clear scope boundaries (one file to modify)

## Related Concepts

- [[concepts/auto-research]] — Framework for autonomous optimization agents
- [[concepts/experiment-loop]] — The autonomous iteration pattern
- [[concepts/recursive-self-improvement]] — Agents improving themselves
- [[concepts/metric-driven-optimization]] — Objective guidance for autonomy

## Related Entities

- [[entities/andrej-karpathy]] — Pioneering autonomous research agents
- [[entities/claude-code]] — Tool supporting autonomous operation
- [[entities/cursor]] — IDE with autonomous agent support
- [[entities/david-andre]] — Explains agent autonomy in tutorials

## Sources

- [[summaries/autoresearch-tutorial]] — Demonstrates fully autonomous agents in practice

## Evolution: From Chatbots to Agents

**2022-2023**: ChatGPT era
- Conversational AI, human-driven
- Responds to prompts
- No persistence between sessions
- Human in every decision

**2024-2026**: Agent era
- Task-driven AI, goal-oriented
- Autonomous execution
- Persistent state (git, memory)
- Human sets goals, agent executes

**AutoResearch insight:**
This is what the progression was building toward - not better chatbots, but autonomous systems doing real work while humans sleep. The goal was always agents, not conversations.
