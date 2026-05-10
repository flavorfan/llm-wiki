---
title: "Human-in-the-Loop (HITL)"
type: concept
tags: [ai-safety, approval-workflows, agents, security, guardrails, foundational]
created: 2026-05-10
updated: 2026-05-10
sources: ["Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md"]
confidence: high
---

## Definition

Human-in-the-Loop (HITL) is a safeguard pattern where AI agents pause execution before performing high-risk or irreversible actions, presenting the intended action to a human for explicit approval or modification. The agent cannot proceed until receiving human confirmation, creating a mandatory checkpoint that prevents automated mistakes with severe consequences.

## How It Works

1. **Agent intent detection**: Agent or orchestrator identifies planned action as high-risk (DELETE, UPDATE, financial transaction, email send, etc.)
2. **Execution pause**: Agent workflow interrupts before performing the action
3. **User notification**: System presents intended action details to human (SQL query, parameters, affected records, etc.)
4. **Approval interface**: User reviews and chooses: Approve | Modify | Reject
5. **Conditional execution**: Agent proceeds only on approval, retries on modification, aborts on rejection
6. **Audit logging**: Record human decision (who approved, when, what was approved)

**Implementation mechanisms**:

- **LangGraph interrupts**: Built-in workflow pause points where agent yields control
- **Intent classification**: LLM-based analysis of SQL/operations to detect destructive patterns (DELETE, UPDATE, DROP, TRUNCATE)
- **Rule-based triggers**: Pattern matching on operations, keywords, or affected row counts
- **Approval UI**: Web interface, Slack bot, or CLI prompt for human decision
- **Timeout handling**: Auto-reject if no response within threshold (prevent hung workflows)

**Example flow**:

```
Agent: "I need to execute: DELETE FROM users WHERE inactive > 90"
[HITL INTERRUPT]
User sees: "⚠️ Destructive operation: DELETE 1,247 users where inactive > 90 days. Approve?"
User: [Approve]
Agent: Executes query with user's RBAC permissions
```

## Key Parameters

- **Risk classification threshold**: What operations trigger HITL (all writes? only deletes? transactions > $X?)
- **Intent detection mechanism**: LLM-based, rule-based, or hybrid
- **Approval timeout**: How long to wait before auto-rejecting (minutes, hours, indefinite)
- **Approval authority**: Who can approve (original user, admin, multi-party approval)
- **Action detail level**: How much context to show (full query, summary, affected entities)
- **Modification support**: Can user edit the action, or only approve/reject?
- **Bypass mechanisms**: Emergency override for approved users (requires separate audit trail)
- **Async vs blocking**: Does user session wait, or is approval handled asynchronously (Slack notification)?

## When To Use

Use HITL for:

- **Destructive data operations**: DELETE, UPDATE, DROP, TRUNCATE in SQL agents
- **Financial transactions**: Purchases, transfers, refunds above threshold
- **External communications**: Sending emails, Slack messages, API calls to external systems
- **Production deployments**: Code pushes, configuration changes, infrastructure updates
- **Access control changes**: Granting permissions, creating API keys, modifying security groups
- **Bulk operations**: Any action affecting > N records (e.g., > 100 rows)
- **Irreversible actions**: Operations that can't be undone (no backup/restore)
- **Compliance-sensitive operations**: Actions requiring documented approval trail
- **Learning phase**: New agent capabilities not yet trusted for autonomous execution

Critical for any AI system where mistakes have high cost or are difficult to reverse, even when RBAC limits blast radius.

## Risks & Pitfalls

**HITL fatigue**: Too many approval requests train users to auto-approve without reading — defeats the purpose. Tune thresholds carefully.

**False sense of security**: HITL doesn't replace RBAC; user can still approve actions they're authorized but shouldn't perform. HITL + RBAC together provide defense in depth.

**Workflow blocking**: Synchronous HITL blocks agent execution, potentially timing out downstream services. Consider async approval for long-running workflows.

**Poor UX**: Showing raw SQL or technical details to non-technical users leads to approval paralysis. Present action in business terms.

**Approval bypass incentive**: If HITL is too restrictive, users/developers create backdoors or workarounds, negating security benefits.

**Inconsistent application**: If only some code paths have HITL, attackers/bugs can route around checkpoints.

**Audit trail gaps**: If approval system isn't integrated with logging, can't prove who approved what in incident investigations.

**Timeout ambiguity**: What does timeout mean? Auto-reject (safe default) or auto-approve (dangerous)? Must be explicit.

**Multi-agent coordination**: If multiple agents need approval, workflow can deadlock; need orchestration strategy.

**Intent detection errors**: False positives (safe operations flagged) → HITL fatigue. False negatives (dangerous operations missed) → security gap.

## Related Concepts

- [[concepts/on-behalf-of-flow]] — HITL complements RBAC; OBO limits what user can approve
- [[concepts/zero-trust-agents]] — HITL is additional safeguard on top of permission scoping
- [[concepts/agent-isolation]] — Per-user agents ensure approvals are user-specific
- [[concepts/rbac-enforcement]] — HITL doesn't replace RBAC, augments it
- [[concepts/audit-trail]] — Approval decisions must be logged for compliance
- [[concepts/intent-classification]] — Detecting which operations need approval
- [[concepts/approval-workflows]] — General pattern HITL implements
- [[concepts/langgraph]] — Framework with built-in interrupt mechanism for HITL

## Sources

- Clippings/Securing A Multi-Agent AI Solution Focused on User Context & the Complexities of On-Behalf-Of.md — HITL for destructive SQL operations using LangGraph interrupts + LLM intent detection
