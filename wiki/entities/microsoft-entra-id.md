---
title: "Microsoft Entra ID"
type: entity
tags: [identity, microsoft, azure, oauth, authentication, enterprise]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's cloud-based identity and access management service. It provides authentication, authorization, and directory services for enterprise applications, with support for OAuth 2.0, OpenID Connect, SAML, and the On-Behalf-Of (OBO) token exchange flow that enables secure service delegation while preserving user identity.

**Key capabilities**:
- User and group management
- OAuth 2.0 / OpenID Connect authentication
- On-Behalf-Of (OBO) flow for token delegation
- App registrations and API permissions
- Conditional access policies
- Multi-factor authentication (MFA)
- Single sign-on (SSO) across applications
- Integration with Azure services (Databricks, App Service, etc.)

**Formerly known as**: Azure Active Directory (Azure AD); rebranded to Microsoft Entra ID

## Characteristics

- **Cloud-native**: SaaS identity provider, no on-premises infrastructure required
- **Enterprise scale**: Supports millions of users, billions of authentications per day
- **OAuth 2.0 compliant**: Standards-based authentication and authorization
- **OBO support**: Native implementation of On-Behalf-Of token exchange for service delegation
- **App registration model**: Applications registered in tenant, exposing APIs and requesting permissions
- **Admin consent**: Sensitive permissions require tenant administrator approval
- **Token formats**: Issues JWT access tokens with claims for user identity and permissions
- **Integration ecosystem**: Native integration with Microsoft services (Azure, Office 365, Dynamics)
- **Security features**: Conditional access, identity protection, privileged identity management
- **Developer tools**: Microsoft Authentication Library (MSAL) SDKs for token acquisition

**OBO flow support**:
- Enables multi-tier applications to exchange tokens while preserving user identity
- Requires app registration with "Expose an API" configuration (`api://{client_id}`)
- Admin consent required for API permissions (e.g., Databricks `user_impersonation`)
- Tokens carry user claims (UPN, OID, roles, groups) through delegation chain

## Common Strategies

**Authentication flows**:
- [[concepts/on-behalf-of-flow]] — Token delegation for multi-tier applications
- [[concepts/oauth-authorization-code-flow]] — Interactive user login with consent
- [[concepts/client-credentials-flow]] — Service-to-service authentication without user
- [[concepts/device-code-flow]] — Authentication for devices without web browser

**Token management**:
- [[concepts/token-audience]] — Configuring audience claims for API security
- [[concepts/token-refresh]] — Handling token expiration and renewal
- [[concepts/token-caching]] — MSAL token cache strategies

**Security patterns**:
- [[concepts/conditional-access]] — Policy-based access controls (MFA, device compliance)
- [[concepts/zero-trust-agents]] — AI agents inheriting user permissions via OBO
- [[concepts/least-privilege]] — Minimizing API permission scope

**App configuration**:
- [[concepts/api-permissions]] — Configuring app registration permissions
- [[concepts/expose-an-api]] — Creating custom API scopes for OBO
- [[concepts/redirect-uri-configuration]] — OAuth callback endpoint registration

## Related Entities

- [[entities/msal]] — Microsoft Authentication Library for token acquisition
- [[entities/azure-app-service]] — Managed hosting with built-in Entra ID authentication
- [[entities/databricks]] — Data platform with Entra ID integration for user impersonation
- [[entities/azure-cosmos-db]] — Database with Entra ID RBAC support
- [[entities/microsoft-graph-api]] — API for Microsoft 365 services, default Entra ID audience
- [[entities/chainlit]] — Python framework requiring custom Entra ID provider for OBO
- [[entities/microsoft-secure-future-initiative]] — Security framework Entra ID aligns with

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Entra ID as identity provider for multi-agent system with OBO flow, app registration configuration
