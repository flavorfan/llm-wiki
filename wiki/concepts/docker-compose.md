---
title: "Docker Compose"
type: concept
tags: [docker, containers, infrastructure-as-code, development-environment, orchestration]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Definition

Docker Compose is a tool for defining and running multi-container Docker applications using YAML configuration files. It enables developers to declare services, networks, and volumes in a single `docker-compose.yml` file and start/stop the entire application stack with simple commands (`docker compose up`/`down`).

## How It Works

1. **Define services**: Each service specifies a container image, environment variables, ports, volumes, and dependencies
2. **Declare infrastructure**: Networks and volumes are defined alongside services for isolation and data persistence
3. **Single command orchestration**: `docker compose up -d` starts all containers in correct order, `docker compose down` stops and removes them
4. **Environment configuration**: Variables externalized in `.env` files are interpolated into compose configuration
5. **Initialization hooks**: Special volume mounts like `/docker-entrypoint-initdb.d` enable startup scripts

## Key Parameters

- **services**: Map of service definitions (container images, ports, volumes, environment)
- **networks**: Network definitions for container communication and isolation
- **volumes**: Named volumes for persistent data storage across container lifecycles
- **env_file / environment**: Configuration via environment variables
- **depends_on**: Service startup ordering
- **ports**: Port mapping between host and container (e.g., `5432:5432`)
- **image**: Container image and version (e.g., `postgres:17.4-alpine`)

## When To Use

- Local development environments requiring multiple services (database + admin tools + application)
- Consistent, reproducible development setups across team members
- Testing multi-service architectures locally before deploying to production
- Providing turnkey development environments via version-controlled compose files
- Quick prototyping with pre-packaged service combinations
- CI/CD pipeline integration for integration testing

## Risks & Pitfalls

- **Version drift**: Using `latest` tags causes non-reproducible builds - pin specific versions in production-like environments
- **Resource consumption**: Running many containers simultaneously requires sufficient host resources (CPU, memory, disk)
- **Network conflicts**: Port collisions if multiple compose projects use same ports
- **Data loss**: Unnamed volumes may not persist correctly - use named volumes for important data
- **Initialization timing**: Services may start before dependencies are ready - use health checks or wait scripts
- **Platform differences**: Windows/Mac use Docker Desktop VM layer with potential performance/path translation issues

## Related Concepts

- [[concepts/development-containers]] - Containerized development environments
- [[concepts/database-initialization]] - Automated database setup patterns
- [[concepts/environment-variables]] - Configuration management
- [[concepts/infrastructure-as-code]] - Declarative infrastructure specification

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - Complete tutorial with PostgreSQL, pgAdmin, Metabase setup
