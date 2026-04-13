---
title: "Claude Skills 2.0: How to use Skill Creator"
type: summary
tags: [claude-code, skills, meta-skills, automation, skill-creator, testing]
created: 2026-04-13
updated: 2026-04-13
sources: ["raw/claude-skills-2-how-to-use-skill-creator.md"]
confidence: high
---

# Claude Skills 2.0: How to use Skill Creator

## Key Points

- **Skills 2.0** refers to the improved process of creating Claude skills using the Skill Creator meta-skill
- **Claude skills** are markdown files with two parts: front matter (tells Claude when to use the skill) and markdown content (workflow/actions)
- **Skill Creator** is a meta-skill that takes a description and generates a complete, tested skill
- **Key innovation**: Skill Creator evaluates quality by running tests and improves the skill based on test results
- **Workflow**: Creates initial skill → measures performance → improves based on testing → delivers final tested skill
- Skills can be installed "for you" (all projects) or per-project via the "manage plugins" command
- Skill creation is fully automated; typical creation time is ~10 minutes for complex skills
- The meta-skill approach produces more detailed and effective skills compared to manual creation

## Process Demonstrated

The video shows a 4-step process:
1. **Install Skill Creator**: Use `manage plugins` command to find and install
2. **Prompt for new skill**: Describe the desired skill functionality
3. **Automated creation**: Skill Creator drafts, tests, and refines the skill
4. **Use the skill**: Invoke with specific commands (e.g., `/super-landing-page`)

Example: Creating a "super landing page" skill that generates Apple-style landing pages with animations, CSS variables, and detailed specifications.

## Relevant Concepts

- [[concepts/meta-skills]] — Skills that create or modify other skills
- [[concepts/claude-skills]] — The skill system in Claude Code
- [[concepts/skill-testing]] — Automated testing and evaluation of skills
- [[concepts/automation-workflows]] — Automated skill generation workflows
- [[entities/skill-creator]] — The meta-skill tool itself
- [[entities/nick-babich]] — Video creator and AI educator

## Source Metadata

- **Type**: Video transcript (YouTube)
- **Author**: Nick Babich
- **Published**: 2026-03-08
- **URL**: https://www.youtube.com/watch?v=rihf3-mpNG4
- **Topic**: Claude Code skills development methodology
- **Duration**: ~5 minutes
