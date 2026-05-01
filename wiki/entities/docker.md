---
title: "Docker"
type: entity
tags: [containers, infrastructure, devops, platform]
created: 2026-05-01
updated: 2026-05-01
sources: ["raw/A local environment for PostgreSQL with Docker Compose.md"]
confidence: high
---

## Overview

Docker is a platform for developing, shipping, and running applications in containers - lightweight, isolated environments that package code and dependencies. Enables consistent environments across development, testing, and production. Industry standard for containerization.

## Characteristics

- **Container engine**: Runs isolated processes with own filesystem, networking, resources
- **Docker Compose**: Tool for multi-container applications defined in YAML
- **Docker Hub**: Public registry with thousands of pre-built images
- **Official images**: Curated images for popular software (postgres, nginx, redis, etc.)
- **Cross-platform**: Windows, Mac, Linux support
- **Docker Desktop**: GUI application with integrated tools (Mac/Windows)
- **CLI tools**: `docker` and `docker compose` commands
- **Rancher Desktop**: Alternative to Docker Desktop with Kubernetes integration

## Common Strategies

- [[concepts/docker-compose]] - Multi-container application orchestration
- [[concepts/development-containers]] - Consistent dev environments
- [[concepts/database-initialization]] - Container startup hooks for database setup
- Microservices deployment with container per service
- CI/CD integration for building and testing

## Related Entities

- [[entities/postgresql]] - Common database deployed in Docker
- [[entities/rancher-desktop]] - Docker Desktop alternative
- [[entities/docker-hub]] - Container image registry

## Sources

- raw/A local environment for PostgreSQL with Docker Compose.md - Docker/Docker Compose for PostgreSQL development
