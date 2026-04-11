---
title: "Andrej Karpathy"
type: entity
tags: [people, ai-research, openai, tesla, auto-research]
created: 2026-04-10
updated: 2026-04-11
sources: ["raw/Claude + Karpathy's Second Brain is INSANE.md", "raw/karpathy-x.md", "raw/llm-wiki.md", "raw/The only AutoResearch tutorial you'll ever need.md"]
confidence: high
---

# Andrej Karpathy

## Overview

Andrej Karpathy is a co-founder at [[entities/openai]] and one of the most legendary AI researchers of all time. He was the main person behind Tesla Autopilot and is widely recognized for his work in deep learning and for making AI concepts accessible. He invented the term "vibe coding" and originated both the [[concepts/llm-knowledge-base]] pattern and [[concepts/auto-research]] framework. Born in Czechoslovakia.

## Characteristics

**Professional background:**
- Co-founder at OpenAI
- Main person behind Tesla Autopilot
- Expert in deep learning
- Attended Stanford University
- Top influential figure in AI community
- Born in Czechoslovakia
- Major contributor to open-source AI community

**Communication style:**
- Tweets that "go super viral" when released
- Intentionally vague in idea files to allow flexible implementation
- Breaks down complex patterns step-by-step
- Shares practical workflows and tooling openly

**Innovation approach:**
- Shifted token throughput from manipulating code to manipulating knowledge (markdown and images)
- Builds and shares personal workflow innovations that become industry patterns
- Creates "idea files" rather than rigid specifications
- Invented the term "vibe coding"
- Predicts all LLM frontier labs will use some form of [[concepts/auto-research]]
- Believes we might be "in the early stages of the singularity"

## Common Strategies

**LLM Knowledge Base Pattern** ([[concepts/llm-knowledge-base]]):
- Originated the pattern of using LLMs to maintain personal wikis
- April 2nd, 2026 tweet on building LLM knowledge bases step-by-step
- Follow-up tweet on "idea file" concept - intentionally abstract framework
- Real-world wiki: ~100 articles, ~400K words on research topics

**AutoResearch Framework** ([[concepts/auto-research]]):
- Created open-source project for autonomous AI self-improvement
- Origin: Was manually optimizing GPT-2 training for months, realized an AI agent could automate this
- Defines [[concepts/three-file-architecture]]: program.md, train.py, prepare.py
- Core principle: "Any metric you care about that is reasonably efficient to evaluate can be auto researched"
- Vision: SETI@home model but for AI research - distributed across millions of computers
- Predicts this is "the final boss battle" for AI labs

**Workflow:**
- Uses [[entities/obsidian]] as IDE frontend
- [[concepts/ingest-workflow]] from raw/ directory
- [[concepts/query-workflow]] for complex questions
- [[concepts/lint-workflow]] for health checks
- Developing custom tools (naive search engines) as needed

**Philosophy:**
- "I rarely touch [the wiki] directly" - LLM maintains it
- Explorations should "add up" in knowledge base rather than disappear
- Focus on markdown and images as knowledge substrate
- Related to Vannevar Bush's Memex (1945) vision

## Related Entities

- [[entities/openai]] — Organization where he's a founding researcher
- [[entities/obsidian]] — Tool he uses as knowledge base IDE
- [[entities/claude-code]] — AI harness that implements his pattern
- [[entities/nick-b-zark]] — Created tutorial implementing his pattern

## Sources

- [[summaries/karpathy-x]] — His original tweet describing the workflow
- [[summaries/llm-wiki]] — The idea file pattern he created
- [[summaries/claude-karpathy-second-brain-video]] — Tutorial based on his tweets
- [[summaries/autoresearch-tutorial]] — Comprehensive tutorial on his AutoResearch framework
