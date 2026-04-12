---
title: "Vault Management"
type: concept
tags: [obsidian, knowledge-management, workflow, organization]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: medium
---

# Vault Management

## Definition

Vault management refers to the practices and workflows for organizing, maintaining, and optimizing an Obsidian vault — the folder structure containing markdown notes, attachments, and configuration. In LLM wiki contexts, effective vault management ensures the knowledge base remains navigable and maintainable.

## How It Works

Key vault management activities include:
- **Directory structure** — organizing notes into folders (concepts, entities, summaries)
- **File naming** — consistent conventions (lowercase, hyphens, slugs)
- **Linking strategy** — when to use wiki links, tags, or folders
- **Plugin configuration** — selecting and configuring Obsidian plugins
- **Backup and sync** — version control, cloud sync, or both
- **Cleanup** — removing orphans, fixing broken links, deduplicating content

For LLM wikis, vault management is often automated through lint workflows and schema enforcement.

## Key Parameters

- **Vault size** — number of notes, total tokens/words
- **Directory depth** — flat vs hierarchical organization
- **Plugin count** — tradeoff between features and complexity
- **Update frequency** — how often content changes
- **Access patterns** — single user vs collaborative

## When To Use

Active vault management becomes important when:
- The vault grows beyond ~50-100 notes
- Multiple people contribute to the same vault
- You need to ensure consistent formatting and structure
- Link rot or orphaned pages accumulate
- Plugin conflicts or performance issues arise

## Risks & Pitfalls

- **Over-organization** — too many folders/tags can create friction
- **Plugin bloat** — too many plugins slow performance
- **Sync conflicts** — multiple editors without coordination
- **Rigid structure** — premature optimization before patterns emerge
- **Manual maintenance** — doesn't scale without automation

## Related Concepts

- [[concepts/second-brain]] — Higher-level concept that vault management supports
- [[concepts/lint-workflow]] — Automated vault maintenance
- [[concepts/wiki-maintenance]] — Ongoing wiki health practices
- [[entities/obsidian]] — The tool being managed

## Sources

- raw/Claude + Karpathy's Second Brain is INSANE.md — Tutorial on setting up and managing an LLM wiki vault
