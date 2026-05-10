---
title: "User Identity Preservation"
type: concept
tags: [security, identity, authentication, multi-agent, rbac, foundational]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

User identity preservation is the practice of maintaining the authenticated user's identity context as requests flow through multi-tier systems, intermediaries, or AI agents, ensuring that all downstream services operate with the user's permissions rather than elevated service account privileges. In AI systems, this prevents agents from becoming "security backdoors" that bypass access controls.

## How It Works

**Identity propagation chain**:

1. **User authenticates** at entry point (web UI, API gateway) → receives identity token
2. **Token carries claims**: User principal name (UPN), object ID (OID), roles, groups, custom claims
3. **Intermediary services** (AI agents, middleware, orchestrators) receive user token
4. **Token exchange** (e.g., OBO flow): Intermediary exchanges user token for downstream-scoped token preserving user identity
5. **Downstream services** validate token, extract user identity, enforce per-user RBAC
6. **Audit trail** logs actions under user's identity, not service account

**Anti-pattern**: Service account authentication where intermediary uses its own credentials (PAT token, API key, service principal) to access downstream services — all users inherit service account permissions, bypassing security policies.

**Correct pattern**: Intermediary authenticates to downstream services using delegated user credentials (OBO, constrained delegation, impersonation) — each user retains their own permission scope.

## Key Parameters

- **Identity tokens**: JWT access tokens containing user claims (UPN, OID, roles, groups)
- **Token delegation mechanism**: OBO flow (OAuth), Kerberos constrained delegation, SAML token exchange
- **User claims**: Attributes carried in token (name, email, groups, custom attributes)
- **Token lifetime**: Session duration before re-authentication required
- **Per-user agent instances**: Each user must have dedicated agent with their token (no global caching)
- **Audit logging**: All operations must log actual user identity, not "system" or service account
- **RBAC enforcement points**: Where user permissions are validated (API gateway, database, file system)
- **Session management**: Tracking user context throughout request lifecycle

## When To Use

Use identity preservation when:

- **AI agents query sensitive data**: LLM agents accessing databases, APIs, or file systems with row-level security
- **Multi-tier applications**: Requests pass through multiple services before reaching data layer
- **Regulatory compliance**: HIPAA, GDPR, SOX, or other regulations requiring user-level audit trails
- **Zero-trust architecture**: No service should have blanket access; all access is user-scoped
- **Row-level security (RLS)**: Database enforces per-user visibility rules (e.g., users see only their department's data)
- **Column masking**: Sensitive columns (SSN, salary) visible only to authorized users
- **Enterprise AI systems**: LLM applications in organizations with existing RBAC policies
- **Data governance requirements**: Unity Catalog, Purview, or other data governance platforms track user access

Critical for any AI system where users could potentially ask agents to access data they shouldn't see directly.

## Risks & Pitfalls

**"AI backdoor" vulnerability**: Without identity preservation, users can bypass security by asking an AI agent to access restricted data — agent uses elevated service account, returns data user couldn't access directly

**Global agent caching**: Storing AI agents globally causes users to share the same agent instance and credentials, breaking isolation

**Token expiration**: User sessions expire; application must handle token refresh or re-authentication without breaking experience

**Audit trail gaps**: If service account credentials are used, audit logs show "service-bot" performed action, not actual user — compliance violation

**Performance overhead**: Per-user agent instances and token exchanges add memory usage and API call latency

**Debugging complexity**: Harder to reproduce issues when each user has different permissions; requires testing with multiple user contexts

**Implementation complexity**: Requires OAuth configuration, token management, session storage, and coordination across all tiers

**Legacy system integration**: Older services may not support token delegation, requiring proxy/gateway pattern

**Token claim bloat**: Large group memberships or custom claims can exceed token size limits

**Cross-service identity mapping**: User identity format may differ across systems (UPN vs email vs OID); requires claim transformation

## Related Concepts

- [[concepts/on-behalf-of-flow]] — Token delegation mechanism for preserving identity
- [[concepts/zero-trust-agents]] — Security model where agents never exceed user permissions
- [[concepts/rbac-enforcement]] — Permission checks using user identity
- [[concepts/agent-isolation]] — Per-user agent instances enforce security boundaries
- [[concepts/audit-trail]] — Logging actions with actual user identity
- [[concepts/token-audience]] — Ensuring tokens are scoped correctly for delegation
- [[concepts/session-management]] — Tracking user context throughout request lifecycle

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Enterprise multi-agent system preserving user identity through Chainlit + LangGraph + Databricks
