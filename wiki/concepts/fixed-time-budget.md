---
title: "Fixed Time Budget"
type: concept
tags: [auto-research, experimentation, fairness, methodology]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Fixed Time Budget

## Definition

Fixed time budget is the constraint in [[concepts/auto-research]] that every experiment runs for exactly the same amount of time (e.g., 5 minutes). This ensures fair comparison between experiments, preventing the agent from "cheating" by simply training longer rather than finding better ideas.

## How It Works

**Basic principle:**
- All experiments get same time allocation
- Typical budget: 5 minutes per experiment
- Agent cannot extend time for promising experiments
- Agent cannot stop early if experiment looks bad
- Only the quality of the idea matters, not time invested

**Analogy from tutorial:**
> "If you're hiring for your company. If you have one applicant and you give him 7 days to complete the task and the other one only has 7 minutes, then obviously the one who has 7 days, on average, will do better."

Same principle applies to AI experiments. If one experiment gets 10 minutes and another gets 5 minutes, they're not comparable.

**In practice:**
- Set time budget at start (e.g., `timeout: 300` seconds)
- All training/testing runs for exactly that duration
- Evaluation compares results after identical time investment
- Agent learns which ideas work within time constraint

## Key Parameters

**Time budget magnitude:**
- **Seconds**: For very fast tasks (web performance, simple tests)
- **Minutes**: For moderate tasks (typical ML training, optimization)
- **Hours**: For expensive tasks (large model training, extensive backtesting)

**Typical AutoResearch settings:**
- 5 minutes per experiment (standard)
- ~100 experiments overnight (~8 hours)
- ~12 experiments per hour at 5 min each

**Trade-offs:**
- **Shorter budget**: More experiments, less thorough testing, might miss slow improvements
- **Longer budget**: Fewer experiments, more thorough testing, might waste time on obviously bad ideas

**Calculation:**
```
Total experiments = Available time / (Time budget + Evaluation time + Overhead)
```

Example: 8 hours overnight, 5 min training, 10 sec evaluation, 20 sec overhead:
```
8 hours = 480 minutes
480 / (5 + 0.17 + 0.33) ≈ 87 experiments
```

## When To Use

**Essential for:**
- Comparing optimization strategies fairly
- Any [[concepts/auto-research]] workflow
- Benchmarking where fairness matters
- Preventing time-based advantage in experiments

**Especially important when:**
- Different approaches have different convergence rates
- Some ideas look good early but plateau
- Some ideas start slow but improve consistently
- You want to isolate idea quality from compute investment

**Applies to:**
- ML model training (epochs/steps limited by time)
- Trading backtests (same time period for all strategies)
- A/B tests (same traffic volume or duration)
- Performance optimization (same benchmark duration)

## Risks & Pitfalls

**Too short:**
- Not enough time to see meaningful differences
- High variance in results (noise dominates signal)
- Ideas don't get chance to demonstrate potential

**Too long:**
- Fewer total experiments (lower throughput)
- Diminishing returns (most gain happens early)
- Wasted compute on obviously bad ideas

**Variable task complexity:**
If some experiments are inherently faster (e.g., smaller models), fixed time might not be fair comparison. Consider fixed compute budget instead.

**Early stopping temptation:**
Agent might want to stop early if experiment looks promising/bad, but this violates fair comparison principle.

**Solution:**
- Choose budget based on typical convergence time
- Allow some preliminary runs to calibrate
- Document budget choice in program.md
- Consistent budget within a session (can change for new sessions)

## Related Concepts

- [[concepts/auto-research]] — Framework that uses this principle
- [[concepts/experiment-loop]] — Each loop iteration gets same budget
- [[concepts/metric-driven-optimization]] — Metrics compared after equal time
- [[concepts/autonomous-agents]] — Need fair comparison for autonomous operation

## Related Entities

- [[entities/andrej-karpathy]] — Emphasizes importance in AutoResearch design

## Sources

- [[summaries/autoresearch-tutorial]] — Explains fixed time budget rationale

## Example: Website Optimization

**Scenario:** Optimizing portfolio website load time

**Time budget:** 5 minutes per experiment

**Experiment 1: Remove unused CSS**
- Time spent: exactly 5 minutes
- Metric: 50ms → 33ms
- Improvement: 17ms

**Experiment 2: Add image compression**
- Time spent: exactly 5 minutes (even though result looked bad after 1 minute)
- Metric: 33ms → 45ms
- Degradation: -12ms

**Experiment 3: Inline critical CSS**
- Time spent: exactly 5 minutes (even though result looked good after 2 minutes)
- Metric: 33ms → 28ms
- Improvement: 5ms

**Without fixed time budget:**
- Agent might spend 10 minutes on experiment 3 because it looked promising
- Or might stop experiment 2 after 1 minute because it looked bad
- Comparisons become invalid

**With fixed time budget:**
- All three experiments directly comparable
- Can confidently rank: Experiment 1 > Experiment 3 > Experiment 2
- Only idea quality determines success, not time investment

## Fairness Principle

**Core insight:**
You want to compare **ideas**, not **compute investment**.

Fixed time budget ensures:
- Same opportunity for every idea
- No advantage to "expensive but mediocre" ideas
- Encourages efficient improvements (big gains in short time)
- Discourages brute-force approaches (more compute ≠ better result)

This is the scientific method applied to optimization: control for confounding variables (time) to isolate the variable of interest (idea quality).

## Overnight Run Example

**Setup:**
- Time budget: 5 minutes per experiment
- Available time: 8 hours (sleep duration)
- ~100 experiments possible

**Without agent (manual):**
- Human runs maybe 5-10 experiments in same 8 hours
- Each takes more time due to context switching
- Inconsistent evaluation (tired, distracted)

**With AutoResearch + fixed time budget:**
- Agent runs ~100 experiments
- Each gets exactly 5 minutes
- Consistent evaluation
- Best improvements identified automatically

**Result:**
10-20x more experiments, perfectly fair comparison, best solutions automatically committed. This is the automation multiplier effect.
