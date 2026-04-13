---
title: "Meta Skills"
type: concept
tags: [claude-code, meta-programming, automation, self-improvement, advanced]
created: 2026-04-13
updated: 2026-04-13
sources: ["raw/claude-skills-2-how-to-use-skill-creator.md"]
confidence: high
---

# Meta Skills

## Definition

Meta skills are [[concepts/claude-skills]] that operate on other skills rather than performing direct tasks. They create, modify, evaluate, or manage other skills — a form of meta-programming applied to AI agent workflows.

## How It Works

### Core Mechanism

Instead of performing a domain task (like "create a landing page"), a meta-skill performs operations on the skill system itself:
- **Generate**: Create new skills from descriptions
- **Evaluate**: Test and measure skill performance
- **Improve**: Refine skills based on evaluation results
- **Manage**: Organize, categorize, or update existing skills

### Example: Skill Creator

[[entities/skill-creator]] is the primary meta-skill, demonstrating the full meta-skill loop:

```
User description 
  → Generate initial skill markdown
  → Create test cases
  → Run tests
  → Analyze results
  → Improve skill based on findings
  → Output refined skill
```

## Key Parameters

- **Scope of operation**: What aspects of skills it can modify
- **Automation level**: Fully automatic vs interactive improvement
- **Evaluation method**: How it measures skill quality
- **Improvement strategy**: How it decides what changes to make

## When To Use

- **Skill creation**: When you need new [[concepts/claude-skills]] but want higher quality than manual creation
- **Skill optimization**: When existing skills need systematic improvement
- **Scaling workflows**: When building many similar skills (e.g., different landing page styles)
- **Quality assurance**: When skill reliability is critical and needs automated testing

## Risks & Pitfalls

- **Complexity overhead**: Meta-skills take longer to run (10+ minutes)
- **Black box problem**: Generated skills may include patterns you don't understand
- **Over-optimization**: Skills optimized for test cases but not real-world edge cases
- **Dependency risk**: If Skill Creator breaks, many workflows may be disrupted
- **Loss of control**: Automated generation may produce different approaches than you'd prefer

## Related Concepts

- [[concepts/claude-skills]] — What meta-skills operate on
- [[concepts/skill-testing]] — Core evaluation mechanism used by meta-skills
- [[concepts/recursive-self-improvement]] — Broader AI concept of self-improving systems
- [[concepts/automation-workflows]] — General automation context
- [[entities/skill-creator]] — The primary meta-skill implementation

## Sources

- [[summaries/claude-skills-2-skill-creator]] — Demonstrates meta-skill in action
