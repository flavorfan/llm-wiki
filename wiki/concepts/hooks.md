---
title: "Hooks"
type: concept
tags: [design-patterns, lifecycle, callbacks, interception, extensibility]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-custom-middleware.md"]
confidence: high
---

## Definition

Hooks are predefined callback points in a program's execution flow where custom code can be injected to observe, modify, or control behavior. They enable extensibility by allowing users to attach custom logic at specific lifecycle events without modifying the core system.

## How It Works

**General pattern:**
1. **Define hook points**: Framework exposes named hooks at key execution stages
2. **Register handlers**: Users attach functions/callbacks to specific hooks
3. **Automatic invocation**: Framework calls registered handlers when reaching hook points
4. **Pass context**: Framework provides relevant state/data to handler
5. **Process results**: Handlers can return values to modify execution flow

**LangChain agent hooks:**
- **Node-style**: Sequential callbacks at fixed points (`before_model`, `after_model`)
  - Receive state and runtime context
  - Return dict to update state or `None` for no changes
  - Can return `jump_to` to change control flow
- **Wrap-style**: Intercept with control over handler invocation (`wrap_model_call`)
  - Receive request and handler function
  - Decide if/how many times to invoke handler
  - Can transform request/response, retry, or short-circuit

## Key Parameters

- **Hook name/type**: Identifies when hook executes (`before_agent`, `after_model`, etc.)
- **Handler signature**: Expected parameters (state, runtime, request, handler)
- **Return value**: Determines effect (state updates, control flow changes)
- **Execution order**: Relative position in middleware list
- **Sync vs async**: Separate hooks for synchronous/asynchronous execution

## When To Use

- **Framework extensibility**: Allow users to customize behavior without forking code
- **Plugin systems**: Third-party integrations via well-defined extension points
- **Cross-cutting concerns**: Logging, metrics, caching applicable to many operations
- **Testing**: Inject mocks, stubs, or test instrumentation
- **Configuration**: Runtime behavior changes without code modifications
- **Migration**: Gradual feature rollout via feature flags in hooks
- **Observability**: Instrument existing systems without invasive changes

## Risks & Pitfalls

- **Version coupling**: Hooks tied to internal implementation details break across versions
- **Performance impact**: Each hook adds overhead - multiple hooks compound latency
- **Error handling**: Hook exceptions must be caught carefully to avoid crashing host system
- **Debugging difficulty**: Control flow becomes non-linear, hard to trace through multiple hooks
- **Hook proliferation**: Too many granular hooks overwhelm users, few coarse hooks limit flexibility
- **Ordering dependencies**: Hooks may depend on execution order, making them fragile
- **State mutation**: Hooks modifying shared state can cause race conditions in async contexts
- **Documentation burden**: Each hook requires clear documentation of purpose, parameters, return values

## Related Concepts

- [[concepts/middleware-pattern]] - Hooks as implementation mechanism for middleware
- [[concepts/callback-pattern]] - General callback concept
- [[concepts/event-driven-architecture]] - Event-based hook systems
- [[concepts/plugin-architecture]] - Extensibility via plugins using hooks
- [[concepts/aspect-oriented-programming]] - Similar to around/wrap hooks
- [[concepts/lifecycle-methods]] - React/framework lifecycle as hook examples

## Sources

- raw/langchain-custom-middleware.md - LangChain middleware hooks (node-style and wrap-style)
