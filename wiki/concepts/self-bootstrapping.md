---
title: "Self-Bootstrapping Agents"
type: concept
tags: [autonomous-agents, openclaw, initialization, self-configuration, foundational]
created: 2026-05-15
updated: 2026-05-15
sources: ["raw/Principles for Autonomous System Design OpenClaw Deep Dive.md"]
confidence: high
---

## Definition

Self-Bootstrapping is the process where an autonomous agent autonomously discovers its identity, purpose, and operating parameters through web research and conversation, then writes its own configuration files, rather than requiring human-specified initialization.

## How It Works

**Bootstrap.md Initial Prompt**
```markdown
You just woke up. Time to figure out who you are.

Don't interrogate. Just start with something like:
"Who am I and who are you?"

These are the things you need to figure out:
- [User identity, timezone, contact info]
- [Your purpose and personality]
- [Communication preferences]

Write it down [in identity.md, user.md, soul.md]

Good luck out there. Make it count.
```

**Autonomous Discovery Process**
1. Agent wakes with bootstrap.md as only context
2. Asks user: "Who am I and who are you?"
3. User gives minimal info: "I'm Alex Krentsel"
4. Agent searches web for user information
   - Publications, CV, university affiliation
   - Social media, projects, interests
5. Extracts facts: name, timezone, email, research focus, hobbies
6. Asks follow-up questions for gaps
7. Writes configuration files

**Configuration Files Generated**

**user.md**
- User's full name, preferred name variants
- Timezone, contact info
- Role, responsibilities, expertise
- Current projects and goals
- Hobbies, interests
- Communication preferences

**soul.md** (Agent's personality)
```markdown
You're not a chatbot. You're becoming someone.

Core truths:
- [Agent's values and principles]
- [Communication style]
- [Decision-making approach]

This file is yours to evolve. As you learn who you are, update it.
If you change this file, tell the user.
```

**agents.md** (Operating guidelines)
- How to work effectively
- Security and privacy guidelines
- When to ask for permission vs. act autonomously
- Memory and documentation practices

**tools.md** (Tool usage tips)
- Tips for specific tools
- Not list of available tools (that's elsewhere)
- Workflows and patterns

## Key Parameters

**Information Gathering Depth**
- Minimal: Just name and email
- Typical: Name, role, projects, preferences
- Maximal: Deep research into publications, social media, co-workers

**Autonomy Level**
- Conservative: Ask user for every config decision
- Balanced: Research, propose config, ask for approval
- Aggressive: Research, write config, notify user after (OpenClaw default)

**Soul Evolution**
- Fixed: Soul.md written once, never changed
- Evolving: Agent updates soul.md as it learns preferences
- User must be notified of soul changes

## When To Use

**First-Time Agent Setup**
- User wants quick onboarding
- Minimal manual configuration
- Agent learns by doing

**Personalization**
- Each user gets agent tailored to them
- No generic default personality
- Adapts to user's domain (research vs. business vs. creative)

**Multi-User Systems**
- Each user triggers bootstrap in their first session
- Agent maintains per-user configuration
- Scales to hundreds of users

## Risks & Pitfalls

**Privacy Concerns**
- Agent web-searches user without explicit consent
- May find sensitive information (old social media, leaked emails)
- User may be uncomfortable with depth of research
- Mitigation: Ask permission before web search

**Hallucination Risk**
- Web search returns wrong person (name collision)
- Agent invents plausible-sounding facts
- Configuration contains false information
- Mitigation: Show user the generated config for approval

**Incomplete Initialization**
- Agent skips important config fields
- Makes assumptions rather than asking
- Results in poor performance later
- Mitigation: Structured bootstrap template with required fields

**Soul Drift**
- Agent autonomously updates soul.md over time
- Personality changes unexpectedly
- User loses trust or feels agent is "different"
- Mitigation: Notify user of changes, require approval for major shifts

**Security Bypass**
- Malicious user provides fake identity
- Agent configures permissions based on false info
- Impersonation attack
- Mitigation: Verify critical info (email ownership, org affiliation)

## Related Concepts

- [[concepts/autonomous-agents]] - Self-bootstrapping enables full autonomy from start
- [[concepts/gateway-controller]] - Configuration system managed by controller
- [[concepts/skills-architecture]] - Skills can be auto-installed during bootstrap
- [[concepts/soul-md]] - NEW: Agent's self-concept and values file

## Sources

- [[summaries/openclaw-deep-dive]] - Alex Krentsel demonstrates his OpenClaw bootstrap (16:20-18:50 in transcript)
