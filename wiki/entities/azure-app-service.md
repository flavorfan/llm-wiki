---
title: "Azure App Service"
type: entity
tags: [azure, hosting, paas, web-apps, microsoft]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Azure App Service is Microsoft's fully managed platform-as-a-service (PaaS) for hosting web applications, REST APIs, and mobile backends. It provides built-in authentication support with Microsoft Entra ID, automatic scaling, and managed infrastructure, making it a natural choice for hosting enterprise AI applications like Chainlit-based multi-agent systems.

**Key features**:
- Managed hosting (no VM maintenance)
- Built-in authentication (Entra ID, Google, Facebook, etc.)
- Automatic scaling (vertical and horizontal)
- Deployment slots (staging, production)
- Continuous deployment (GitHub, Azure DevOps)
- SSL/TLS certificates
- Custom domains
- Application insights integration
- Hybrid connectivity (VNet, VPN)

**Documentation**: https://learn.microsoft.com/en-us/azure/app-service/

## Characteristics

- **PaaS model**: Managed runtime, patching, and infrastructure; focus on code, not servers
- **Multi-language support**: Python, Node.js, .NET, Java, PHP, Ruby
- **Built-in auth**: "Easy Auth" feature integrates Entra ID OAuth without code changes
- **Autoscaling**: Scale based on metrics (CPU, requests) or schedule
- **Deployment slots**: Blue-green deployments with traffic splitting
- **HTTPS by default**: Free SSL certificates for custom domains
- **Logging**: Application logs, web server logs, diagnostic traces
- **Monitoring**: Integrated with Azure Monitor and Application Insights
- **Hybrid scenarios**: Connect to on-premises data via VNet or Hybrid Connections
- **Container support**: Can host Docker containers or App Service native runtime

**Authentication integration**:
- Built-in OAuth provider support (Entra ID, Google, Facebook, Twitter, GitHub)
- Token injection into app headers (`X-MS-TOKEN-AAD-ACCESS-TOKEN`)
- Session management handled by platform
- Can be combined with custom OAuth providers for advanced scenarios (OBO flow)

## Common Strategies

**Hosting patterns**:
- [[concepts/chainlit-deployment]] — Hosting Python Chainlit apps on App Service
- [[concepts/multi-agent-hosting]] — Deploying LangGraph orchestrators
- [[concepts/deployment-slots]] — Staging and production environment strategy

**Authentication patterns**:
- [[concepts/built-in-authentication]] — Using App Service Easy Auth for SSO
- [[concepts/custom-oauth-provider]] — Integrating MSAL for OBO scenarios
- [[concepts/authentication-proxy]] — App Service as OAuth gateway to backend

**Scaling strategies**:
- [[concepts/autoscaling-rules]] — Metric-based or schedule-based scaling
- [[concepts/session-affinity]] — ARR affinity for stateful apps
- [[concepts/scale-out-agents]] — Horizontal scaling considerations for agent instances

**Monitoring patterns**:
- [[concepts/application-insights]] — Performance monitoring and debugging
- [[concepts/diagnostic-logging]] — App and server log collection
- [[concepts/availability-monitoring]] — Health checks and uptime tracking

## Related Entities

- [[entities/microsoft-entra-id]] — Identity provider for App Service authentication
- [[entities/chainlit]] — Python framework commonly hosted on App Service
- [[entities/langgraph]] — Multi-agent orchestrator deployed to App Service
- [[entities/azure-cosmos-db]] — Often paired for agent state storage
- [[entities/azure-monitor]] — Observability platform for App Service

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — App Service as managed hosting with built-in authentication support and autoscaling for Chainlit + LangGraph system
