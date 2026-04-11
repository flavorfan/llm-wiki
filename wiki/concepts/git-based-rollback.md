---
title: "Git-Based Rollback"
type: concept
tags: [auto-research, version-control, workflow, experimentation]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Git-Based Rollback

## Definition

Git-based rollback is the practice of using version control (git) to manage experiment state in [[concepts/auto-research]]. Successful experiments are committed to git history; failed experiments trigger `git reset --hard` to instantly revert to the last known good state. This creates a clean binary decision mechanism with no partial states or manual undo.

## How It Works

**Basic mechanism:**

**For successful experiments:**
1. Agent modifies train.py
2. Runs evaluation
3. Metric improves
4. System runs: `git commit -m "Description: baseline → improved"`
5. Commit becomes new baseline

**For failed experiments:**
1. Agent modifies train.py
2. Runs evaluation
3. Metric gets worse
4. System runs: `git reset --hard`
5. Instantly reverts to last commit (previous success)
6. Failed change leaves no trace

**Git history as optimization trajectory:**
- Each commit = successful experiment
- Commit message shows metric improvement
- Can see full optimization path
- Can rollback to any previous state
- Failed experiments never appear in history

## Key Parameters

**Commit strategy:**
- One commit per successful experiment
- Commit message format: "Change description: oldMetric → newMetric"
- Example: "Remove unused CSS: 50ms → 33ms"
- Commits are automatic (agent or system creates them)

**Reset strategy:**
- Always hard reset: `git reset --hard`
- Not soft reset (doesn't preserve changes)
- Not mixed reset (doesn't preserve staging)
- Completely discard failed experiment

**Branch management:**
- Typically work on non-main branch
- Can create dedicated AutoResearch branch
- Keeps main branch clean
- Can review optimization trajectory before merging

**Baseline tracking:**
- Initial commit establishes baseline
- File `results.tsv` or similar tracks metrics over time
- Each commit updates baseline for comparison
- Clear audit trail of improvements

## When To Use

**Essential for:**
- [[concepts/auto-research]] workflows (core requirement)
- Any autonomous optimization where failures must be discarded
- High-volume experimentation (100+ experiments)
- Overnight or unsupervised runs

**Advantages:**
- **Clean state**: No accumulation of failed changes
- **Instant rollback**: `git reset --hard` is milliseconds
- **Audit trail**: Git history shows what worked
- **Safety**: Can always revert to earlier state
- **Automation**: No manual undo or file management

**Works well with:**
- Automated experiment loops
- Continuous integration
- Reproducible research
- Collaborative optimization (multiple agents)

## Risks & Pitfalls

**Destructive by design:**
`git reset --hard` permanently discards uncommitted work. This is intentional for AutoResearch (discard failed experiments), but dangerous if:
- You have uncommitted work you want to keep
- You run AutoResearch on wrong branch
- You need to analyze why experiments failed

**Lost debugging info:**
Failed experiments leave no trace, making it hard to understand what doesn't work. Consider logging before reset.

**Branch confusion:**
Running AutoResearch on main/master can pollute production branch. Always use dedicated branch.

**Merge conflicts:**
If running multiple AutoResearch processes in parallel, can create git conflicts requiring manual resolution.

**Solutions:**
- Always use dedicated branch for AutoResearch
- Log all experiments (success + failure) before git operations
- Consider keeping results.tsv file with full history
- Review optimization trajectory before merging to main

## Related Concepts

- [[concepts/auto-research]] — Framework that uses this pattern
- [[concepts/experiment-loop]] — Loop that implements commit/reset decisions
- [[concepts/three-file-architecture]] — train.py is what gets committed/reset

## Related Entities

- [[entities/andrej-karpathy]] — Designed this rollback pattern

## Sources

- [[summaries/autoresearch-tutorial]] — Explains git commit/reset workflow

## Example: Website Optimization Session

**Initial state:**
```
git log:
abc123 Baseline: portfolio website, 50ms load time
```

**Experiment 1 (success):**
- Agent removes unused CSS
- Metric: 50ms → 33ms
- Action: `git commit -m "Remove unused CSS: 50ms → 33ms"`

**After experiment 1:**
```
git log:
def456 Remove unused CSS: 50ms → 33ms
abc123 Baseline: portfolio website, 50ms load time
```

**Experiment 2 (failure):**
- Agent adds image compression
- Metric: 33ms → 45ms (worse!)
- Action: `git reset --hard` (back to def456)
- No trace in git history

**Experiment 3 (success):**
- Agent inlines critical CSS
- Metric: 33ms → 28ms
- Action: `git commit -m "Inline critical CSS: 33ms → 28ms"`

**Final state:**
```
git log:
ghi789 Inline critical CSS: 33ms → 28ms
def456 Remove unused CSS: 50ms → 33ms
abc123 Baseline: portfolio website, 50ms load time
```

**Git history shows:**
- Clean optimization trajectory: 50ms → 33ms → 28ms
- Only successful experiments visible
- Clear understanding of what worked
- Failed image compression experiment left no trace

## Comparison to Other Approaches

**Manual undo:**
- Slow (human has to undo changes)
- Error-prone (might miss some changes)
- Doesn't scale (can't run overnight)

**Backup files:**
- Clutters filesystem
- Manual management required
- Unclear which is "current" version

**Git stash:**
- Preserves failed experiments (unnecessary)
- More complex than needed
- Stash stack can get confusing

**Git hard reset:**
- ✅ Instant (milliseconds)
- ✅ Complete (no missed changes)
- ✅ Scalable (automated)
- ✅ Simple (one command)
- ✅ Clean (no file clutter)

Git reset is the right tool for this job because the goal is to discard failures completely and permanently.
