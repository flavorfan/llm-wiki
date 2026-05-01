---
title: "Middleware Pattern"
type: concept
tags: [design-patterns, agents, interception, cross-cutting-concerns, langchain]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-custom-middleware.md", "raw/langchain-middleare-overview.md"]
confidence: high
---

## Definition

The middleware pattern is a design pattern where functions/objects are inserted into an execution pipeline to intercept, modify, or observe requests and responses. In LangChain agents, middleware provides hooks at specific lifecycle points (before/after model calls, tool execution) to implement cross-cutting concerns like logging, retries, guardrails, and transformations without modifying core agent logic.

## How It Works

**LangChain middleware execution:**
1. **Registration**: Middleware passed to `create_agent(middleware=[...])` as ordered list
2. **Hook points**: Framework calls registered hooks at specific execution points
3. **Sequential before hooks**: Before hooks execute in order (middleware1 → middleware2 → middleware3)
4. **Nested wrap hooks**: Wrap hooks nest like function calls (outer wraps inner)
5. **Reverse after hooks**: After hooks execute in reverse order (middleware3 → middleware2 → middleware1)
6. **State updates**: Middleware can update agent state, jump to different nodes, or short-circuit execution

**Hook types:**
- **Node-style**: Run at specific points (`before_agent`, `before_model`, `after_model`, `after_agent`)
- **Wrap-style**: Wrap around calls (`wrap_model_call`, `wrap_tool_call`) with full control over handler invocation

**Implementation styles:**
- **Decorator-based**: `@before_model` decorator for simple, single-hook middleware
- **Class-based**: `AgentMiddleware` subclass for complex, multi-hook middleware with sync/async variants

## Key Parameters

- **Middleware list**: Ordered array determines execution sequence
- **Hook type**: Node-style (sequential) vs wrap-style (control flow)
- **State schema**: Extended state schema for middleware-specific properties
- **Jump targets**: Allowed destinations for early exit (`can_jump_to=['end', 'tools', 'model']`)
- **Handler function**: Callable passed to wrap hooks - middleware decides if/how many times to invoke

## When To Use

- **Observability**: Logging, analytics, debugging, tracing across all agent executions
- **Guardrails**: Content filtering, PII detection, safety checks before/after model calls
- **Reliability**: Retries, fallbacks, circuit breakers for transient failures
- **Performance**: Caching, prompt optimization, model selection, rate limiting
- **Customization**: Dynamic prompts, tool filtering, output transformation
- **Compliance**: Audit logging, usage tracking, cost monitoring
- **Development**: Debug logging, performance profiling, test instrumentation

## Risks & Pitfalls

- **Order matters**: Middleware order affects behavior (logging before retry captures all attempts)
- **Error propagation**: Middleware exceptions crash agent unless caught - implement defensive error handling
- **Performance overhead**: Each middleware adds latency - keep hooks fast, use async when possible
- **State conflicts**: Multiple middleware updating same state fields requires careful reducer design
- **Complexity accumulation**: Too many middleware makes behavior hard to understand and debug
- **Tight coupling**: Middleware accessing internal agent details becomes brittle across versions
- **Infinite loops**: Wrap middleware retrying indefinitely can hang agent - always set max attempts
- **Silent failures**: Middleware swallowing exceptions masks underlying issues

## Related Concepts

- [[concepts/langchain-agents]] - LangChain agent framework
- [[concepts/hooks]] - Lifecycle callbacks
- [[concepts/cross-cutting-concerns]] - Aspects affecting multiple modules
- [[concepts/decorator-pattern]] - Function wrapping pattern
- [[concepts/interceptor-pattern]] - Request/response interception
- [[concepts/aspect-oriented-programming]] - Modular cross-cutting concerns

## Sources

- raw/langchain-custom-middleware.md - Detailed custom middleware implementation guide
- raw/langchain-middleare-overview.md - High-level middleware concept introduction
