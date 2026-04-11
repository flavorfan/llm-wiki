---
title: "Puppeteer"
type: entity
tags: [tools, web-automation, testing, benchmarking]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Puppeteer

## Overview

Puppeteer is a web automation and testing tool used for programmatic browser control. In the context of [[concepts/auto-research]], it's used to benchmark website performance by measuring load times automatically.

## Characteristics

**Core capabilities:**
- Headless browser automation (can run Chrome in background)
- Web page load time measurement
- Automated testing and benchmarking
- JavaScript execution in browser context

**Use in AutoResearch:**
- Creates `benchmark.mjs` evaluation scripts
- Measures median load time as optimization metric
- Runs on localhost for local performance testing
- Provides objective, automated evaluation without human in the loop

**Technical features:**
- Can run faster than human can perceive (closes Chrome before visible)
- Produces structured output (e.g., results.tsv files)
- Integrates with Node.js ecosystem (.mjs files)

## Common Strategies

**Website optimization loops:**
- Serves as the prepare.py equivalent for web performance
- Measures performance metrics automatically
- Enables [[concepts/experiment-loop]] for front-end optimization
- Provides repeatable, objective measurements

**Evaluation pattern:**
1. Start local server (e.g., localhost:3000)
2. Launch Puppeteer to load page
3. Measure load time
4. Record metric for comparison
5. Agent modifies code based on result

## Related Entities

- [[entities/claude-code]] — Uses Puppeteer in AutoResearch demonstrations
- [[entities/david-andre]] — Demonstrates Puppeteer in tutorial

## Related Concepts

- [[concepts/auto-research]] — Framework that uses Puppeteer for web benchmarking
- [[concepts/metric-driven-optimization]] — Puppeteer provides the metrics
- [[concepts/experiment-loop]] — Puppeteer runs in the evaluation phase

## Sources

- [[summaries/autoresearch-tutorial]] — Demonstration of Puppeteer in AutoResearch workflow
