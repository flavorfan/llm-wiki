---
title: "Charles Chukwudozie"
type: entity
tags: [people, microsoft, azure, ai-engineering, content-creator]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: medium
---

## Overview

Charles Chukwudozie is a technical author and engineer at Microsoft who writes about enterprise AI architectures, particularly multi-agent systems, security patterns, and Azure integrations. He published a technical blog post on securing multi-agent AI solutions with On-Behalf-Of flow, demonstrating implementation patterns for preserving user identity across LangGraph agents and Databricks.

## Characteristics

- **Affiliation**: Microsoft (Azure Architecture team, based on publication venue)
- **Expertise**: Multi-agent AI systems, enterprise security, OAuth/Entra ID, Azure Databricks integration
- **Content style**: Technical deep-dives with architecture diagrams, code snippets, and implementation details
- **Audience**: Enterprise architects, AI engineers building production systems
- **Publication venues**: Microsoft Tech Community (Azure Architecture Blog)
- **Writing approach**: Two-part series format (technical implementation + CXO perspective)

**Notable work**:
- "Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of" (Feb 2026)
  - Technical implementation of OBO flow in Chainlit + LangGraph + Databricks
  - Custom OAuth provider for token audience configuration
  - Per-user agent isolation patterns
  - Human-in-the-loop for destructive operations

## Common Strategies

**Topics covered**:
- [[concepts/on-behalf-of-flow]] — Token delegation for multi-tier AI systems
- [[concepts/zero-trust-agents]] — AI agents inheriting user permissions
- [[concepts/user-identity-preservation]] — Maintaining identity across agent boundaries
- [[concepts/human-in-the-loop]] — Approval workflows for high-risk agent actions

**Technologies documented**:
- [[entities/microsoft-entra-id]] — Identity provider configuration
- [[entities/chainlit]] — Custom OAuth provider implementation
- [[entities/langgraph]] — Multi-agent orchestration
- [[entities/databricks-genie]] — Natural language SQL with RBAC

## Related Entities

- [[entities/microsoft-entra-id]] — Core technology in Charles's security patterns
- [[entities/chainlit]] — Framework requiring custom OAuth implementation
- [[entities/langgraph]] — Orchestration framework in documented architecture
- [[entities/microsoft-secure-future-initiative]] — Security framework alignment

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Author of technical blog post on enterprise multi-agent security
