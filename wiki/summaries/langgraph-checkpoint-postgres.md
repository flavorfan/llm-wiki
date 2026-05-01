---
title: "LangGraph Checkpoint Postgres"
type: summary
tags: [langgraph, postgresql, state-persistence, checkpointing, langchain]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/LangGraph Checkpoint Postgres.md"]
confidence: high
---

## Key Points

- **Official LangChain implementation**: `langgraph-checkpoint-postgres` is the official, production-ready PostgreSQL checkpoint implementation for LangGraph
- **Dual sync/async support**: Provides both `PostgresSaver` (sync) and `AsyncPostgresSaver` (async) classes for flexible integration
- **Cross-language availability**: Available as Python package (`pip install langgraph-checkpoint-postgres`) and JavaScript/TypeScript npm package (`@langchain/langgraph-checkpoint-postgres`)
- **Long-term memory support**: Includes `PostgresStore` and `AsyncPostgresStore` for persistent memory with vector search via pgvector extension
- **Shallow mode option**: Lightweight `shallow` variant saves only latest state without time-travel capabilities for reduced storage overhead
- **Production optimization**: Designed for LangGraph Cloud, officially maintained by LangChain team
- **Setup pattern**: Simple connection string initialization (`PostgresSaver.from_conn_string(DB_URI)`), requires one-time `.setup()` call to create tables
- **Concurrency support**: Async versions support concurrent agent execution
- **Cleanup limitation**: No native API for deleting old checkpoints - requires manual SQL or third-party solutions
- **Community alternatives**: Minor community fork exists (baudm/langgraph-checkpoint-postgres) but official version is recommended

## Relevant Concepts

- [[concepts/langgraph]] - Graph-based agent framework from LangChain
- [[concepts/checkpoint-persistence]] - Saving agent state between executions
- [[concepts/state-management]] - Managing agent conversation and execution state
- [[concepts/vector-search]] - Semantic search capabilities for long-term memory
- [[concepts/async-programming]] - Asynchronous execution patterns for agents

## Source Metadata

- **Type**: AI-generated documentation summary (DeepSeek chat)
- **Language**: Chinese with code examples
- **Date**: 2026-04-18
- **Primary references**: LangChain official docs, GitHub repository (langchain-ai/langgraph), PyPI package page
- **Technical level**: Intermediate - assumes familiarity with LangGraph and PostgreSQL
