---
title: "Cron Scheduling for Agents"
type: concept
tags: [automation, time-management, openclaw, autonomous-agents, foundational]
created: 2026-05-15
updated: 2026-05-15
sources: ["raw/Principles for Autonomous System Design OpenClaw Deep Dive.md"]
confidence: high
---

## Definition

Cron Scheduling for Agents is the practice of giving autonomous agents direct access to schedule recurring or one-time tasks using cron syntax, enabling them to interact with the dimension of time by autonomously planning future work without staying continuously active.

## How It Works

**Traditional Cron**
- Unix/Linux utility for scheduled task execution
- Syntax: minute, hour, day-of-month, month, day-of-week
- Examples: `0 9 * * *` (9am daily), `0 9 * * 1-5` (9am weekdays), `0 0 1 * *` (midnight first of month)
- Avoids inefficient polling loops that waste CPU

**Agent-Accessible Cron**
- Expose cron as tool the agent can call
- Agent analyzes task requirements and autonomously creates schedule
- Can set both recurring and one-time schedules
- Example workflow: "Send me paper summary at 9am daily"
  1. Agent writes task description
  2. Creates dedicated session for task
  3. Schedules cron job: `55 8 * * *` (8:55am to finish by 9am)
  4. Cron fires daily, spawns session, executes task

**What Makes It Magical**
- Agents gain temporal autonomy (plan ahead without human scheduling)
- Enables predictable, time-sensitive workflows
- Complements heartbeat for unpredictable monitoring
- Agent can modify/cancel its own scheduled tasks

## Key Parameters

**Time Granularity**
- Typical minimum: 1 minute intervals
- Practical minimum: ~5-10 minutes (allow task completion)
- Common patterns: Daily summaries, weekly reports, hourly checks

**Task Specification**
- Must describe: What to do, when to do it, where to store results
- Can include: Session to wake, tools to use, success criteria
- Agent writes task description in natural language or structured format

**Cron Tool Interface**
- Minimal: Schedule(time, prompt) → creates cron job with that prompt
- Advanced: Schedule(time, session_id, task_json, repeat_rule)
- Cancel: StopCron(job_id)
- List: ListCron() → show all scheduled jobs

**Coordination with Heartbeat**
- Cron: Predictable ("every day at 9am")
- Heartbeat: Unpredictable ("check if process finished")
- Together: Complete time management ("I'll schedule the daily report, and heartbeat will check if the long-running experiment crashed")

## When To Use

**Scheduled Reporting**
- Daily paper summaries at specific time
- Weekly progress reports
- Monthly analytics digests

**Recurring Maintenance**
- Nightly backups
- Hourly health checks
- Daily inbox triage

**Deadline-Based Work**
- "Remind me 2 hours before meeting"
- "Start deploy at 2am when traffic is low"
- "Send birthday message on specific date"

**Coordinated Workflows**
- Sequential tasks across days ("scrape data at 8am, analyze at 9am, report at 10am")
- Multi-stage pipelines with delays ("train model, wait 2 hours, evaluate, wait 1 hour, deploy")

## Risks & Pitfalls

**Cron Job Sprawl**
- Agents create many jobs over time
- Forgotten jobs keep running
- Need garbage collection or expiration policy

**Time Zone Confusion**
- User's time zone vs. server time zone vs. UTC
- Daylight saving time transitions
- Best practice: Store user TZ in user.md, agent converts

**Task Drift**
- "Send paper summary at 9am" may take 20 minutes
- Next day's task overlaps with previous
- Solution: Agent should schedule at 8:55am with 5-min buffer, or enforce task completion

**Failed Task Accumulation**
- Cron fires but task fails (API down, out of credits, etc.)
- Should it retry? Skip? Notify?
- Need failure handling policy

**Cron Syntax Complexity**
- Agents may generate invalid cron expressions
- Edge cases: "last Friday of month", "every other Tuesday"
- Validation layer helps prevent malformed schedules

## Related Concepts

- [[concepts/heartbeat-monitoring]] - Complementary mechanism for unpredictable monitoring
- [[concepts/gateway-controller]] - Contains cron manager component
- [[concepts/loop-automation]] - Claude Code's scheduled loop execution
- [[concepts/autonomous-agents]] - Cron enables temporal autonomy

## Sources

- [[summaries/openclaw-deep-dive]] - Alex Krentsel explains cron magic (21:52-24:39 in transcript)
