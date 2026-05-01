---
title: "Checkpoint Persistence"
type: concept
tags: [langgraph, state-management, persistence, reliability, crash-recovery]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/LangGraph Checkpoint Postgres.md"]
confidence: high
---

## Definition

Checkpoint persistence is the practice of saving agent execution state at strategic points (checkpoints) to enable crash recovery, conversation resumption, time-travel debugging, and branching conversations. In LangGraph, checkpoints capture the full agent state after each node execution.

## How It Works

**LangGraph checkpoint flow:**
1. **Execute node**: Agent executes a node (model call, tool execution)
2. **State update**: Node updates agent state via reducers
3. **Save checkpoint**: Checkpointer saves full state to storage backend
4. **Continue or resume**: Execution continues, or can later resume from saved checkpoint

**Storage backends:**
- **MemorySaver**: In-memory (development, testing)
- **SqliteSaver**: SQLite database (single-machine persistence)
- **PostgresSaver**: PostgreSQL (production, distributed systems)
- **Shallow variant**: Saves only latest state, no history (reduced storage)

**Recovery patterns:**
- **Thread-based**: Each conversation has `thread_id`, checkpoints saved per thread
- **Time-travel**: Load any historical checkpoint by `checkpoint_id`
- **Branching**: Create new conversation branch from any checkpoint

## Key Parameters

- **Checkpointer type**: Storage backend choice (`PostgresSaver`, `AsyncPostgresSaver`, etc.)
- **Connection string**: Database connection for persistent storage
- **Thread ID**: Conversation identifier for checkpoint isolation
- **Checkpoint ID**: Specific checkpoint to load for time-travel
- **Shallow mode**: Boolean - save only latest state (true) or full history (false)
- **Setup**: One-time `.setup()` call to create database schema

## When To Use

- **Production agents**: Enable crash recovery and conversation resumption
- **Long-running conversations**: Persist state across server restarts
- **Multi-session workflows**: User can leave and return later
- **Debugging**: Replay agent decisions from specific checkpoints
- **A/B testing**: Branch conversations to try different agent configurations
- **Compliance**: Audit trail of agent decision-making
- **Human-in-the-loop**: Save state while awaiting human approval
- **Distributed systems**: Share agent state across multiple processes/servers

## Risks & Pitfalls

- **Storage explosion**: Full history checkpointing for long conversations consumes GB of storage - use shallow mode or implement cleanup
- **No cleanup API**: LangGraph checkpoint implementations lack native delete - requires manual SQL or custom tooling
- **Schema migration**: Changing state schema breaks old checkpoints - plan migration strategy
- **Sensitive data**: Checkpoints may contain PII, credentials, API keys - encrypt storage and implement retention policies
- **Performance overhead**: Checkpoint save latency adds to each node execution - use async savers and connection pooling
- **Concurrent writes**: Multiple processes updating same thread require careful locking/transaction handling
- **Checkpoint corruption**: Partial writes during crash leave inconsistent state

## Related Concepts

- [[concepts/langgraph]] - Graph-based agent framework
- [[concepts/state-management]] - Managing agent state
- [[concepts/crash-recovery]] - Recovering from failures
- [[concepts/time-travel-debugging]] - Replaying execution
- [[concepts/conversation-persistence]] - Saving chat history

## Sources

- raw/LangGraph Checkpoint Postgres.md - PostgreSQL checkpoint implementation details
