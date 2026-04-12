---
title: "Agent Skills"
type: concept
tags: [ai-agents, claude-code, capabilities, skills, obsidian]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian CLI.md", "raw/Obsidian 必装 Skills.md"]
confidence: high
---

## Definition

Agent Skills are discrete capability packages that extend AI agents with domain-specific knowledge and tool usage patterns. In the context of [[entities/obsidian]] and [[entities/claude-code]], Skills are defined by `SKILL.md` files that provide instructions, examples, and constraints for how agents should interact with specific tools or workflows.

## How It Works

**File Structure**: Each Skill lives in its own directory with a `SKILL.md` manifest:
```
skills/
  skill-name/
    SKILL.md          # Main instruction file
    references/       # Supporting docs, schemas, examples
    assets/           # Templates, samples
```

**Agent-Specific Paths**:
- **Claude Code**: `.claude/skills/` in project root
- **OpenCode**: `~/.opencode/skills/`
- **Codex CLI**: `~/.codex/skills/`

**Activation**: When an agent encounters a task matching a Skill's trigger conditions (keywords, file types, user intent), it loads the SKILL.md into context and follows those instructions instead of improvising.

**Example Flow**:
1. User: "Read this article [URL] and summarize it"
2. Agent detects URL → matches [[concepts/defuddle]] Skill trigger
3. Loads defuddle SKILL.md into context
4. Executes: `defuddle [URL]` to get clean Markdown
5. Summarizes cleaned content (not raw HTML)

## Skill Categories

### Official Obsidian Skills (kepano)

Created by [[entities/steph-ango]], maintained at `kepano/obsidian-skills`:

- **obsidian-cli**: Wraps [[concepts/obsidian-cli]] commands with proper syntax and error handling
- **obsidian-bases**: Creates Notion-like database views (.base files) with filters/formulas
- **obsidian-markdown**: Writes Obsidian-flavored Markdown (wikilinks, callouts, embeds)
- **defuddle**: Web scraping to clean Markdown, YouTube transcript extraction
- **json-canvas**: Creates .canvas whiteboard files (deprecated - use enhanced versions)

### Community Skills

**Visualization** (axtonliu):
- **obsidian-canvas-creator**: Enhanced canvas with automatic layout algorithms (MindMap/freeform)
- **mermaid-visualizer**: Text → Mermaid diagrams with Obsidian-specific syntax fixes
- **excalidraw-diagram**: Text → hand-drawn Excalidraw diagrams with animation support

**Learning** (RoundTable02):
- **tutor-setup**: Converts documents/code → StudyVault with quizzes
- **tutor**: Interactive quiz system tracking knowledge gaps

**Research** (EESJGong):
- **scholar-skill**: L1-L3 tiered paper reading (2.5+ hour deep analysis loops)

### Legacy/Deprecated

- **obsidian-skill** (OpenClaw): Direct file I/O, high token cost, replaced by CLI-based approach

## Two Paradigms

**Modern (CLI-based)**:
- Uses [[concepts/obsidian-cli]] for all operations
- Token-efficient (~100 tokens per query)
- Preserves graph integrity (auto-updates wikilinks)
- Requires running Obsidian process
- **Recommended**

**Legacy (File I/O)**:
- Reads/writes Markdown files directly
- Extremely token-intensive (scans entire vault)
- Risk of broken wikilinks when moving files
- Risk of sync conflicts and data corruption
- **Deprecated** (but still used by scholar-skill due to historical reasons)

## Key Parameters

**Trigger Conditions**: Keywords, file types, user intent patterns that activate the Skill

**Dependencies**: External tools (Node.js, plugins, Python packages) required for Skill to function

**Token Budget**: Expected token consumption (critical for cost management)

**Risk Level**: Data safety considerations (read-only vs. destructive operations)

**Customizability**: Whether users should/can modify the Skill for personal workflows

## When To Use

**Create a new Skill when**:
- A workflow gets repeated frequently
- Domain-specific knowledge would help agent performance
- Complex tool syntax needs to be abstracted
- You want consistent behavior across sessions

**Use existing Skills when**:
- Task matches known Skill trigger (agent will auto-activate)
- You want proven, community-tested approaches
- Token optimization matters (CLI-based Skills)

## Risks & Pitfalls

**Token Bombs**: Some Skills (scholar-skill L3 mode) can consume $100+ in API costs for a single task. Always check token budget in Skill documentation.

**Data Corruption**: Legacy file I/O Skills can corrupt vaults during sync. Use git versioning and test in isolated vaults first.

**Dependency Hell**: Skills with complex dependencies (Python, multiple plugins) can break during updates. BRAT helps but doesn't solve everything.

**Overfitting**: Highly customized Skills may not transfer to other users or vaults.

**Obsolescence**: Skills may become outdated as tools evolve (e.g., json-canvas superseded by canvas-creator).

## Installation

**Via BRAT** (recommended for beta Skills):
1. Install BRAT plugin in Obsidian
2. Settings → BRAT → Add Beta plugin
3. Enter GitHub repo (e.g., `kepano/obsidian-skills`)
4. BRAT auto-updates on Obsidian restart

**Manual**:
1. Download Skill files from GitHub
2. Place in appropriate `skills/` directory
3. Restart agent or reload Skills

**Via Git Submodule** (for project-specific Skills in Claude Code):
```bash
cd .claude/skills
git submodule add https://github.com/user/skill-name
```

## Related Concepts

- [[concepts/obsidian-cli]] — Underlying tool that modern Skills use
- [[concepts/token-optimization]] — Why CLI-based Skills matter
- [[concepts/defuddle]] — Specific example of a Skill
- [[concepts/llm-knowledge-base]] — Pattern that Skills enable

## Sources

- [[summaries/obsidian-cli-core-principles]] — Integration architecture
- [[summaries/obsidian-essential-skills]] — Curated catalog and comparisons
