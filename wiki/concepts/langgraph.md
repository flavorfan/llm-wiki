---
title: "LangGraph"
type: concept
tags: [langchain, agents, graph, workflow, state-management, orchestration]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/LangGraph Checkpoint Postgres.md"]
confidence: high
---

## Definition

LangGraph is a graph-based agent orchestration framework from LangChain that models agent workflows as stateful graphs with nodes (operations) and edges (control flow). It provides persistence, checkpointing, time-travel debugging, and human-in-the-loop capabilities for building production-ready AI agents.

## How It Works

1. **Graph definition**: Define nodes (functions/agents) and edges (transitions) to create workflow graph
2. **State management**: Graph maintains state object passed between nodes, updated via reducers
3. **Execution**: Graph executes nodes in order determined by edges, passing state through
4. **Checkpointing**: After each node execution, state can be persisted to checkpoint storage (memory, SQLite, Postgres)
5. **Time-travel**: Saved checkpoints enable replaying from any point, branching conversations
6. **Human-in-the-loop**: Execution can pause for human approval before continuing

**Key components:**
- **Nodes**: Individual operations (LLM calls, tool execution, data processing)
- **Edges**: Transitions between nodes (conditional or unconditional)
- **State**: Dict-like object with typed schema, updated through reducers
- **Checkpointer**: Persistence backend for saving/loading state
- **Store**: Long-term memory separate from conversation state

## Key Parameters

- **Graph structure**: Nodes and edges defining workflow topology
- **State schema**: TypedDict defining state fields and types
- **Reducers**: Functions controlling how state updates are merged
- **Checkpointer**: Storage backend (`MemorySaver`, `SqliteSaver`, `PostgresSaver`)
- **Thread ID**: Identifier for conversation/session to checkpoint
- **Checkpoint ID**: Specific point in execution history to resume from
- **Store**: Optional long-term memory with vector search

## When To Use

- Multi-step agent workflows requiring state persistence across executions
- Production agents needing reliability (crash recovery via checkpoints)
- Complex conditional branching based on agent outputs
- Human-in-the-loop workflows requiring approval steps
- Time-travel debugging to inspect/replay agent decision points
- Multi-agent systems with communication between agents
- Long-running conversations requiring session management
- Agents with long-term memory beyond conversation history

## Risks & Pitfalls

- **State size growth**: Checkpointing full conversation history causes storage bloat - use shallow mode or implement cleanup
- **Reducer complexity**: Incorrect reducers cause state corruption or lost updates
- **Checkpoint cleanup**: No native API for deleting old checkpoints - requires manual management
- **Migration challenges**: State schema changes may break existing checkpoints
- **Performance overhead**: Checkpointing after every node adds latency - balance frequency vs recovery granularity
- **Concurrency issues**: Async operations require `AsyncPostgresSaver` to avoid blocking
- **Connection pooling**: Database connection management critical for production deployments

## Related Concepts

- [[concepts/langchain-agents]] - LangChain agent framework
- [[concepts/checkpoint-persistence]] - Saving agent state
- [[concepts/state-management]] - Managing execution state
- [[concepts/state-reducers]] - State update patterns
- [[concepts/human-in-the-loop]] - Human approval workflows
- [[concepts/time-travel-debugging]] - Replaying execution history

## Sources

- raw/LangGraph Checkpoint Postgres.md - PostgreSQL checkpoint implementation overview
