---
title: "Metric-Driven Optimization"
type: concept
tags: [auto-research, experimentation, foundational, measurement]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Metric-Driven Optimization

## Definition

Metric-driven optimization is the practice of improving a system by defining a single measurable objective and systematically testing changes to optimize that metric. In [[concepts/auto-research]], this principle is fundamental: optimization proceeds entirely based on objective measurements, with no subjective human judgment in the loop.

## How It Works

**Core principle:**
"What gets measured gets improved" - but only if:
1. The metric is a single number (scalar)
2. The metric has clear direction (higher/lower is better)
3. The metric can be evaluated automatically
4. The metric actually captures what you care about

**In AutoResearch:**
- prepare.py defines the metric (immutable)
- Agent proposes changes to optimize that metric
- System evaluates each change objectively
- Only improvements by the metric get kept
- Human never involved in judging "better"

**Key insight from Karpathy:**
> "Any metric you care about that is reasonably efficient to evaluate can be auto researched"

The bottleneck is not execution (AI does that), but choosing what to measure.

## Key Parameters

**Metric characteristics:**
- **Scalar**: Single number, not vector or distribution
- **Directional**: Clear which direction is improvement
- **Automated**: No human evaluation needed
- **Fast**: Can evaluate in minutes or seconds, not hours
- **Aligned**: Actually measures what you care about

**Examples of good metrics:**
- Model loss (lower is better)
- Accuracy percentage (higher is better)
- Load time in milliseconds (lower is better)
- Conversion rate (higher is better)
- Sharpe ratio for trading (higher is better)
- API latency p99 (lower is better)

**Examples of bad metrics:**
- "User satisfaction" (subjective, requires human judgment)
- "Visual appeal" (no objective measurement)
- "Code quality" (too multifaceted, no single number)
- "Brand fit" (subjective, cultural judgment)

## When To Use

**Ideal domains:**
- **Performance optimization**: Speed, memory, throughput
- **Machine learning**: Loss, accuracy, F1 score
- **Trading**: Returns, Sharpe ratio, drawdown
- **Marketing**: Click-through rate, conversion rate, revenue
- **Web development**: Load time, bundle size, Core Web Vitals
- **Prompt engineering**: Success rate on test set

**Requirements:**
- You can define what "better" means objectively
- You can measure it automatically
- The measurement is fast enough to run repeatedly
- The metric aligns with your actual goal

**Warning:**
> "If you give it a bad metric, it will very confidently optimize the wrong thing"

Goodhart's Law applies: when a measure becomes a target, it ceases to be a good measure.

## Risks & Pitfalls

**Metric misalignment:**
- Optimize for clicks → clickbait headlines
- Optimize for speed → broken functionality
- Optimize for conversion → dark patterns
- Optimize for brevity → unclear communication

**Goodhart's Law:**
Once you optimize for a metric, the system finds ways to game it that don't improve the underlying goal.

**Examples:**
- Test accuracy ↑ but generalization ↓ (overfitting)
- Load time ↓ but user experience ↓ (removed features)
- Trading returns ↑ but risk ↑ (overleveraged)

**Single-metric blindness:**
Real goals are multi-dimensional, single metric is proxy. Agent will sacrifice unmeasured dimensions to optimize measured one.

**Solution strategies:**
- Choose metrics carefully (hardest part)
- Include constraints in program.md (e.g., "maintain visual appearance")
- Periodically review if metric still aligns with goal
- Use composite metrics when necessary (but still scalar)

## Related Concepts

- [[concepts/auto-research]] — Framework built on this principle
- [[concepts/experiment-loop]] — Process guided by metric
- [[concepts/three-file-architecture]] — prepare.py defines the metric
- [[concepts/autonomous-agents]] — Need objective metrics for autonomy

## Related Entities

- [[entities/andrej-karpathy]] — Emphasizes metric importance in AutoResearch

## Sources

- [[summaries/autoresearch-tutorial]] — Extensive discussion of metric selection

## The Skill of the Future

**Traditional work:**
- Execution is the bottleneck
- Skilled workers do the work
- Results are slow, expensive

**With autonomous agents:**
- Execution becomes "basically free"
- AI agents do the work
- Results are fast, cheap

**New bottleneck:**
> "What will become valuable is knowing what to measure, picking the right metric, and setting the right constraints. This is the skill that is going to make millionaires in the future."

The critical skill shifts from execution to objective-setting:
- Define what success means
- Choose measurable proxies
- Set appropriate constraints
- Recognize when metrics diverge from goals

## Case Study: Website Optimization

**Good metric:** Median load time (ms)
- Scalar: Single number
- Directional: Lower is better
- Automated: Puppeteer measures automatically
- Fast: Evaluation takes seconds
- Aligned: Users want fast sites

**Result:** 50ms → 25ms in 4 minutes (50% improvement)

Agent tried:
- ✅ Remove unused CSS (improvement)
- ❌ Add image compression (worse)
- ✅ Inline critical CSS (improvement)
- ✅ Further optimizations...

Each experiment judged purely on median load time. No human evaluation of "how it looks" or "whether users will like it." Pure metric optimization.

## Three Conditions for Success

From the tutorial, AutoResearch requires:
1. **Clear metric** ← This concept
2. **Automated evaluation** ← Enables autonomous loop
3. **One modifiable file** ← Constrains the search space

The metric is the first requirement because without it, nothing else matters. The entire system is driven by the metric.
