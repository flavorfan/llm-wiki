---
title: "Database Initialization"
type: concept
tags: [databases, automation, devops, postgresql, schema-management]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Definition

Database initialization is the automated process of setting up database schema, loading initial data, and configuring settings when a database instance first starts. In containerized environments, this typically involves executing SQL scripts and data import commands via special startup hooks.

## How It Works

**PostgreSQL Docker pattern:**
1. **Volume mapping**: Mount local directory to container's `/docker-entrypoint-initdb.d/`
2. **Script execution**: On first startup, PostgreSQL container executes all `.sql`, `.sql.gz`, `.sh` files in alphabetical order
3. **Schema creation**: SQL scripts create tables, indexes, constraints, views
4. **Data loading**: `COPY` commands import CSV/data files into created tables
5. **One-time execution**: Scripts run only if data directory is empty (fresh database)

**General pattern:**
- Migration tools (Flyway, Liquibase) for versioned, repeatable migrations
- ORM migrations (Alembic, Django migrations) for application-driven schema evolution
- Seed data scripts for development/testing fixtures

## Key Parameters

- **Initialization directory**: Location for startup scripts (`/docker-entrypoint-initdb.d/` for Postgres)
- **Execution order**: Alphabetical by filename - use prefixes (01_, 02_) to control order
- **Idempotency**: Scripts should handle repeated execution gracefully (`IF NOT EXISTS`, `CREATE OR REPLACE`)
- **Data sources**: CSV files, JSON, SQL dumps - must be accessible within container
- **Error handling**: Initialization failure typically prevents container startup

## When To Use

- Setting up local development databases with schema and sample data
- Automated testing environments requiring fresh database state per test run
- CI/CD pipelines where database must be provisioned from scratch
- Demo/training environments with pre-populated example data
- Microservices with self-contained database initialization
- Multi-tenant systems where each tenant database follows same schema

## Risks & Pitfalls

- **Initialization only runs once**: Changing scripts requires destroying volume and recreating container
- **Large datasets slow startup**: Loading GBs of data on every container recreation impairs developer experience
- **Hardcoded credentials**: Avoid embedding passwords in SQL scripts - use environment variables
- **Missing files**: Script references to CSV/data files fail if not mounted in container
- **Order dependencies**: Table creation must precede data loading, foreign keys must reference existing tables
- **Production risk**: Initialization scripts suitable for development may be dangerous in production (DROP TABLE commands)
- **No rollback**: Failed initialization leaves database in inconsistent state

## Related Concepts

- [[concepts/docker-compose]] - Container orchestration including database services
- [[concepts/schema-migration]] - Versioned database schema changes
- [[concepts/seed-data]] - Sample data for development/testing
- [[concepts/infrastructure-as-code]] - Declarative infrastructure setup

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - PostgreSQL initialization with CSV data import example
