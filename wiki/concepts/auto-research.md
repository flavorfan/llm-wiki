---
title: "AutoResearch"
type: concept
tags: [llm-agents, autonomous-agents, recursive-self-improvement, experimentation, foundational]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# AutoResearch

## Definition

AutoResearch is an open-source framework created by [[entities/andrej-karpathy]] that enables AI agents to autonomously run experiments, evaluate results, and keep what works while discarding what doesn't. The system operates on a simple loop: give the AI one file to modify, one metric to optimize, and let it run hundreds or thousands of experiments while you sleep.

## How It Works

**Core mechanism:**
1. Agent generates hypothesis about what could improve the metric
2. Agent modifies the designated file (code, config, prompt, equation)
3. System runs experiment for fixed time budget (e.g., 5 minutes)
4. System evaluates result using predefined metric
5. If improved: commit to git history
6. If worse: `git reset --hard` and try something else
7. Repeat loop indefinitely

**Three-file architecture** ([[concepts/three-file-architecture]]):
- `program.md` — Human defines goals, constraints, rules (agent cannot modify)
- `train.py` — The one file the agent can modify
- `prepare.py` — Evaluation metric script (agent cannot modify)

**Origin story:**
Karpathy was manually optimizing GPT-2 training for months. He realized: "Why am I doing this? Why don't I just have an AI agent run different experiments in a loop to figure out what's the best way to optimize this model?"

## Key Parameters

**Critical requirements (all three must be present):**
1. **Clear scalar metric** — One number with clear direction of improvement
2. **Automated evaluation** — No human in the loop
3. **One modifiable file** — Not zero, not two, exactly one

**Fixed time budget:**
- Makes every experiment directly comparable
- Prevents agent from "cheating" by just training longer
- Typical: 5 minutes per experiment, ~100 experiments overnight
- Ensures only the quality of the idea determines success

**Immutable constraints:**
- Agent cannot modify `prepare.py` (prevents cheating the eval)
- Agent cannot modify `program.md` (preserves human-set goals)
- Git provides rollback mechanism for failed experiments

## When To Use

**Ideal applications** (proven use cases):
- **Machine learning**: Model training optimization (original use case)
- **Trading**: Strategy optimization with Sharpe ratio on historical data
- **Marketing**: A/B testing emails, ads, landing pages, headlines, thumbnails at scale
- **Code performance**: "Make it faster" optimization loops
- **Model compression**: Fine-tuning models to run locally
- **Prompt engineering**: Optimizing system prompts (language, complexity level)
- **Website optimization**: Load time, performance metrics

**General rule** (Karpathy):
> "Any metric you care about that is reasonably efficient to evaluate can be auto researched"

**Three conditions for success:**
1. Clear objective metric (one number, measurable)
2. Fast feedback loop (automated evaluation)
3. One file to optimize

## Risks & Pitfalls

**Where AutoResearch fails:**
- **Subjective metrics**: Brand design, UX, pricing where "better" is a judgment call
- **Slow feedback loops**: Scenarios requiring human evaluation or long cycle times
- **Bad metrics**: Agent will confidently optimize the wrong thing if given wrong metric
- **Multiple files**: Agent needs exactly one file to modify, no more, no less

**Common mistakes:**
- Not fixing time budget → unfair experiment comparison
- Allowing agent to modify prepare.py → agent can cheat the eval
- Setting wrong metric → optimization in wrong direction
- No automated evaluation → can't run while sleeping, not "auto" research

**Critical insight:**
> "If you give it a bad metric, it will very confidently optimize the wrong thing"

The quality of your metric determines the value of the entire loop.

## Related Concepts

- [[concepts/three-file-architecture]] — The structural pattern AutoResearch uses
- [[concepts/experiment-loop]] — The core iteration mechanism
- [[concepts/metric-driven-optimization]] — Optimization guided by measurable outcomes
- [[concepts/git-based-rollback]] — Version control for experiment management
- [[concepts/fixed-time-budget]] — Fair comparison mechanism
- [[concepts/recursive-self-improvement]] — Broader AI capability this enables
- [[concepts/autonomous-agents]] — Agents operating without human intervention

## Related Entities

- [[entities/andrej-karpathy]] — Creator of AutoResearch
- [[entities/david-andre]] — Created comprehensive tutorial
- [[entities/claude-code]] — Tool used for implementing AutoResearch
- [[entities/cursor]] — Alternative IDE for AutoResearch
- [[entities/puppeteer]] — Used for web performance benchmarking

## Sources

- [[summaries/autoresearch-tutorial]] — Comprehensive explanation and tutorial

## Future Vision

**Karpathy's predictions:**
- All LLM frontier labs will use some form of AutoResearch
- "This is the final boss battle"
- "We might be in the early stages of the singularity"

**End vision:**
SETI@home model for AI research — millions of AI agents distributed across thousands of computers, with humans allocating where that research effort goes.

**Industry impact:**
- Execution of work becomes "basically free"
- Value shifts to: knowing what to measure, picking the right metric, setting the right constraints
- "This is the skill that is going to make millionaires in the future"

**Scale predictions:**
- Marketing: 30 experiments/year → 36,000/year (1,200x increase)
- Mobile AI: Sonnet 4.6 quality models on iPhones in 3-4 months
- Real autonomous loops doing meaningful work for companies/individuals
