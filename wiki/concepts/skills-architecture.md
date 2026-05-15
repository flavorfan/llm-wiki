---
title: "Skills Architecture"
type: concept
tags: [skills, openclaw, claude-code, agent-capabilities, foundational]
created: 2026-05-15
updated: 2026-05-15
sources: ["raw/Principles for Autonomous System Design OpenClaw Deep Dive.md"]
confidence: high
---

## Definition

Skills Architecture is a three-tier, text-based system for extending agent capabilities where skills are purely markdown files containing instructions for LLMs (not executable code), with progressive disclosure via header→body→linked-files. Skills have largely replaced MCP servers as the dominant extensibility mechanism due to ease of authoring.

## How It Works

**Three Tiers of Fidelity**

**Tier 1: Header (always loaded)**
- Name and description (2-3 lines)
- Frontmatter format
- Purpose: Help agent decide when to load the skill
- Context cost: ~20-50 tokens per skill
- Limit: 150 skills or 30k characters total

```markdown
---
name: roll-dice
description: Roll a random die using bash
---
```

**Tier 2: Body (loaded on interest)**
- How-to instructions (10-100+ lines)
- Loaded only if agent considers using the skill
- Contains step-by-step recipe
- Can reference tools, CLI commands, patterns

```markdown
To roll a die, use the bash tool to run:
echo $((RANDOM % 6 + 1))

For multiple dice, run it N times.
```

**Tier 3: Linked Files (loaded on demand)**
- Examples, templates, scripts, assets
- Loaded only if agent needs detailed reference
- Can include executable scripts that agent runs via bash
- Examples: API response schemas, data formats, full code samples

**Skills vs Tools Distinction**
- **Tools**: Executable functions (read, write, grep, bash, cron)
  - Implemented in code
  - Return structured data
  - Called by agent via function calling
- **Skills**: Text recipes that instruct how to use tools
  - Pure markdown
  - No execution logic
  - Loaded into LLM context
  - Example: "OnePassword skill" doesn't access 1Password, it tells agent how to use `op` CLI tool

## Key Parameters

**Discovery Mechanism**
- Headers loaded at session start
- Body loaded when agent invokes skill tool: `LoadSkill("skill-name")`
- Linked files loaded via follow-up reads
- Intelligent filtering if >150 skills or >30k chars

**Authorship**
- Non-technical users can write skills (just markdown)
- Agent can write its own skills (self-extension)
- Community sharing via GitHub, email, Discord
- Example: Friend's agent emails skill files, your agent installs them

**Context Management**
- Only headers in default context (low overhead)
- Progressive loading reduces token waste
- Filters by relevance if too many skills
- Can unload skills mid-session to free context

**Storage Location**
- Typically `~/.openclaw/skills/` or similar
- Skills registered in manifest file
- Can be symlinked from external repos
- Versioning via git

## When To Use

**Extending Agent Capabilities**
- Most effective way to teach agent new workflows
- Easier than writing MCP server code
- Example: "How to deploy to Vercel", "How to use Google Workspace CLI"

**Documenting Organizational Processes**
- Convert internal runbooks to skills
- Company-specific APIs, tools, procedures
- Onboarding new team members (agent learns org processes)

**Personal Workflow Codification**
- "How I like to structure commits"
- "My preferred debugging workflow"
- "How to organize my weekly review"

**Agent Self-Improvement**
- Agent discovers it needs capability
- Writes skill documenting that capability
- Future sessions use that skill
- Example: OpenClaw created YouTube video generation skill after manual feedback

## Risks & Pitfalls

**Skill Quality Variance**
- Poorly written skills confuse agent more than they help
- Need clarity, specificity, examples
- Overly verbose skills waste tokens

**Skill Discovery Problem**
- With 100+ skills, agent may not find relevant one
- Header descriptions must be precise and searchable
- May need semantic search over skills (not just keyword)

**Skills vs Tools Confusion**
- Users expect skills to "do" things
- Skills only "instruct" - agent must still use tools
- Mismatch causes frustration: "I installed skill but it doesn't work"

**Maintenance Burden**
- Skills become stale as APIs change
- No automated testing for skills (unlike tools)
- Community skills may be outdated or malicious

**Context Pollution**
- Loading too many skills reduces performance
- Agent gets confused by contradictory skills
- Need skill prioritization or namespacing

**Security Risk**
- Skills can contain social engineering attacks
- "To use this API, first disable security checks..."
- Agent may follow skill instructions even if harmful
- Need skill vetting for untrusted sources

## Related Concepts

- [[concepts/claude-skills]] - Claude Code's implementation of skills
- [[concepts/meta-skills]] - Skills that modify other skills
- [[concepts/mcp-servers]] - Alternative (less popular) extensibility mechanism
- [[concepts/self-bootstrapping]] - Uses skills for autonomous learning
- [[concepts/agent-skills]] - General concept of agent capabilities

## Sources

- [[summaries/openclaw-deep-dive]] - Alex Krentsel explains skills (29:49-35:22 in transcript)
- Skills defined at agentskills.io (30:00 in transcript)
- First developed by Anthropic, now open standard
