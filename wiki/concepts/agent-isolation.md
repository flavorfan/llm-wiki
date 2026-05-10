---
title: "Agent Isolation"
type: concept
tags: [security, agents, multi-tenancy, architecture, foundational]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

Agent isolation is the architectural practice of creating separate agent instances for each user or session, ensuring that agents never share state, credentials, or memory across users. This prevents information leakage, permission confusion, and cross-user contamination in multi-tenant AI systems.

## How It Works

**Anti-pattern (global agent)**:
```python
# WRONG: Global agent shared across all users
global_agent = create_genie_agent(service_account_token)

@app.route("/query")
def query(request):
    user = request.user
    return global_agent.query(request.question)  # All users share same agent!
```

**Correct pattern (per-user agent)**:
```python
# RIGHT: Per-user agent with user's token
@app.route("/query")
def query(request):
    user = request.user
    user_token = get_user_obo_token(user)  # Get user's delegated token
    user_agent = create_genie_agent(user_token)  # New agent per request
    return user_agent.query(request.question)
```

**Why isolation matters**:
- **Security**: User A's token shouldn't be accessible to User B's agent
- **Permissions**: Each agent must operate with its user's RBAC scope
- **Memory**: Conversation history shouldn't leak between users
- **State**: Agent state (intermediate results, context) must be user-specific
- **Audit**: Each agent's actions must trace to correct user

**Implementation strategies**:
1. **Per-request instantiation**: Create agent on each API call, pass user token
2. **Session caching**: Cache agents keyed by user ID/session ID, evict on timeout
3. **Thread-local storage**: Store agent in thread-local variable for request scope
4. **Container isolation**: Dedicated container per user (expensive, for high-security scenarios)

**Isolation granularity**:
- Per-user: Each user has their own agent instance(s)
- Per-session: Each login session gets fresh agents
- Per-request: New agent created for every API call (stateless, safest)

## Key Parameters

- **Agent instantiation scope**: Per-request, per-session, or per-user
- **State storage**: Where agent state lives (memory, Redis, database) and how it's keyed
- **Credential passing**: How user tokens are passed to agent (constructor param, context manager)
- **Cache eviction**: When cached agents are destroyed (timeout, logout, memory pressure)
- **Memory isolation**: Separate conversation history per user
- **Resource limits**: Per-user quotas (memory, API calls, storage) to prevent resource exhaustion
- **Session binding**: Tying agent lifecycle to user session
- **Cleanup strategy**: Ensuring agents are garbage-collected when no longer needed

## When To Use

Use agent isolation when:

- **Multi-tenant AI systems**: SaaS products where users share infrastructure
- **Enterprise applications**: Multiple employees using same AI agent service
- **Regulatory compliance**: HIPAA, GDPR, or other regulations prohibiting data sharing
- **Permission-based systems**: Users have different access levels (RBAC, ACLs)
- **Sensitive data**: PII, PHI, financial data, trade secrets in agent context
- **Audit requirements**: Need to trace actions to specific users
- **Conversational agents**: Agent maintains state across turns; state must not leak between users
- **Zero-trust architecture**: Per-user token delegation requires per-user agents
- **Long-running tasks**: Agent processes that might outlive single request

Critical for any multi-user AI system; single-user prototypes can skip isolation.

## Risks & Pitfalls

**Global agent caching**: Most dangerous pitfall — storing agents in global variables or shared caches without user-specific keys

**Session ID confusion**: Using session IDs that aren't cryptographically secure or can be guessed

**Token leakage**: Passing user tokens through global state where other threads/requests can access

**Memory leaks**: Cached agents not evicted, accumulating over time until OOM

**Race conditions**: Multiple requests for same user creating multiple agent instances that interfere

**Credential in logs**: Logging agent state that contains user tokens or sensitive data

**Cross-user prompts**: User A's prompt appearing in User B's context if agents share memory

**Resource exhaustion**: Not limiting per-user agent count; malicious user creates thousands of agents

**Stale credentials**: Cached agent holding expired token; need refresh or re-instantiation

**Development shortcuts**: Using global agents during development, forgetting to fix for production

**Serialization issues**: Attempting to serialize/deserialize agents containing user credentials

**Shared libraries**: Agent libraries with module-level state can cause cross-user contamination

## Related Concepts

- [[concepts/zero-trust-agents]] — Isolation enables zero-trust by ensuring agents inherit user permissions
- [[concepts/user-identity-preservation]] — Isolated agents maintain user identity through token delegation
- [[concepts/on-behalf-of-flow]] — Per-user tokens require per-user agents
- [[concepts/multi-tenancy]] — Broader architectural pattern agent isolation implements
- [[concepts/session-management]] — Tying agent lifecycle to user sessions
- [[concepts/state-management]] — Managing per-user agent state safely
- [[concepts/resource-quotas]] — Preventing per-user resource exhaustion
- [[concepts/thread-safety]] — Concurrent requests for same user must not interfere

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — "A critical design decision: never cache user-specific agents globally. Each user needs their own Genie agent instance."
