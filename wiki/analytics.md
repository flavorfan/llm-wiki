---
title: "Analytics"
type: dashboard
tags: [meta]
updated: 2026-05-10
---

# Analytics

Visual analytics powered by the [Charts View](https://github.com/caronchen/obsidian-chartsview-plugin) Obsidian plugin.

## Page Distribution by Type

```chartsview
type: pie
options:
  legend:
    display: true
    position: right
data:
  - label: Concepts
    value: 58
  - label: Entities
    value: 35
  - label: Summaries
    value: 22
  - label: Syntheses
    value: 0
  - label: Index
    value: 1
```

## Confidence Distribution

```chartsview
type: bar
options:
  legend:
    display: false
  indexAxis: y
data:
  - label: High
    value: 114
    backgroundColor: "#4caf50"
  - label: Medium
    value: 5
    backgroundColor: "#ff9800"
  - label: Low
    value: 6
    backgroundColor: "#f44336"
```

## Top Tags by Frequency

```chartsview
type: wordcloud
options:
  maxRotation: 0
  minRotation: 0
data:
  - tag: knowledge-synthesis
    value: 15
  - tag: foundational
    value: 12
  - tag: automation
    value: 10
  - tag: claude-code
    value: 9
  - tag: ai-agents
    value: 8
  - tag: tools
    value: 8
  - tag: obsidian
    value: 7
  - tag: workflow
    value: 7
  - tag: llm-agents
    value: 6
  - tag: advanced
    value: 5
```
