---
title: "A local environment for PostgreSQL with Docker Compose"
type: summary
tags: [docker, postgresql, database, development-environment, devops]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Key Points

- **Complete local PostgreSQL development environment** using Docker Compose with PostgreSQL instance plus administration tools (pgAdmin, Metabase, DBeaver)
- **Initialization automation**: Database automatically initialized from SQL scripts and CSV files via `docker-entrypoint-initdb.d` volume mapping
- **Environment variable configuration**: Credentials and settings externalized in `.env` file for easy customization
- **Multiple access methods**: CLI (psql), web GUI (pgAdmin), BI tool (Metabase), desktop client (DBeaver, pgAdmin Desktop)
- **Modular compose files**: Project provides variants (postgres-only, postgres-pgadmin, postgres-metabase, complete) for different use cases
- **Cross-platform compatible**: Tested on Windows 11 with Docker and Rancher Desktop, works on Windows/Mac/Linux
- **Network and volume management**: Proper Docker practices with named volumes and network isolation
- **Production-ready patterns**: Version pinning (postgres:17.4-alpine example), proper port mapping, container naming

## Relevant Concepts

- [[concepts/docker-compose]] - Infrastructure-as-code for multi-container applications
- [[concepts/database-initialization]] - Automated schema and data setup on container startup
- [[concepts/environment-variables]] - Externalized configuration management
- [[concepts/development-containers]] - Containerized local development environments

## Source Metadata

- **Type**: Technical tutorial article
- **Author**: Christophe Vaudry
- **Source**: Medium / Norsys Octogone blog
- **Date**: 2025-06-11
- **URL**: https://medium.com/norsys-octogone/a-local-environment-for-postgresql-with-docker-compose-7ae68c998068
- **Audience**: Developers setting up local PostgreSQL environments
- **Tools demonstrated**: Docker Compose, PostgreSQL, pgAdmin, Metabase, DBeaver, Rancher Desktop
