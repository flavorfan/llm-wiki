---
title: "PostgreSQL"
type: entity
tags: [database, relational, sql, open-source]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md", "raw/LangGraph Checkpoint Postgres.md"]
confidence: high
---

## Overview

PostgreSQL is an open-source, ACID-compliant relational database management system known for robustness, extensibility, and SQL standards compliance. Used for everything from local development to production systems storing critical data. Supports advanced features like JSON/JSONB, full-text search, and extensions (pgvector for vector embeddings).

## Characteristics

- **Open source**: Free, PostgreSQL license (permissive)
- **ACID compliance**: Reliable transactions with strong consistency guarantees
- **Extensibility**: Support for custom data types, functions, operators, and extensions
- **Standards compliance**: Strong SQL standard adherence
- **Docker official image**: `postgres` on Docker Hub with variants (alpine, bullseye, specific versions)
- **Initialization hooks**: `/docker-entrypoint-initdb.d/` for startup scripts
- **CLI tool**: `psql` command-line interface for database interaction
- **Vector search**: pgvector extension enables embedding storage and similarity search
- **Default port**: 5432

## Common Strategies

- [[concepts/docker-compose]] - Container-based local development environments
- [[concepts/database-initialization]] - Automated schema and data setup
- [[concepts/checkpoint-persistence]] - LangGraph agent state storage
- [[concepts/vector-search]] - Semantic search via pgvector extension

## Related Entities

- [[entities/pgadmin]] - Web and desktop GUI administration tool
- [[entities/metabase]] - Business intelligence and analytics platform
- [[entities/dbeaver]] - Universal database management tool
- [[entities/docker]] - Container runtime for PostgreSQL deployment
- [[entities/langchain]] - Uses PostgreSQL for LangGraph checkpointing

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - Docker-based development setup
- raw/LangGraph Checkpoint Postgres.md - PostgreSQL as checkpoint storage backend
