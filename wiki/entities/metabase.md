---
title: "Metabase"
type: entity
tags: [business-intelligence, analytics, visualization, database-tools]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Overview

Metabase is an open-source business intelligence and analytics platform that enables users to explore data, create dashboards, and visualize metrics without SQL knowledge. Provides web interface for querying databases, building charts, and sharing insights. Different use case than pgAdmin - focused on analytics and insights rather than database administration.

## Characteristics

- **Business intelligence focus**: Data exploration, visualization, dashboards
- **No-SQL interface**: Visual query builder alongside SQL editor
- **Open source**: Free version with paid enterprise features
- **Docker image**: `metabase/metabase` on Docker Hub
- **Multi-database support**: Connects to PostgreSQL, MySQL, MongoDB, and many others
- **Default port**: 3000 (typically mapped to host port like 5434)
- **First-run configuration**: Web wizard for language, user setup, database connection
- **Dashboard sharing**: Collaborative analytics with shareable dashboards

## Common Strategies

- Deploy alongside application database for real-time analytics
- Create dashboards for business metrics, user behavior, system health
- Democratize data access - non-technical users can explore data
- Embed dashboards in internal tools and applications

## Related Entities

- [[entities/postgresql]] - One of many supported database backends
- [[entities/docker]] - Container deployment method
- [[entities/pgadmin]] - Complementary tool (administration vs analytics)
- [[entities/dbeaver]] - Database administration alternative

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - Metabase in Docker Compose setup
