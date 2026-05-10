---
title: "On-Behalf-Of (OBO) Flow"
type: concept
tags: [oauth, authentication, security, token-delegation, microsoft-entra, foundational]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

On-Behalf-Of (OBO) flow is an OAuth 2.0 token exchange pattern where a service exchanges an access token it received from a user for a new access token scoped to a different downstream service, while preserving the user's identity. This enables secure delegation chains where each service in the chain acts on behalf of the authenticated user, not with its own elevated permissions.

## How It Works

1. **Initial authentication**: User authenticates to frontend application, receives access token with audience = frontend app client ID
2. **Token audience requirement**: Frontend must request scope `api://{client_id}/access_as_user` so the token has correct audience for OBO exchange (not Graph API)
3. **OBO exchange**: Frontend/middleware calls Microsoft Entra ID token endpoint with user's access token, requests new token for downstream service (e.g., Databricks)
4. **Downstream token**: New token has audience = downstream service resource ID, contains user's identity claims (UPN, OID)
5. **Service call**: Downstream service receives token, validates it, applies user-specific RBAC policies
6. **Audit trail**: All actions appear in logs under user's identity, not service account

Token flow: `User → Frontend App Token → [OBO Exchange] → Databricks Token → API Call`

Key insight: The access token audience matters. If initial token has audience `graph.microsoft.com`, OBO exchange will fail. Must request custom scope `api://{client_id}/access_as_user` to get correct audience.

## Key Parameters

- **Initial token audience**: Must be the frontend application's client ID, not Graph API
- **Requested scope**: `api://{client_id}/access_as_user` for initial authentication
- **Downstream resource ID**: Target service resource identifier (e.g., Azure Databricks resource ID)
- **Token claims**: User principal name (UPN), object ID (OID), any custom claims for authorization
- **ID token vs access token**: OBO exchanges access token; ID token contains user info when Graph API not available
- **Token lifetime**: OBO tokens inherit user session lifetime, require refresh when expired
- **Admin consent**: Downstream API permissions require tenant admin consent in Entra ID

## When To Use

Use OBO flow when:

- **Multi-tier application architecture**: Frontend → middleware → backend services, each tier needs user context
- **AI agent systems**: Agents query databases/APIs on user's behalf, must respect user permissions
- **Zero-trust security**: Never want services to have more access than the user who initiated the request
- **Audit requirements**: All actions must be traceable to actual user, not service account
- **RBAC enforcement**: Backend services have row-level security, column masking, or per-user access policies
- **Regulatory compliance**: Data access must be auditable and scoped to authenticated user permissions
- **Service delegation chains**: Each service needs to call another service while preserving user identity

Particularly critical for AI/LLM applications where agents might access sensitive data — prevents "AI backdoor" where users can bypass security by asking an agent.

## Risks & Pitfalls

**Token audience misconfiguration**: Most common failure — requesting Graph API scope by default yields token that can't be exchanged for downstream services

**Global agent caching**: Storing user-specific agents or tokens in global cache breaks user isolation; each user must have their own agent instance

**Missing admin consent**: OBO requires tenant admin to consent to API permissions (e.g., Databricks `user_impersonation` scope)

**Token expiration handling**: OBO tokens expire; applications must refresh tokens or handle re-authentication gracefully

**ID token confusion**: Can't call Graph API with custom-scoped access token (wrong audience), must extract user info from ID token claims instead

**Scope creep**: Each downstream service needs explicit API permission configuration; missing permissions cause runtime failures

**Debugging complexity**: Token exchange failures are opaque; validate audience/scope claims in token before attempting OBO

**Performance overhead**: Token exchange adds latency (additional API call per request); consider caching OBO tokens per user session

**Chained OBO limitations**: Some services don't support OBO, breaking delegation chains; verify all services in chain support OBO

**User-specific state**: Must track tokens per user session; session storage or secure cache required

## Related Concepts

- [[concepts/zero-trust-agents]] — Security model where agents inherit user permissions
- [[concepts/user-identity-preservation]] — Maintaining user context across system boundaries
- [[concepts/token-audience]] — OAuth audience claim configuration
- [[concepts/rbac-enforcement]] — Role-based access control in multi-tier systems
- [[concepts/human-in-the-loop]] — Complementary safeguard for high-risk operations
- [[concepts/agent-isolation]] — Per-user agent instantiation enforces security boundaries
- [[concepts/oauth-token-exchange]] — General token exchange patterns beyond OBO

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Enterprise multi-agent system implementation with Chainlit, LangGraph, Databricks Genie
