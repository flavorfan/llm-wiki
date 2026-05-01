---
title: "LangChain Custom Middleware"
type: summary
tags: [langchain, middleware, agents, hooks, interception, state-management]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-custom-middleware.md"]
confidence: high
---

## Key Points

- **Two hook styles**: Node-style hooks (sequential execution points) and wrap-style hooks (around each call with control flow)
- **Node-style hooks**: `before_agent`, `before_model`, `after_model`, `after_agent` - run at specific lifecycle points for logging, validation, state updates
- **Wrap-style hooks**: `wrap_model_call`, `wrap_tool_call` - intercept execution with full control (retry logic, caching, short-circuit, transformation)
- **Two implementation patterns**: Decorator-based (quick, single-hook) and class-based (complex, multi-hook, sync+async)
- **State extension**: Middleware can extend agent state with custom properties via `state_schema` parameter for cross-hook data sharing
- **State updates differ by hook type**: Node-style returns dict directly, wrap-style returns `ExtendedModelResponse` with `Command` for model calls or `Command` directly for tools
- **Agent jumps**: Middleware can exit early via `jump_to` with targets: `'end'`, `'tools'`, `'model'` - requires `can_jump_to` declaration
- **Execution order**: Before hooks run in order (1→2→3), wrap hooks nest (1 wraps 2 wraps 3), after hooks run in reverse (3→2→1)
- **Command composition**: Multiple middleware can return `ExtendedModelResponse` - commands compose with reducers (additive for messages), outer wins on conflicts for non-reducer fields
- **Dynamic capabilities**: Modify system prompts, select models, filter tools, add caching directives - all at runtime before each call
- **Common use cases**: Dynamic prompts, model selection, tool filtering, monitoring, retries, prompt caching (Anthropic), PII detection, rate limiting

## Relevant Concepts

- [[concepts/langchain-agents]] - LangChain agent framework
- [[concepts/middleware-pattern]] - Interceptor pattern for request/response processing
- [[concepts/hooks]] - Lifecycle callbacks for execution interception
- [[concepts/state-reducers]] - State update aggregation patterns
- [[concepts/prompt-engineering]] - Dynamic prompt modification
- [[concepts/tool-selection]] - Runtime tool filtering strategies

## Source Metadata

- **Type**: Official documentation
- **Source**: LangChain OSS Python documentation
- **URL**: https://docs.langchain.com/oss/python/langchain/middleware/custom
- **Audience**: LangChain developers building custom agent middleware
- **Related docs**: Built-in middleware reference, testing agents, middleware API reference
