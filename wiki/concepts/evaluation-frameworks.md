---
title: "Evaluation Frameworks"
type: concept
tags: [evaluation, testing, metrics, quality-assurance, methodology, foundational]
created: 2026-05-26
updated: 2026-05-26
sources: ["raw/The prompting playbook_zh.md"]
confidence: high
---

## Definition

Evaluation frameworks are systematic approaches to testing language model outputs against defined criteria. They provide rigor to determine whether [[concepts/prompt-engineering]] changes actually improve performance or whether degradation is due to model capability vs. behavior differences.

## How It Works

**Test Case Design** — Three critical categories must be included:

1. **Control cases** — Should always pass
   - Basic, unambiguous questions the model handles well
   - Establish baseline competence
   - Example: "What's the data limit on our basic plan?" (when answer is in provided data)

2. **Edge cases** — Known failure modes
   - Situations where model previously failed
   - Test whether defensive instructions prevent regression
   - Example: "How much hotspot data do I have on my legacy plan?" (when answer requires reconciling current policy with legacy account data)

3. **Capability boundary cases** — Know when to refuse
   - Test model understands limits of its knowledge
   - Should escalate to humans or refuse appropriately
   - Example: "Detect and escalate billing errors instead of trying to self-diagnose"

**Evaluation Process**:

1. **Baseline** — Run test suite against current prompt version; document all failures
2. **Isolation** — For each failure pattern, make targeted prompt/tool changes
3. **Regression testing** — Re-run full suite to ensure fixes don't break passing cases
4. **Statistical rigor** — Account for natural variance in LLM outputs (run multiple trials)

**Measurement Approaches**:

- **Rule-based** (hard constraints) — Python functions that programmatically check if output violated business rules
- **LLM-based** — Use a separate evaluator prompt to grade each output
- **Hybrid** — Hard checks for binary criteria (e.g., JSON format valid?) + LLM for nuanced evaluation

## Key Parameters

- **Test set size** — Minimum 5-10 cases covering the three categories
- **Trial repetitions** — Run each test 3-5 times to account for LLM variance
- **Pass/fail criteria** — Clear definition of what constitutes success
- **Metric alignment** — Evaluation metrics should match actual business goals
- **Automation** — Framework should be reproducible and runnable without human judgment

## When To Use

- **Before prompt changes** — Establish baseline to measure against
- **During debugging** — Isolate which specific changes improve which failure modes
- **After model migrations** — Distinguish capability gaps from behavior shifts
- **Continuous validation** — Catch regressions in production systems
- **Agentic system design** — Validate multi-step workflows work correctly

## Risks & Pitfalls

- **Insufficient coverage** — Only testing happy paths misses edge cases
- **Metric misalignment** — Optimizing for wrong metrics (e.g., toxicity score when customers actually want helpfulness)
- **Variance masking** — Single run without repetitions can show false improvements
- **Maintenance burden** — Test suite gets stale; doesn't reflect real usage patterns
- **False negatives** — Evaluator prompt might miss subtle failures
- **Over-fitting to evals** — Optimizing prompts specifically for test cases rather than real-world performance

## Related Concepts

- [[concepts/prompt-engineering]] — Evaluation is essential before/after each prompt iteration
- [[concepts/metric-driven-optimization]] — Using evaluation results to drive improvements
- [[concepts/agentic-loops]] — Evaluators are often separate prompts in multi-step systems
- [[concepts/experiment-loop]] — Evaluation feedback loop
- [[concepts/skill-testing]] — Testing [[concepts/agent-skills]] reliability
- [[concepts/adaptive-thinking]] — Evaluating whether deeper reasoning helps

## Sources

- [[wiki/summaries/the-prompting-playbook-zh]] — Margot Vanlar's detailed walkthrough of evaluation frameworks for customer service bot debugging
