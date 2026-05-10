---
title: "Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of."
source: "https://techcommunity.microsoft.com/blog/azurearchitectureblog/securing-a-multi-agent-ai-solution-focused-on-user-context--the-complexities-of-/4493308"
author:
  - "[[Charles_Chukwudozie]]"
published: 2026-02-12
created: 2026-05-07
description: "How we built an enterprise-grade multi-agent system that preserves user identity across AI agents and DatabricksIntroductionWhen building AI-powered..."
tags:
  - "clippings"
---
## This is the first of two posts. This one focuses on the technical aspects; the next will address the CXOs perspective. Providing a comprehensive unified point of view.

*How we built an enterprise-grade multi-agent system that preserves user identity across AI agents and Databricks*

## Introduction

When building AI-powered applications for the enterprise, a common challenge emerges: how do you maintain user identity and access controls when an AI agent queries backend services on behalf of a user?

In many implementations, AI agents authenticate to backend systems using a shared service account or with PAT (Personal Access Token) tokens, effectively bypassing row-level security (RLS), column masking, and other data governance policies that organizations carefully configure. This creates a security gap where users can potentially access data they shouldn’t see, simply by asking an AI agent.

In this post, I’ll walk through how we solved this challenge for a current enterprise customer by implementing [Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/what-is-entra) [On-Behalf-Of](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-on-behalf-of-flow) (OBO) secure flow in a custom multi-agent LangGraph solution, enabling our [Databricks Genie](https://learn.microsoft.com/en-us/azure/databricks/genie/) agent to query data and the data agent designed to modify or update delta tables, to do so as the authenticated user, while preserving all RBAC policies.

## The Architecture

Our system is built on several key components:

**[Chainlit](https://docs.chainlit.io/authentication/oauth)**: Python-based web interface for LLM-driven conversational applications, integrated with OAuth 2.0–based authentication. Customizing the framework to satisfy customer UI requirements eliminated the need to develop and maintain a bespoke React front end. It fulfilled the majority of requirements while reducing maintenance overhead.

**Azure App Service** - Managed hosting with built-in authentication support and autoscaling

[**LangGraph**](https://docs.langchain.com/oss/python/langgraph/overview): Opensource Multi-agent orchestration framework.  
**Azure Databricks Genie**: Natural language to SQL agent.  
[**Azure Cosmos DB**](https://learn.microsoft.com/en-us/azure/cosmos-db/overview): Long-term memory and checkpoint storage.  
**Microsoft Entra ID**: Identity provider with OBO support.

This shows:

Genie: Read-only natural language queries, per-user OBO  
Task Agent: Handles sensitive operations (SQL modifications, etc.) with HITL approval + OBO  
Memory: Shared agent, no per-user auth needed

## The Problem with Chainlit OAuth Provider

Chainlit was integrated with Microsoft Entra ID for OAuth authentication; however, the default implementation assumes Microsoft Graph scopes, requiring extension to support custom resource scopes. This means:

The access token you receive is scoped for Microsoft [Graph API](https://learn.microsoft.com/en-us/graph/overview)  
You can’t use it for OBO flow to downstream services like Databricks  
The token’s audience is graph.microsoft.com, not your application  
For OBO to work, you need an access token where:

The audience is your application’s client ID  
The scope includes your custom API permission (e.g., api://{client\_id}/access\_as\_user)

## Solution: Custom Entra ID OBO Provider

We created a custom OAuth provider that replaces Chainlit’s built-in one.

Key insight: By requesting api://{client\_id}/access\_as\_user as the scope, the returned access token has the correct audience for OBO exchange.

Since we can’t call [Graph API](https://learn.microsoft.com/en-us/graph/overview) with this token (wrong audience), we extract user information from the ID token claims instead.

## The OBO Token Exchange

Once we have the user’s access token (with correct audience), we exchange it for a Databricks-scoped token using [MSAL](https://learn.microsoft.com/en-us/entra/msal/python/).

The resulting token:

Has audience = Databricks resource ID  
Contains the user’s identity (UPN, OID)  
Can be used with Databricks SDK/API  
Respects all Unity Catalog permissions configured for that user

## Per-User Agent Creation

A critical design decision: never cache user-specific agents globally. Each user needs their own Genie agent instance.

## Using the OBO Token with Databricks Genie

The key integration point is passing the OBO-acquired token to the Databricks SDK’s WorkspaceClient as indicated in the above screenshot, which the Genie agent uses internally for all API calls as shown in the following image.

Initialize Genie Agent with User’s Access Token:

Wire It Into LangGraph:

The user\_access\_token flows from Chainlit’s OAuth callback → session config → LangGraph config → agent creation, ensuring every Genie query runs with the authenticated user’s permissions.

## Human-in-the-Loop for Destructive SQL Operations

While Databricks Genie handles natural language queries (read-only), our system also supports custom SQL execution for data modifications. Since these operations can DELETE or UPDATE data, we implement human-in-the-loop approval using LangGraph’s interrupt feature.

The OBO token ensures that even when executing user-authored SQL, the query runs with the user’s permissions: they can only modify data they’re authorized to change.

The destructive operation detector uses LLM-based intent analysis

## Entra ID App Registration Requirements

Your Entra ID [app registration](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app) needs:

1. API Permissions: Azure Databricks → user\_impersonation (admin consent required)
2. Expose an API: Scope access\_as\_user on URI api://{client-id}
3. Redirect URI: {your-app-url}/auth/oauth/azure-ad/callback

## Lessons Learned

1. **Token audience matters**: OBO fails if your initial token has the wrong audience
2. **Don’t cache user-specific clients**: breaks user isolation
3. **ID tokens contain user info**: use claims when you can’t call [Graph API](https://learn.microsoft.com/en-us/graph/overview)
4. **HITL for destructive ops**: even with RBAC, require explicit user confirmation

## Conclusion

By implementing Entra ID OBO flow in our multi-agent system, we achieved:

1. User identity preservation across AI agents
2. [RBAC](https://learn.microsoft.com/en-us/azure/role-based-access-control/overview) enforcement at the [Databricks/Unity Catalog](https://learn.microsoft.com/en-us/azure/databricks/data-governance/unity-catalog/) level
3. Audit trail showing actual user making queries
4. Zero-trust architecture: the AI agent never has more access than the user
5. Human-in-the-loop for destructive SQL operations

This approach enables any organization building AI systems that supports OAuth 2.0 to participate in an on‑behalf‑of (OBO) flow. More importantly, it establishes a critical layer of AI governance for enterprise‑grade, custom multi‑agent solutions, aligning with Microsoft’s Secure Future Initiative (SFI) and Zero Trust principles.

As organizations accelerate toward multi‑agent AI architectures and broader AI transformation, centralized services that standardize identity, authorization, and user delegation become foundational. Capabilities such as Microsoft Entra Agent ID and Azure AI Foundry are emerging precisely to address this need - enabling secure, scalable, and user‑context–aware agent interactions.

In the next post, I’ll shift the lens from architecture to outcomes - examining what this foundation means from a CXO perspective, and why identity‑first AI governance is quickly becoming a board‑level concern.

Version 3.0