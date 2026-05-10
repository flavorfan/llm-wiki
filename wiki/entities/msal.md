---
title: "Microsoft Authentication Library (MSAL)"
type: entity
tags: [authentication, microsoft, oauth, library, python, security]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Microsoft Authentication Library (MSAL) is Microsoft's official SDK for acquiring OAuth 2.0 access tokens from Microsoft Entra ID. It provides language-specific implementations (Python, JavaScript, .NET, Java, etc.) with built-in support for On-Behalf-Of (OBO) flow, token caching, and refresh token handling, simplifying secure authentication for enterprise applications.

**Key capabilities**:
- OAuth 2.0 authorization code flow
- Client credentials flow (service-to-service)
- On-Behalf-Of (OBO) token exchange
- Automatic token caching
- Refresh token handling
- Device code flow
- Silent token acquisition
- Multi-cloud support (Azure public, government, China)

**Documentation**: https://learn.microsoft.com/en-us/entra/msal/python/

## Characteristics

- **Language-specific SDKs**: Python (MSAL Python), JavaScript (MSAL.js), .NET (MSAL.NET), Java (MSAL Java), etc.
- **Token caching**: Automatic in-memory or persistent cache, reduces token acquisition calls
- **OBO support**: Native `acquire_token_on_behalf_of()` method for service delegation
- **Refresh handling**: Automatically refreshes expired tokens using refresh tokens
- **Cloud-aware**: Supports Azure public cloud, government clouds, Azure China
- **Error handling**: Rich exception types for authentication failures
- **Confidential vs public clients**: Separate client types for server-side vs browser/mobile apps
- **PKCE support**: Proof Key for Code Exchange for public clients
- **Token validation**: Validates audience, issuer, expiration, and signature

**Python example (OBO flow)**:
```python
from msal import ConfidentialClientApplication

app = ConfidentialClientApplication(
    client_id="<app-id>",
    client_credential="<app-secret>",
    authority="https://login.microsoftonline.com/<tenant-id>"
)

# Exchange user token for Databricks-scoped token
result = app.acquire_token_on_behalf_of(
    user_assertion=user_access_token,
    scopes=["<databricks-resource-id>/.default"]
)

databricks_token = result["access_token"]
```

## Common Strategies

**Authentication flows**:
- [[concepts/on-behalf-of-flow]] — Using `acquire_token_on_behalf_of()` for delegation
- [[concepts/authorization-code-flow]] — Interactive user login with `acquire_token_by_authorization_code()`
- [[concepts/client-credentials-flow]] — Service authentication with `acquire_token_for_client()`
- [[concepts/device-code-flow]] — Browserless device login with `acquire_token_by_device_flow()`

**Token management**:
- [[concepts/token-caching]] — MSAL built-in cache strategies
- [[concepts/silent-token-acquisition]] — `acquire_token_silent()` for cache-first retrieval
- [[concepts/token-refresh]] — Automatic refresh token handling

**Integration patterns**:
- [[concepts/zero-trust-agents]] — MSAL for acquiring per-user agent tokens
- [[concepts/agent-isolation]] — Using MSAL in per-user agent initialization
- [[concepts/custom-oauth-provider]] — Wrapping MSAL for framework integration (e.g., Chainlit)

**Security best practices**:
- [[concepts/confidential-client-configuration]] — Secure secret/certificate storage
- [[concepts/token-validation]] — Verifying MSAL-acquired token claims
- [[concepts/least-privilege]] — Requesting minimal necessary scopes

## Related Entities

- [[entities/microsoft-entra-id]] — Identity provider MSAL authenticates against
- [[entities/chainlit]] — Framework requiring custom MSAL-based OAuth provider
- [[entities/databricks-genie]] — Agent receiving MSAL-acquired OBO tokens
- [[entities/azure-app-service]] — Hosting platform often using MSAL for authentication
- [[entities/langgraph]] — Agent framework integrating MSAL for user token acquisition

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — MSAL Python for OBO token exchange: exchanging user access token for Databricks-scoped token
