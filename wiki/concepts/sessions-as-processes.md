---
title: "Sessions as Processes"
type: concept
tags: [architecture, autonomous-agents, openclaw, foundational, operating-systems]
created: 2026-05-15
updated: 2026-05-15
sources: ["raw/Principles for Autonomous System Design OpenClaw Deep Dive.md"]
confidence: high
---

## Definition

Sessions as Processes is an architectural pattern for autonomous agent systems where each session maps to an operating system process (separate context, permissions, sandboxing), and agents within sessions map to threads. This provides familiar OS-level abstractions for managing concurrent, isolated agent work.

## How It Works

**Session = Process**
- Separate context: Each session maintains independent conversation history
- Separate permissions: Sessions can have different access levels (e.g., admin vs. restricted)
- Sandboxing: Sessions can run in isolated environments
- Parallel execution: Multiple sessions run concurrently
- Inter-session communication: Sessions can send messages to each other

**Agent = Thread**
- Multiple agents per session: Main agent + spawned sub-agents
- Shared session context: All agents in session see same history
- Lightweight compared to sessions
- Framework manages agent spawning (not user-initiated)

**Gateway Controller = Process Scheduler**
- Routes incoming messages to correct session
- Manages session lifecycle (create, pause, terminate)
- Coordinates inter-session communication
- Handles resource allocation

## Key Parameters

**Session Mapping Strategy**
- WhatsApp: One session per contact
- Discord: One session per channel (enables topic organization)
- iMessage: Typically single session (causes context mixing)
- Admin UI: Dedicated main session with elevated permissions

**Context Boundaries**
- Session context: Full conversation history, working directory, loaded skills
- When context overflows: Moved to session database, can be retrieved
- Context isolation prevents cross-talk between unrelated tasks

**Permission Models**
- Session-level: File system access, network permissions, API keys
- System sessions: Main (admin), Heartbeat (monitoring)
- User sessions: Connector-specific isolation

## When To Use

**Multi-Project Management**
- User working on parallel tasks that shouldn't share context
- Different projects need different permissions or environments
- Example: Research paper + website development + ML experiment

**Team Collaboration**
- Multiple users each get isolated sessions
- Prevents one user's context from polluting another's
- Enables user-specific customization within shared agent

**Resource Isolation**
- CPU/memory-intensive tasks in dedicated sessions
- Prevent one runaway task from affecting others
- Clean termination without affecting other work

**Security Boundaries**
- Untrusted code execution in sandboxed session
- Different trust levels for different connectors (personal email vs. public Discord)

## Risks & Pitfalls

**Context Fragmentation**
- User must remember which session has which context
- Cross-session information sharing requires explicit copying
- Solution: Discord Hub pattern with semantic channel naming

**Session Proliferation**
- Too many sessions → tracking overhead
- Each session consumes memory/storage
- Need session garbage collection for abandoned work

**Over-Isolation**
- Some tasks benefit from shared context
- Inter-session communication adds latency and complexity
- Not all work needs process-level isolation

**Permission Confusion**
- Users may forget which session has which permissions
- Escalation attacks: tricking admin session into executing untrusted commands
- Need clear visual indicators of session permissions

## Related Concepts

- [[concepts/gateway-controller]] - The session scheduler/router
- [[concepts/subagents]] - Agents as threads within sessions
- [[concepts/discord-hub-pattern]] - Best practice for session organization
- [[concepts/agent-isolation]] - Security model leveraging session boundaries
- [[concepts/heartbeat-monitoring]] - Special system session for monitoring

## Sources

- [[summaries/openclaw-deep-dive]] - Alex Krentsel explains abstraction (14:02-15:52 in transcript)
