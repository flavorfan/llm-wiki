---
title: "Token Audience"
type: concept
tags: [oauth, jwt, security, authentication, configuration, foundational]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

Token audience is an OAuth 2.0 / JWT claim (`aud`) that specifies which service or API the access token is intended for. Each service validates that incoming tokens have the correct audience claim before accepting them, preventing tokens intended for one service from being reused with another. Audience mismatch is the most common cause of OBO flow failures.

## How It Works

**Token lifecycle**:

1. **Authorization request**: Client requests access token with specific scope (e.g., `api://{client_id}/access_as_user`)
2. **Token issuance**: Identity provider issues JWT with `aud` claim = the resource identifier requested in scope
3. **Token validation**: Target service validates JWT signature + expiration + **audience claim match**
4. **Audience enforcement**: If `aud` claim doesn't match service's expected value, token is rejected (401 Unauthorized)

**Example audience values**:
- Microsoft Graph API: `aud: "https://graph.microsoft.com"`
- Custom application: `aud: "api://12345678-1234-1234-1234-123456789abc"`
- Azure Databricks: `aud: "2ff814a6-3304-4ab8-85cb-cd0e6f879c1d"` (Azure Databricks resource ID)

**OBO flow dependency**:
- OBO exchange requires initial token with `aud` = calling application's client ID
- If you request default scopes (Microsoft Graph), you get `aud: "https://graph.microsoft.com"` → OBO fails
- Must explicitly request `api://{client_id}/access_as_user` scope to get correct audience

**Why Chainlit OAuth provider fails for OBO**:
- Chainlit default provider assumes Microsoft Graph usage
- Requests Graph scopes → token has `aud: "https://graph.microsoft.com"`
- This token can call Graph API but **cannot** be used for OBO exchange to Databricks
- Custom provider needed to request `api://{app_id}/access_as_user` scope

## Key Parameters

- **Audience claim (`aud`)**: JWT claim specifying intended recipient (resource ID or URL)
- **Scope parameter**: Authorization request scope determines audience (e.g., `api://{client_id}/access_as_user`)
- **Resource parameter**: Some OAuth flows use explicit `resource` parameter to set audience
- **Token validation**: Service validates audience matches its registered resource ID
- **Multi-audience tokens**: Some implementations support multiple audiences in array; not widely supported
- **Application ID URI**: Custom API surface exposes via `api://{client_id}` format in Entra ID
- **Resource ID vs audience**: Resource ID (GUID) vs audience URL may differ depending on service

## When To Use

Understand and configure token audience when:

- **Implementing OBO flow**: Audience must be set correctly for token exchange to succeed
- **Building multi-tier apps**: Each tier needs tokens with its own audience
- **Custom API integration**: Exposing APIs that validate audience claims
- **OAuth troubleshooting**: 401 errors often caused by audience mismatch
- **Service-to-service auth**: Each service validates tokens have its audience
- **Token reuse scenarios**: Preventing tokens from being misused with unintended services
- **Security reviews**: Verifying tokens are scoped to intended recipients only
- **Identity provider configuration**: Setting up app registrations with correct exposed APIs

Critical for any OAuth implementation beyond single-tier applications.

## Risks & Pitfalls

**Wrong scope requested**: Requesting default/Graph scopes yields token with wrong audience for downstream services — OBO fails

**Audience validation disabled**: Some services don't validate audience (insecure) — tokens can be reused across services

**Hardcoded assumptions**: Assuming audience always matches resource ID — not always true (e.g., Graph uses URL, not GUID)

**Multi-audience confusion**: Tokens with multiple audiences are non-standard; most services reject them

**Missing "Expose an API" configuration**: Forgetting to configure `api://{client_id}` scope in Entra ID app registration

**Admin consent required**: Custom scopes often need tenant admin consent before users can request them

**Token inspection gaps**: Not decoding JWT to verify `aud` claim during debugging — wastes time on wrong troubleshooting path

**Resource parameter deprecation**: Some OAuth flows used `resource` parameter to set audience; modern flows use scopes — check documentation

**Audience vs scope confusion**: Scope controls what the token can do; audience controls where it can be used — different concepts

**Token reuse security**: If audience validation is weak, attacker can steal token from one service and use it with another

## Related Concepts

- [[concepts/on-behalf-of-flow]] — OBO requires correct audience configuration to succeed
- [[concepts/oauth-token-exchange]] — Token exchange patterns depend on audience claims
- [[concepts/jwt-validation]] — Audience is one of several claims validated
- [[concepts/scope-vs-audience]] — Clarifying the distinction between scope and audience
- [[concepts/api-permissions]] — App registration configuration for exposing custom APIs
- [[concepts/token-introspection]] — Debugging token claims including audience

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Audience configuration for Chainlit + OBO flow: "The access token you receive is scoped for Microsoft Graph API... For OBO to work, you need an access token where the audience is your application's client ID"
