---
title: "LangChain Middleware Overview"
type: summary
tags: [langchain, middleware, agents, observability, control-flow]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-middleare-overview.md"]
confidence: high
---

## Key Points

- **Purpose**: Middleware provides tight control over agent execution for tracking, transforming, and controlling agent behavior
- **Core use cases**: Logging/analytics/debugging, prompt/tool/output transformation, retries/fallbacks/early termination, rate limits/guardrails/PII detection
- **Integration**: Add middleware via `create_agent(middleware=[...])` parameter as list of middleware instances
- **Agent loop structure**: Core loop is model call → tool selection → tool execution → repeat until no tools called
- **Hook points exposed**: Middleware hooks available before/after agent start/end, before/after model calls, wrapping model calls, wrapping tool calls
- **Built-in middleware examples**: SummarizationMiddleware (conversation compression), HumanInTheLoopMiddleware (human approval), LLMToolSelector (dynamic tool filtering), ModelFallback (fallback on failure), ToolRetry (retry on tool errors), ModelCallLimit (rate limiting), PIIDetection (detect sensitive data)
- **Visual flow**: Documentation includes diagrams showing core agent loop and middleware insertion points

## Relevant Concepts

- [[concepts/langchain-agents]] - LangChain agent framework
- [[concepts/middleware-pattern]] - Interceptor pattern for request/response processing
- [[concepts/observability]] - Monitoring and tracking agent behavior
- [[concepts/guardrails]] - Safety and control mechanisms for AI agents
- [[concepts/summarization]] - Conversation compression techniques
- [[concepts/human-in-the-loop]] - Human approval workflows

## Source Metadata

- **Type**: Official documentation overview
- **Source**: LangChain OSS Python documentation  
- **URL**: https://docs.langchain.com/oss/python/langchain/middleware/overview
- **Description**: High-level introduction to middleware concept
- **Audience**: LangChain developers learning about middleware capabilities
- **Related docs**: Custom middleware guide, built-in middleware reference
