---
title: "Experiment Loop"
type: concept
tags: [auto-research, experimentation, workflow, foundational]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Experiment Loop

## Definition

The experiment loop is the core iteration pattern of [[concepts/auto-research]]: hypothesis → modify code → train/test → evaluate → commit if improved OR git reset if worse → repeat. This loop runs continuously and autonomously, with the agent generating and testing hundreds of experiments to optimize a target metric.

## How It Works

**The six-step cycle:**

1. **Hypothesis generation**
   - Agent proposes theory about what could improve the metric
   - Based on current state and previous experiment results
   - Example: "Minifying CSS will reduce load time"

2. **Code modification**
   - Agent modifies the designated file (train.py)
   - Implements the hypothesis concretely
   - Could be code changes, config tweaks, content variations

3. **Training/testing phase**
   - Run experiment for fixed time budget (e.g., 5 minutes)
   - Time box ensures fair comparison between experiments
   - No early stopping based on intermediate results

4. **Evaluation**
   - Run prepare.py to measure result
   - Get single scalar metric (one number)
   - Compare to baseline or previous best

5. **Decision point**
   - **If improved**: Commit to git history, update baseline
   - **If worse**: `git reset --hard`, revert to previous state
   - No partial commits, no "maybe" outcomes

6. **Repeat**
   - Loop continues indefinitely
   - Each iteration builds on previous successes
   - Typical overnight run: ~100 iterations

## Key Parameters

**Fixed time budget:**
- Ensures fair comparison (prevents "cheat by training longer")
- Typical: 5 minutes per experiment
- Same duration for all experiments in a session
- Makes comparison apples-to-apples

**Scalar metric:**
- One number, clear direction of improvement
- Examples: loss decreases, accuracy increases, load time decreases
- Must be automatically evaluatable
- Defined in immutable prepare.py

**Git-based state management:**
- Each successful experiment = one commit
- Failed experiments leave no trace (hard reset)
- Git history becomes optimization trajectory
- Easy rollback if needed

**Autonomy:**
- No human intervention during loop
- Agent decides all hypotheses
- Automatic evaluation, automatic commit/reset
- Runs while you sleep

## When To Use

**Ideal for:**
- High-volume optimization (need 100+ experiments)
- Clear metric (objective measurement)
- Fast feedback (evaluation completes quickly)
- Exploration problems (large search space)

**Example scenarios:**
- ML model training (original use case)
- Website performance (load time optimization)
- Trading strategies (Sharpe ratio on historical data)
- Marketing copy (conversion rate testing)
- Prompt engineering (success rate on test cases)

**Scale advantage:**
Humans run ~30 experiments/year manually. Experiment loop runs ~36,000/year (100/day) autonomously. 1,200x throughput increase.

## Risks & Pitfalls

**Bad metric:**
Loop will confidently optimize wrong direction if metric is bad. No human checkpoints to catch this.

**Slow evaluation:**
If prepare.py takes hours, loop becomes impractical. Need fast feedback for overnight runs.

**Subjective evaluation:**
If "better" requires human judgment, loop cannot be autonomous. Breaks the pattern.

**No rollback mechanism:**
Without git reset capability, failed experiments accumulate. Git is essential.

**Resource exhaustion:**
Unconstrained loop can consume unlimited API tokens, compute, money. Need budget limits.

## Related Concepts

- [[concepts/auto-research]] — Framework built on this loop
- [[concepts/three-file-architecture]] — Structure the loop operates on
- [[concepts/git-based-rollback]] — How the loop manages state
- [[concepts/fixed-time-budget]] — Fair comparison mechanism
- [[concepts/metric-driven-optimization]] — What guides the loop
- [[concepts/autonomous-agents]] — What runs the loop

## Related Entities

- [[entities/andrej-karpathy]] — Designed this pattern
- [[entities/claude-code]] — Executes the loop autonomously

## Sources

- [[summaries/autoresearch-tutorial]] — Detailed explanation with examples

## Visual Representation

```
┌─────────────────────────────────────┐
│ 1. Agent generates hypothesis       │
└────────────┬────────────────────────┘
             ↓
┌─────────────────────────────────────┐
│ 2. Agent modifies train.py          │
└────────────┬────────────────────────┘
             ↓
┌─────────────────────────────────────┐
│ 3. Run training (fixed time budget) │
└────────────┬────────────────────────┘
             ↓
┌─────────────────────────────────────┐
│ 4. Run prepare.py evaluation        │
└────────────┬────────────────────────┘
             ↓
        ┌────┴────┐
        │ Better? │
        └────┬────┘
         ┌───┴───┐
         │       │
        Yes     No
         │       │
         ↓       ↓
    ┌────────┐ ┌──────────────┐
    │ Commit │ │ Git reset    │
    │ to git │ │ --hard       │
    └───┬────┘ └──────┬───────┘
        └───────┬────┘
                ↓
        ┌───────────────┐
        │ Repeat loop   │
        └───────────────┘
```

## Example: Website Optimization

**Iteration 1:**
- Hypothesis: "Remove unused CSS"
- Modify: Delete 50 lines from style.css
- Test: Run for 5 minutes
- Evaluate: 50ms → 33ms (improved!)
- Action: `git commit -m "Remove unused CSS: 50ms → 33ms"`

**Iteration 2:**
- Hypothesis: "Add image compression"
- Modify: Add compression middleware
- Test: Run for 5 minutes
- Evaluate: 33ms → 45ms (worse!)
- Action: `git reset --hard` (back to 33ms)

**Iteration 3:**
- Hypothesis: "Inline critical CSS"
- Modify: Move critical styles to HTML
- Test: Run for 5 minutes
- Evaluate: 33ms → 28ms (improved!)
- Action: `git commit -m "Inline critical CSS: 33ms → 28ms"`

Loop continues: 50ms → 33ms → 28ms → ... → 25ms over 4 minutes with multiple iterations.
