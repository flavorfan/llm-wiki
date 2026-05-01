---
title: "pgAdmin"
type: entity
tags: [database-tools, postgresql, gui, administration]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Overview

pgAdmin is the official open-source administration and development platform for PostgreSQL. Available as web application (runs in browser) and desktop application (Electron-based). Provides graphical interface for database management, query execution, schema design, and server monitoring.

## Characteristics

- **Official tool**: Maintained by PostgreSQL community
- **Dual deployment**: Web version (docker: `dpage/pgadmin4`) and desktop client
- **Rich features**: Schema browser, SQL editor, query builder, monitoring, backup/restore
- **Docker image**: `dpage/pgadmin4` on Docker Hub
- **Configuration**: Email and password set via `PGADMIN_DEFAULT_EMAIL`, `PGADMIN_DEFAULT_PASSWORD` environment variables
- **Default port**: 80 for web version (typically mapped to host port like 5433)
- **Electron-based desktop**: `runtime/pgAdmin4.exe` on Windows
- **Resource intensive**: Electron app requires significant system resources

## Common Strategies

- Web deployment via Docker Compose alongside PostgreSQL instance
- Desktop installation for heavyweight database administration tasks
- Server registration connects to PostgreSQL via host name, port, credentials
- Query development and schema design in visual interface

## Related Entities

- [[entities/postgresql]] - Database system pgAdmin manages
- [[entities/docker]] - Container runtime for web pgAdmin deployment
- [[entities/dbeaver]] - Alternative database tool (lighter weight)
- [[entities/metabase]] - Complementary BI tool (analytics, not administration)

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - pgAdmin setup in Docker Compose
