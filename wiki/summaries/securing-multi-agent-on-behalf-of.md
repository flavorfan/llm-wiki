---
title: "Securing A Multi-Agent AI Solution with On-Behalf-Of Flow"
type: summary
tags: [security, multi-agent, authentication, azure, databricks, microsoft-entra, oauth, rbac]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Key Points

- **Problem**: AI agents typically authenticate to backend services using shared service accounts or PAT tokens, bypassing row-level security (RLS), column masking, and data governance policies
- **Solution**: Implement Microsoft Entra ID On-Behalf-Of (OBO) flow to preserve user identity and RBAC enforcement across multi-agent systems
- **Architecture**: Chainlit (UI) + LangGraph (orchestration) + Databricks Genie (NL-to-SQL) + Azure Cosmos DB (memory) + Microsoft Entra ID (identity)
- **Custom OAuth provider**: Replace Chainlit's default Graph-scoped OAuth with custom provider requesting `api://{client_id}/access_as_user` scope for correct token audience
- **Token exchange**: Exchange user access token for Databricks-scoped token via MSAL, preserving user identity (UPN, OID) for Unity Catalog permissions
- **Per-user agent isolation**: Never cache user-specific agents globally; each user gets their own Genie agent instance with their OBO token
- **Human-in-the-loop (HITL)**: Destructive SQL operations (DELETE, UPDATE) require explicit user approval via LangGraph interrupts, even with OBO RBAC enforcement
- **Zero-trust architecture**: AI agent never has more access than the authenticated user; all queries run with user's permissions and appear in audit trail
- **Case study results**: Enterprise customer deployment achieving user identity preservation, RBAC enforcement, audit trail, and HITL for destructive operations
- **Future direction**: Microsoft Entra Agent ID and Azure AI Foundry emerging to standardize identity, authorization, and user delegation for multi-agent systems

## Relevant Concepts

- [[concepts/on-behalf-of-flow]] — OAuth 2.0 OBO pattern for token delegation
- [[concepts/user-identity-preservation]] — Maintaining user context across agent boundaries
- [[concepts/human-in-the-loop]] — Approval workflows for high-risk agent actions
- [[concepts/zero-trust-agents]] — Security model where agents inherit user permissions
- [[concepts/token-audience]] — OAuth token audience/scope configuration
- [[concepts/multi-agent-orchestration]] — LangGraph coordination of specialized agents
- [[concepts/rbac-enforcement]] — Role-based access control in AI systems
- [[concepts/agent-isolation]] — Per-user agent instantiation patterns

## Entities Referenced

- [[entities/microsoft-entra-id]] — Identity provider with OBO support
- [[entities/chainlit]] — Python web UI for LLM applications with OAuth
- [[entities/langgraph]] — Multi-agent orchestration framework
- [[entities/databricks-genie]] — Natural language to SQL agent
- [[entities/azure-cosmos-db]] — Long-term memory and checkpoint storage
- [[entities/azure-app-service]] — Managed hosting with authentication
- [[entities/unity-catalog]] — Databricks data governance layer
- [[entities/msal]] — Microsoft Authentication Library for token exchange
- [[entities/charles-chukwudozie]] — Article author
- [[entities/microsoft-secure-future-initiative]] — Security framework alignment

## Source Metadata

- **Type**: Technical blog post (Microsoft Tech Community)
- **Author**: Charles Chukwudozie
- **Published**: 2026-02-12
- **URL**: https://techcommunity.microsoft.com/blog/azurearchitectureblog/securing-a-multi-agent-ai-solution-focused-on-user-context--the-complexities-of-/4493308
- **Context**: Enterprise customer implementation, first of two posts (technical focus; CXO perspective to follow)
- **Domain**: Enterprise AI security, multi-agent systems, identity management
- **Technologies**: Azure, Databricks, LangChain/LangGraph, Microsoft Entra ID, Python
- **Version**: 3.0
