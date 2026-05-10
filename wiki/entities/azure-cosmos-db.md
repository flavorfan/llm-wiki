---
title: "Azure Cosmos DB"
type: entity
tags: [database, azure, nosql, distributed, microsoft]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Overview

Azure Cosmos DB is Microsoft's globally distributed, multi-model NoSQL database service. In the context of multi-agent AI systems, it serves as long-term memory storage and checkpoint persistence, enabling agents to maintain conversation history, intermediate state, and workflow progress across sessions.

**Key features**:
- Globally distributed with multi-region replication
- Multiple data models (document, key-value, graph, column-family)
- Automatic indexing
- Low latency (< 10ms reads, < 15ms writes at P99)
- Elastic scale (throughput and storage)
- Multiple consistency levels
- Built-in RBAC with Entra ID integration

**Documentation**: https://learn.microsoft.com/en-us/azure/cosmos-db/overview

## Characteristics

- **Multi-model**: Supports document (JSON), graph (Gremlin), table (key-value), and MongoDB/Cassandra APIs
- **Schema-flexible**: NoSQL design, no fixed schema enforcement (ideal for agent state)
- **Global distribution**: Automatic replication across Azure regions for low-latency access
- **Consistency options**: Five consistency levels from eventual to strong
- **Automatic indexing**: All properties indexed by default (can be customized)
- **Throughput provisioning**: Request Units (RUs) model for predictable performance
- **Serverless option**: Pay-per-request pricing for variable workloads
- **Change feed**: Stream of document changes for real-time processing
- **Time-to-live (TTL)**: Automatic document expiration for ephemeral data
- **ACID transactions**: Within partition, with multi-document transaction support

**For AI agent systems**:
- **Conversation history**: Store user messages and agent responses
- **Checkpoint storage**: LangGraph workflow states for crash recovery
- **Long-term memory**: Facts, preferences, context spanning sessions
- **Session management**: User sessions with token metadata
- **Audit logs**: Agent actions with timestamps and user identity

## Common Strategies

**Agent storage patterns**:
- [[concepts/checkpoint-persistence]] — LangGraph state storage for workflow recovery
- [[concepts/conversation-history]] — Storing chat messages with user context
- [[concepts/long-term-memory]] — Persistent facts and preferences across sessions

**Data modeling**:
- [[concepts/partition-key-design]] — Cosmos DB partitioning strategy (e.g., by user_id)
- [[concepts/document-schema]] — Structuring agent state as JSON documents
- [[concepts/ttl-strategies]] — Auto-expiring ephemeral agent state

**Performance optimization**:
- [[concepts/ru-optimization]] — Minimizing request unit consumption
- [[concepts/indexing-policy]] — Excluding large agent state from indexing
- [[concepts/session-tokens]] — Cosmos DB session consistency for read-after-write

**Integration patterns**:
- [[concepts/entra-id-rbac]] — User-scoped database access with Entra ID
- [[concepts/change-feed-processing]] — Reacting to agent state changes

## Related Entities

- [[entities/langgraph]] — Uses Cosmos DB (or other stores) for checkpoint persistence
- [[entities/microsoft-entra-id]] — Identity provider for Cosmos DB RBAC
- [[entities/azure-app-service]] — Often deployed together for managed hosting
- [[entities/chainlit]] — Web UI storing session data in Cosmos DB
- [[entities/azure-monitor]] — Observability for Cosmos DB performance and cost

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — Cosmos DB as long-term memory and checkpoint storage for multi-agent system
