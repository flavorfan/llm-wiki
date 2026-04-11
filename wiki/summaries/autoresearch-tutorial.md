---
title: "The Only AutoResearch Tutorial You'll Ever Need"
type: summary
tags: [auto-research, autonomous-agents, llm-agents, recursive-self-improvement, experimentation]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# The Only AutoResearch Tutorial You'll Ever Need

Video tutorial by David Andre explaining Andrej Karpathy's AutoResearch project - an open-source framework for autonomous AI self-improvement through systematic experimentation.

## Source Metadata

- **Type**: YouTube video transcript
- **Presenter**: David Andre
- **Date**: 2024
- **URL**: https://www.youtube.com/watch?v=uBWuKh1nZ2Y
- **Focus**: Tutorial on understanding and implementing AutoResearch loops

## Key Points

- **Core concept**: AutoResearch enables AI agents to run experiments autonomously, keeping what works and discarding what doesn't
- **Three-file architecture**: Essential structure includes:
  - `program.md` - human-defined goals, constraints, and rules (immutable by agent)
  - `train.py` - the one file the agent can modify (code, config, prompt, equation)
  - `prepare.py` - evaluation metric and scoring script (immutable by agent)
- **Experiment loop**: hypothesis → modify code → train (fixed time budget) → evaluate → commit if improved or git reset if worse
- **Origin story**: Karpathy was manually optimizing GPT-2 training for months, then realized an AI agent could automate this
- **Key constraint**: Fixed time budget (e.g., 5 minutes per experiment) ensures fair comparison - prevents agent from "cheating" by just training longer
- **Typical overnight run**: ~100 experiments while sleeping
- **Critical requirements for success**:
  1. Clear scalar metric (one number, clear direction)
  2. Automated evaluation (no human in the loop)
  3. One file the agent can modify
- **Git-based rollback**: Successful experiments get committed to git history; failures trigger `git reset`
- **Agent cannot modify prepare.py**: Prevents cheating by rewriting the scoring function

## Relevant Concepts

- [[concepts/auto-research]] - the main framework
- [[concepts/recursive-self-improvement]] - broader AI capability this enables
- [[concepts/autonomous-agents]] - agents that operate without human intervention
- [[concepts/three-file-architecture]] - program.md, train.py, prepare.py structure
- [[concepts/experiment-loop]] - the core iteration pattern
- [[concepts/metric-driven-optimization]] - optimization guided by measurable outcomes
- [[concepts/git-based-rollback]] - using version control for experiment management
- [[concepts/fixed-time-budget]] - ensuring fair experiment comparison

## Use Cases Demonstrated

### Proven Applications
- **Machine learning**: Model training optimization (original use case)
- **Trading**: Strategy optimization using Sharpe ratio on historical data
- **Marketing**: A/B testing of emails, ad creatives, landing pages, headlines, thumbnails
- **Code performance**: "Make it faster" optimization loops
- **Model compression**: Fine-tuning open-source models to run locally
- **Prompt engineering**: Optimizing system prompts for AI agents (different languages, complexity levels)
- **Website optimization**: Load time optimization (demonstrated in tutorial with 50% improvement in 4 minutes)

### Where AutoResearch Fails
- **Subjective metrics**: Brand design, UX, pricing decisions where "better" is a judgment call
- **Slow feedback loops**: Scenarios requiring human evaluation or long cycle times
- **Unclear metrics**: When success criteria cannot be reduced to an objective number

## Key Insights

1. **Not just for ML**: Biggest misconception is thinking AutoResearch only applies to machine learning - works anywhere with clear metrics
2. **Execution becomes free**: With AI agents, the bottleneck shifts from execution to knowing what to measure
3. **Future skill**: "Picking the right metric and setting the right constraints" becomes the valuable skill
4. **Bad metric = wrong optimization**: Agent will confidently optimize in the wrong direction if given wrong metric
5. **Scale prediction**: Video predicts marketing teams going from 30 experiments/year to 36,000 (100/day)
6. **Mobile AI prediction**: Predicts Sonnet 4.6 quality models running on iPhones in 3-4 months (as of video date)
7. **Industry adoption**: Karpathy predicts all LLM frontier labs will use some form of AutoResearch
8. **End vision**: SETI@home model but for AI research - distributed across millions of computers

## Technical Details

- Uses Puppeteer for web performance benchmarking
- Median load time as metric for website optimization
- Results logged in `results.tsv`
- Agent uses bypass permissions mode to run continuously
- Tutorial demonstrates 50% speed improvement (50ms → 25ms) in 4 minutes

## Notable Quotes

- "Give AI one file, one metric, and let it run hundreds, if not thousands, of experiments by itself while you sleep and watch it improve"
- "Any metric you care about that is reasonably efficient to evaluate can be auto researched" - Andrej Karpathy
- "Most marketing teams run 30 experiments per year. The next generation will run 36,000" - Eric Seu
- "We might be in the early stages of the singularity" - Andrej Karpathy

## Related Entities

- [[entities/andrej-karpathy]] - creator of AutoResearch
- [[entities/david-andre]] - tutorial creator
- [[entities/claude-code]] - tool used in tutorial demonstration
- [[entities/cursor]] - alternative IDE mentioned
- [[entities/puppeteer]] - web automation tool for benchmarking
- [[entities/eric-seu]] - quoted on marketing applications
- [[entities/harrison-chase]] - LangChain founder, mentioned for prompt engineering use case
