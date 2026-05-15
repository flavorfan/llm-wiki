---
title: "Heartbeat Monitoring"
type: concept
tags: [monitoring, autonomous-agents, openclaw, reliability, foundational]
created: 2026-05-15
updated: 2026-05-15
sources: ["raw/Principles for Autonomous System Design OpenClaw Deep Dive.md"]
confidence: high
---

## Definition

Heartbeat Monitoring is a periodic wake-up mechanism for autonomous agents where a special system session executes every N minutes (default 30) with instructions from heartbeat.md and history of past heartbeats, enabling unpredictable monitoring, intervention, and maintenance that can't be scheduled via cron.

## How It Works

**System Session**
- Special "heartbeat" session with elevated permissions
- Not triggered by user messages
- Fires on timer (default every 30 minutes, configurable)

**Execution Flow**
1. Timer expires (30 min since last heartbeat)
2. Gateway controller spawns heartbeat session
3. Injects heartbeat.md instructions as prompt
4. Includes history of previous N heartbeats (context)
5. Agent executes checks, decides if intervention needed
6. Can send inter-session messages to wake other sessions
7. Session completes, waits for next timer

**Heartbeat.md Instructions**
- Agent writes its own heartbeat.md over time
- Typical contents:
  - "Check if experiment X is still running"
  - "Verify website Y is responding"
  - "Review inbox for urgent messages"
  - "Check if any sessions need attention"

**Inter-Session Communication**
- Heartbeat discovers problem in session A
- Sends wake message to session A with diagnosis
- Session A receives message and fixes issue
- Next heartbeat confirms fix worked

## Key Parameters

**Heartbeat Interval**
- Default: 30 minutes
- Too frequent: Wasted LLM calls, increased cost
- Too infrequent: Delayed response to problems
- Trade-off: Responsiveness vs. efficiency
- Configurable in settings

**Context Window**
- Includes recent heartbeat history (prevents repeated checks)
- Typical: Last 5-10 heartbeats
- Enables learning: "I checked this 3 times, it's still broken, escalate to user"

**Failure Response**
- Heartbeat can't fix everything (may lack permissions)
- Escalation path: Send user notification via connector
- Can create new sessions to handle recovery

## When To Use

**Unpredictable Monitoring**
- Long-running jobs that might crash unexpectedly
- External service availability checks
- Email inbox monitoring for urgent messages

**Complementing Cron**
- Cron handles predictable ("9am daily report")
- Heartbeat handles unpredictable ("check if the job I started yesterday finished")
- Example: Agent starts training run, adds heartbeat instruction to monitor progress

**Health Checks**
- "Is my deployed website still up?"
- "Are all my scheduled cron jobs executing successfully?"
- "Do any sessions have errors that need attention?"

**Autonomous Recovery**
- Detect stuck sessions and restart them
- Retry failed API calls
- Clean up completed sessions

## Risks & Pitfalls

**Heartbeat Spam**
- If instructions are too broad, heartbeat does too much
- Every 30 minutes = 48 times/day = significant LLM cost
- Best practice: Keep heartbeat.md focused on truly important checks

**Instruction Drift**
- Agent adds monitoring tasks but never removes completed ones
- Heartbeat.md grows unbounded
- Need periodic cleanup: "Is this still relevant?"

**False Positives**
- Heartbeat thinks something is wrong, wakes session unnecessarily
- Causes confusion, wasted cycles
- Need confidence thresholds: "Only intervene if 90% sure there's a problem"

**Inter-Session Race Conditions**
- Heartbeat sends fix to session A
- User simultaneously sends different instruction to session A
- Conflicting commands, unpredictable behavior
- Need coordination protocol or lock mechanism

**30-Minute Blindness**
- Critical failures invisible for up to 30 minutes
- Not suitable for real-time monitoring (use external monitoring + webhook trigger instead)
- Or reduce interval (increases cost)

## Related Concepts

- [[concepts/cron-scheduling]] - Complementary mechanism for predictable scheduling
- [[concepts/sessions-as-processes]] - Heartbeat as special system session
- [[concepts/gateway-controller]] - Contains heartbeat scheduler
- [[concepts/autonomous-agents]] - Heartbeat contributes to sense of liveliness

## Sources

- [[summaries/openclaw-deep-dive]] - Alex Krentsel explains heartbeat magic (20:19-21:52 in transcript)
