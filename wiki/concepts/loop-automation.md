---
title: "Loop Automation"
type: concept
tags: [automation, claude, workflow]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# Loop Automation

## Definition

Loop automation (via Claude Code's `/loop` command or similar mechanisms in other AI harnesses) allows an AI agent to execute a prompt or skill on a recurring interval. In the [[concepts/second-brain]] context, this enables automatic ingestion of accumulated raw sources without manual triggering - the agent runs `ingest` every few hours, processing any new content that's appeared.

## How It Works

**Basic loop operation:**

```bash
/loop [interval] [command]
# Example: /loop 3h second-brain ingest
```

1. **Setup**: Configure loop with interval (e.g., 3 hours, 24 hours, weekly)
2. **Command**: Specify what to run (skill, prompt, or command)
3. **Execution**: Agent runs command on schedule while session active
4. **Monitoring**: Can check status, view output, stop loop as needed

**Second brain integration:**

- **Continuous capture**: Drop files into `raw/` throughout day (web clipper, mobile notes, transcripts)
- **Scheduled processing**: Loop runs ingest every N hours
- **Automatic organization**: When you return to desktop, new content already integrated into wiki
- **Low friction**: No manual "now ingest" step, happens in background

**Practical scenarios:**

- **Mobile workflow**: Record voice note on phone → saves to synced Obsidian vault → desktop loop ingests automatically
- **Meeting transcripts**: Zoom auto-saves transcripts to `raw/` → loop processes them
- **RSS/newsletter**: Automated scraping to `raw/` → loop ingests
- **Research sessions**: Clip many articles throughout week → loop processes overnight

## Key Parameters

- **Interval**: How often to run (minutes, hours, days)
  - Too frequent: Unnecessary processing of empty `raw/`
  - Too infrequent: Delays in availability of new knowledge

- **Command**: What to execute
  - `ingest`: Process new raw sources
  - `lint`: Health check wiki
  - Custom queries or reports

- **Session lifetime**: Loops run only while AI session active
  - Desktop runs: Keep terminal/app open
  - Server deployment: Run as persistent service

- **Resource usage**: Balance between responsiveness and compute cost

## When To Use

**Ideal for loop automation:**

- **Regular capture patterns**: You add content to `raw/` predictably (daily, weekly)
- **High-volume scenarios**: Many small sources accumulate quickly (tweets, notes, clips)
- **Team collaboration**: Multiple people adding to shared knowledge base
- **Real-time needs**: Want new information available ASAP without manual triggering
- **Habit building**: Makes knowledge base maintenance completely automatic

**Skip loop automation when:**

- Ingest infrequently (weekly or less) - manual triggering is fine
- Sources are large and need careful review before ingestion
- Want to guide LLM on what to emphasize per source (interactive mode better)
- Session can't stay open (mobile-only, intermittent use)

## Risks & Pitfalls

- **Runaway processing**: If sources accumulate faster than ingestion, loop may never finish
- **Quality degradation**: Automatic batch processing may miss nuance vs. interactive
- **Session dependency**: Loops stop when session ends; not truly persistent
- **Error accumulation**: Issues in automatic ingestion can compound before noticed
- **Resource waste**: Running loop when `raw/` is empty wastes compute
- **Synchronization issues**: If multiple agents/loops run, may conflict

**Mitigation strategies:**

- Start with longer intervals (6-24 hours) and tune based on usage
- Monitor logs to catch ingestion errors early
- Use interactive ingestion for high-value sources
- Consider proper automation infrastructure (cron, services) for production use

## Related Concepts

- [[concepts/ingest-workflow]] — What loop automation typically executes
- [[concepts/second-brain]] — Primary use case for automated ingestion
- [[concepts/llm-knowledge-base]] — System that benefits from continuous updates
- [[entities/claude-code]] — Provides loop functionality

## Sources

- [[summaries/claude-karpathy-second-brain-video]] — Loop automation demonstration and use cases
