---
title: "Databricks Genie"
type: entity
tags: [databricks, natural-language, sql, agents, azure, ai-tools]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Databricks Genie is a natural language to SQL agent that translates user questions into SQL queries, executes them against Databricks data warehouses, and returns results. It respects Unity Catalog permissions when authenticated with user tokens, making it suitable for enterprise multi-agent systems where row-level security and column masking must be enforced.

**Key capabilities**:
- Natural language understanding of data questions
- SQL query generation from conversational input
- Execution against Databricks SQL warehouses
- Unity Catalog RBAC enforcement when using user tokens
- Integration with Databricks SDK WorkspaceClient
- Read-only operations (safe for autonomous agent use)

**Documentation**: https://learn.microsoft.com/en-us/azure/databricks/genie/

## Characteristics

- **Natural language interface**: Users ask questions in plain English (or other languages)
- **SQL generation**: LLM-powered query synthesis based on schema understanding
- **RBAC-aware**: When passed user's OBO token, respects Unity Catalog permissions
- **Read-only focus**: Designed for querying, not data modification (safe for autonomous use)
- **Schema understanding**: Learns table structures, relationships, and common query patterns
- **Result formatting**: Returns structured data suitable for agent consumption
- **Error handling**: Provides feedback when queries fail or questions are ambiguous
- **Integration**: Works via Databricks SDK WorkspaceClient with proper authentication

**Security model**:
- **With service account**: Bypasses RBAC, returns all data (security gap)
- **With user OBO token**: Enforces row-level security, column masking, table permissions per user
- **Per-user agent requirement**: Each user must have their own Genie instance with their token

## Common Strategies

**Authentication patterns**:
- [[concepts/on-behalf-of-flow]] — Passing user OBO tokens to Genie for RBAC enforcement
- [[concepts/zero-trust-agents]] — Genie agents inheriting user permissions
- [[concepts/agent-isolation]] — Per-user Genie instances, never cached globally

**Integration strategies**:
- [[concepts/multi-agent-orchestration]] — Genie as read-only agent in LangGraph workflows
- [[concepts/natural-language-sql]] — Patterns for NL-to-SQL agent use cases
- [[concepts/schema-retrieval]] — How Genie learns available tables and columns

**Security patterns**:
- [[concepts/user-identity-preservation]] — Maintaining user permissions through agent calls
- [[concepts/rbac-enforcement]] — Unity Catalog permission checks on queries
- [[concepts/row-level-security]] — Filtering results based on user attributes
- [[concepts/column-masking]] — Hiding sensitive columns from unauthorized users

**Complementary agents**:
- [[concepts/human-in-the-loop]] — Custom SQL agent for write operations requiring approval
- [[concepts/task-agent-pattern]] — Separating read (Genie) from write (custom agent) operations

## Related Entities

- [[entities/databricks]] — Data platform Genie operates on
- [[entities/unity-catalog]] — Data governance layer enforcing permissions
- [[entities/microsoft-entra-id]] — Identity provider for OBO tokens
- [[entities/databricks-sdk]] — WorkspaceClient used to initialize Genie agents
- [[entities/langgraph]] — Orchestration framework integrating Genie
- [[entities/msal]] — Token acquisition for Genie authentication

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Genie agent in multi-agent architecture, OBO token integration, per-user instantiation pattern
