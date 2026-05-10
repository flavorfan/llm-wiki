---
title: "Chainlit"
type: entity
tags: [python, llm-ui, web-framework, oauth, conversational-ai]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Chainlit is a Python-based web framework for building LLM-driven conversational applications with built-in UI components, session management, and OAuth 2.0 authentication support. It eliminates the need for custom React frontends by providing a pre-built interface optimized for chat-based AI applications, reducing development and maintenance overhead for conversational AI products.

**Key features**:
- Pre-built chat UI components (messages, inputs, file uploads)
- OAuth 2.0 authentication with provider plugins
- Session management for conversation state
- Streaming response support
- File attachment handling
- Markdown rendering
- Customizable styling and branding
- Python-native API (no JavaScript required)

**Website**: https://docs.chainlit.io/

## Characteristics

- **Python-first**: Entire application written in Python, no separate frontend codebase
- **OAuth integration**: Built-in authentication support (Google, GitHub, Azure AD, custom providers)
- **Conversational UX**: Optimized for chat-based interactions (messages, turns, streaming)
- **Rapid prototyping**: Faster time-to-market than building custom React frontend
- **LLM-agnostic**: Works with any LLM API (OpenAI, Anthropic, Hugging Face, etc.)
- **Session handling**: Automatic conversation history and state management
- **File support**: Upload/download files within conversations
- **Customizable**: CSS/styling overrides for branding requirements
- **Reduced maintenance**: Framework updates maintain UI without custom frontend work

**Default OAuth limitation**:
- Built-in OAuth provider assumes Microsoft Graph API usage
- Access tokens have `aud: "https://graph.microsoft.com"` audience
- Cannot be used for OBO flow to custom APIs (e.g., Databricks)
- Requires custom OAuth provider implementation for OBO scenarios

**Custom provider solution**:
- Replace default provider with custom implementation
- Request `api://{client_id}/access_as_user` scope instead of Graph scopes
- Extract user info from ID token claims (can't call Graph with custom-scoped token)
- Resulting access token has correct audience for OBO exchange

## Common Strategies

**Authentication patterns**:
- [[concepts/oauth-authentication]] — Integrating OAuth providers with Chainlit
- [[concepts/on-behalf-of-flow]] — Custom provider for OBO token exchange
- [[concepts/user-identity-preservation]] — Passing user tokens to backend agents

**UI customization**:
- [[concepts/chainlit-theming]] — Customizing appearance for brand requirements
- [[concepts/conversational-ux]] — Designing effective chat interfaces

**Integration strategies**:
- [[concepts/multi-agent-orchestration]] — Chainlit as frontend for LangGraph agents
- [[concepts/session-management]] — Storing conversation state and user context
- [[concepts/streaming-responses]] — Real-time LLM response rendering

**Deployment patterns**:
- [[concepts/azure-app-service-deployment]] — Hosting Chainlit with managed infrastructure
- [[concepts/authentication-proxy]] — Using App Service built-in auth with Chainlit

## Related Entities

- [[entities/microsoft-entra-id]] — Identity provider requiring custom OAuth implementation
- [[entities/langgraph]] — Multi-agent orchestration framework Chainlit connects to
- [[entities/databricks-genie]] — Agent accessed via Chainlit UI with OBO tokens
- [[entities/azure-app-service]] — Hosting platform with OAuth integration
- [[entities/msal]] — Library used in custom Chainlit OAuth provider

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Chainlit as UI layer for multi-agent system, custom OAuth provider implementation for OBO flow
