---
title: "Skill Creator"
type: entity
tags: [tools, meta-skills, claude-code, automation, code-generation]
created: 2026-04-13
updated: 2026-04-13
sources: ["raw/claude-skills-2-how-to-use-skill-creator.md"]
confidence: high
---

# Skill Creator

## Overview

Skill Creator is a meta-skill for [[entities/claude-code]] that automates the creation of new Claude skills. It takes a skill description and generates a complete, tested, and refined skill markdown file. Often referred to as the foundation of "Skills 2.0" by the Claude community.

## Characteristics

- **Type**: Meta-skill (skill that creates other skills)
- **Installation**: Available via `manage plugins` command in Claude Code
- **Scope**: Can be installed per-project or globally ("for you")
- **Creation time**: Approximately 10 minutes for complex skills
- **Output format**: Complete markdown file with front matter and workflow instructions

## Key Features

### Self-Evaluation Loop

The distinguishing feature is its ability to evaluate and improve its own output:
1. Creates initial skill based on description
2. Generates test cases for the skill
3. Runs tests to measure performance
4. Refines the skill based on test results
5. Delivers final tested skill with improvements

### Automation

- Fully automated workflow requiring no manual intervention during creation
- Creates detailed to-do plans before execution
- Generates comprehensive test cases automatically
- Provides test result tables showing improvements made

### Quality Improvements

Example improvements demonstrated in testing:
- Added animations to landing page skills
- Added CSS variables for better maintainability
- Enhanced detailed specifications beyond initial requirements

## Common Strategies

- Install globally for consistent access across all projects
- Verify installation with `manage plugins` and direct query ("Do you have skill creator available?")
- Provide detailed descriptions including: layout, tech stack, structure, behavior, accessibility requirements
- Review test results table to understand what improvements were made

## Related Entities

- [[entities/claude-code]] — The platform it runs on
- [[entities/nick-babich]] — Created tutorial demonstrating its use
- [[concepts/meta-skills]] — The conceptual category it belongs to
- [[concepts/claude-skills]] — What it creates
- [[concepts/skill-testing]] — Its core evaluation mechanism
