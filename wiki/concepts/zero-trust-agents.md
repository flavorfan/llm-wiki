---
title: "Zero-Trust Agents"
type: concept
tags: [security, zero-trust, ai-agents, rbac, foundational, enterprise]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

Zero-trust agents is a security architecture principle where AI agents never possess more access permissions than the authenticated user who initiated their work. Rather than granting agents elevated service account credentials, agents inherit the user's exact permission scope through token delegation, ensuring the agent can only perform actions the user themselves could perform directly.

## How It Works

**Traditional (insecure) pattern**:
- AI agent authenticates with service account credentials (API key, PAT token, service principal)
- Service account has broad permissions (e.g., read all databases, write all tables)
- All users share same agent with same elevated access
- User asks agent to query restricted data → agent succeeds because it has service account permissions → user bypasses security

**Zero-trust pattern**:
- User authenticates, receives access token with their permissions
- Agent receives user's token (or exchanges it via OBO flow for downstream services)
- Agent makes API calls using user's token, not service account credentials
- Backend services apply RBAC to user's identity (row-level security, column masking, etc.)
- User asks agent to query restricted data → agent fails because user lacks permission → security preserved

**Key principle**: "The AI agent never has more access than the user" — audit logs show actual user performing actions, not "ai-service-bot".

## Key Parameters

- **Token delegation mechanism**: OBO flow, Kerberos delegation, SAML assertion
- **Per-user agent instances**: Each user gets their own agent instance with their token (no global caching)
- **Permission inheritance**: Agent permissions = user permissions (never elevated)
- **Audit trail**: All agent actions logged under user identity
- **RBAC enforcement points**: Where user permissions are validated (database, API gateway, file system)
- **Token refresh strategy**: How to handle token expiration during long-running agent tasks
- **Least privilege principle**: Even within user's permissions, agent should request minimal necessary scope
- **Fail-closed default**: Agent fails if it can't authenticate as user (doesn't fall back to service account)

## When To Use

Use zero-trust agent architecture when:

- **Enterprise AI systems**: Deploying LLM agents in organizations with existing RBAC and data governance
- **Regulated industries**: Healthcare (HIPAA), finance (SOX), government (FedRAMP) requiring user-level audit trails
- **Multi-tenant SaaS**: AI features where users share infrastructure but must see only their own data
- **Database agents**: LLM-to-SQL agents querying databases with row-level security or column masking
- **API orchestration**: Agents calling internal/external APIs that enforce user permissions
- **Document access**: AI agents searching/summarizing documents with access control lists
- **Sensitive data**: Any system handling PII, PHI, financial records, trade secrets
- **Compliance requirements**: SOC 2, ISO 27001, or other frameworks requiring least-privilege access

Critical for any AI system where users shouldn't have uniform access to all data the agent could theoretically reach.

## Risks & Pitfalls

**Complexity overhead**: Per-user tokens, OBO flows, and session management add significant implementation complexity vs. simple service account

**Performance impact**: Token exchanges and per-user agent instances increase latency and memory usage

**Token expiration**: Long-running agent tasks may outlive user token lifetime; need refresh strategy or task checkpointing

**Legacy system integration**: Older services without token delegation support require proxy/shim layer

**Developer friction**: Easier to prototype with service account ("works on my machine"); zero-trust requires production-grade auth from day one

**Debugging difficulty**: Reproducing bugs requires access to user's exact permission context; can't just use admin account

**User permission variability**: Agent behavior differs per user; harder to test all edge cases

**Overengineering for prototypes**: Zero-trust may be excessive for internal tools with uniform access; balance risk vs. complexity

**Agent autonomy limitations**: Some agent workflows need to continue after user disconnects; requires secure long-lived delegation

**Multi-agent coordination**: When agents call other agents, need to propagate user context through entire chain (OBO flow stacking)

## Related Concepts

- [[concepts/on-behalf-of-flow]] — Core token delegation mechanism enabling zero-trust agents
- [[concepts/user-identity-preservation]] — Maintaining user context through agent calls
- [[concepts/rbac-enforcement]] — Permission checks agents are subject to
- [[concepts/agent-isolation]] — Per-user agent instances enforce security boundaries
- [[concepts/human-in-the-loop]] — Additional safeguard on top of zero-trust permissions
- [[concepts/audit-trail]] — Logging agent actions under user identity
- [[concepts/least-privilege]] — Minimizing permissions even within user scope
- [[concepts/security-by-design]] — Building security into architecture, not bolting on later

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Zero-trust multi-agent system: "the AI agent never has more access than the user"
