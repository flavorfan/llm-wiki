---
title: "LangChain"
type: entity
tags: [ai-framework, agents, llm, python, typescript, orchestration]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/LangGraph Checkpoint Postgres.md", "raw/langchain-custom-middleware.md", "raw/langchain-middleare-overview.md"]
confidence: high
---

## Overview

LangChain is an open-source framework for building applications powered by language models. Provides abstractions for LLM integration, agents, chains, memory, and tools. Core projects include LangChain (base framework), LangGraph (graph-based agents), LangSmith (observability), and LangServe (deployment).

## Characteristics

- **Multi-language**: Python (`langchain`) and JavaScript/TypeScript (`langchainjs`) implementations
- **Modular architecture**: Composable components (LLMs, prompts, chains, agents, memory)
- **Agent framework**: `create_agent()` API with middleware, tools, state management
- **LangGraph**: Graph-based workflow orchestration with checkpointing
- **Tool ecosystem**: Integrations with hundreds of LLMs, vector stores, APIs, databases
- **Middleware system**: Hooks for logging, retries, guardrails, transformations
- **Production features**: Checkpointing, human-in-the-loop, streaming, async support
- **Official packages**: `langgraph-checkpoint-postgres`, `langgraph-checkpoint-sqlite`, etc.
- **LangChain AI org**: GitHub organization `langchain-ai` with main repositories

## Common Strategies

- [[concepts/langchain-agents]] - Building AI agents with tools and reasoning
- [[concepts/middleware-pattern]] - Cross-cutting concerns via middleware hooks
- [[concepts/langgraph]] - Graph-based agent workflows
- [[concepts/checkpoint-persistence]] - Agent state persistence
- [[concepts/prompt-engineering]] - Dynamic prompt construction

## Related Entities

- [[entities/postgresql]] - Checkpoint storage backend
- [[entities/openai]] - LLM provider integration
- [[entities/anthropic]] - Claude model integration
- [[entities/langgraph]] - Graph orchestration sub-project

## Sources

- raw/LangGraph Checkpoint Postgres.md - LangGraph PostgreSQL integration
- raw/langchain-custom-middleware.md - Middleware system documentation
- raw/langchain-middleare-overview.md - Middleware overview
