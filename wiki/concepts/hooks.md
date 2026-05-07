---
title: "Hooks"
type: concept
tags: [design-patterns, lifecycle, callbacks, interception, extensibility, automation, claude-code]
created: 2026-05-01
updated: 2026-05-04
sources: ["raw/langchain-custom-middleware.md", "raw/Hooks reference.md", "raw/Stop Writing Bad CLAUDE.md Files.md"]
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

**Claude Code hooks:**
- **Event-driven**: Hooks fire at specific lifecycle points (session start, tool use, prompt submit, etc.)
- **Five handler types**: Command (shell), HTTP (POST endpoint), MCP tool, Prompt (LLM), Agent (subagent)
- **JSON communication**: Input via stdin/POST body, output via exit codes and JSON stdout
- **Decision control**: Hooks can allow, deny, block, or inject context based on exit codes and JSON output
- **Matchers**: Filter hooks by tool name, event type, command name, or file paths (glob/regex patterns)
- **Three-level config**: Event → Matcher group → Handler(s)

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

**General use cases:**
- **Framework extensibility**: Allow users to customize behavior without forking code
- **Plugin systems**: Third-party integrations via well-defined extension points
- **Cross-cutting concerns**: Logging, metrics, caching applicable to many operations
- **Testing**: Inject mocks, stubs, or test instrumentation
- **Configuration**: Runtime behavior changes without code modifications
- **Migration**: Gradual feature rollout via feature flags in hooks
- **Observability**: Instrument existing systems without invasive changes

**Claude Code specific (replace CLAUDE.md instructions):**
- **Code formatting**: PostToolUse hook runs linters/formatters after Edit/Write instead of style instructions
- **Environment setup**: SessionStart hook loads context, sets environment variables
- **Security validation**: PreToolUse hook validates Bash commands before execution
- **Policy enforcement**: PermissionRequest hook auto-approves/denies based on rules
- **Context injection**: Hooks add dynamic context (current branch, open issues, test results) without static instructions
- **Reactive automation**: FileChanged hook triggers when watched files change
- **Custom workflows**: Stop hook runs before Claude finishes turn (tests, validation, documentation generation)

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
- [[concepts/code-style-automation]] - Using PostToolUse hooks for formatting
- [[concepts/claude-md-configuration]] - Hooks as alternative to instructions
- [[concepts/instruction-following-limits]] - Why hooks are better than instructions for enforcement
- [[concepts/event-driven-architecture]] - Event-based hook systems
- [[concepts/lifecycle-events]] - Session, turn, and tool lifecycle
- [[concepts/permission-system]] - PermissionRequest/PermissionDenied hooks
- [[concepts/context-injection]] - Adding dynamic context via hooks

## Sources

- raw/langchain-custom-middleware.md - LangChain middleware hooks (node-style and wrap-style)
- raw/Hooks reference.md - Claude Code comprehensive hook reference
- raw/Stop Writing Bad CLAUDE.md Files.md - PostToolUse hooks for formatting example
