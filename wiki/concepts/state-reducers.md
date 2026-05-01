---
title: "State Reducers"
type: concept
tags: [state-management, functional-programming, data-structures, agents, langgraph]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/langchain-custom-middleware.md"]
confidence: high
---

## Definition

State reducers are functions that define how state updates are merged or combined when multiple sources attempt to modify the same state field. In agent frameworks like LangGraph, reducers ensure predictable state evolution when middleware, nodes, and commands all update shared state.

## How It Works

**Basic pattern:**
```python
def reducer(current_value, new_value):
    return merged_value
```

**Common reducer types:**
- **Last-wins**: New value replaces old (`return new_value`)
- **Additive**: Append to list/array (`return current + new`)
- **Merge**: Deep merge dicts (`return {**current, **new}`)
- **Max/min**: Keep highest/lowest value
- **Custom logic**: Domain-specific merge rules

**LangGraph application:**
1. **State schema**: Each field annotated with reducer: `Annotated[list, add_messages]`
2. **Update received**: Node/middleware returns dict with state updates
3. **Apply reducer**: For each field, call reducer with current value and update
4. **New state**: Result becomes current state for next operation

**Message handling example:**
```python
# Additive reducer for messages
messages: Annotated[list, add_messages]
# Updates: {"messages": [new_msg1, new_msg2]}
# Result: existing_messages + [new_msg1, new_msg2]
```

## Key Parameters

- **Reducer function**: Function defining merge logic `(old, new) -> merged`
- **Field annotation**: State schema associates field with reducer
- **Update order**: When multiple updates occur, order of reducer application matters
- **Initialization**: Reducer must handle empty/None initial values

## When To Use

- **List fields**: Messages, tool calls, errors - use additive reducers
- **Counter fields**: Token usage, request counts - use addition reducer
- **Configuration fields**: Settings, flags - use last-wins or merge reducer
- **Aggregation fields**: Metrics, scores - use custom aggregation logic
- **Idempotent updates**: Use set-based reducers for unique collections
- **Conflict resolution**: When multiple sources update same field simultaneously

## Risks & Pitfalls

- **Non-commutative reducers**: Order-dependent reducers cause different results based on update sequence
- **Memory growth**: Additive reducers without bounds cause unbounded state growth
- **Lost updates**: Last-wins reducer discards previous values - use only when appropriate
- **Initialization errors**: Reducers failing on None/empty initial values crash agent
- **Type mismatches**: Reducer receiving wrong type raises exceptions - validate types
- **Side effects**: Reducers with side effects (I/O, mutation) break functional contract
- **Performance**: Complex merge logic in hot path adds latency per update

## Related Concepts

- [[concepts/state-management]] - Managing application state
- [[concepts/functional-programming]] - Pure functions without side effects
- [[concepts/langgraph]] - Graph-based agent framework using reducers
- [[concepts/command-pattern]] - State updates as commands
- [[concepts/conflict-resolution]] - Resolving concurrent updates
- [[concepts/operational-transformation]] - Advanced merge strategies

## Sources

- raw/langchain-custom-middleware.md - LangGraph reducer usage in middleware state updates
