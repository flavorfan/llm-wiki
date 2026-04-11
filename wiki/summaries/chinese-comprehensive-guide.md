---
title: "LLM Wiki: Complete Guide (Chinese)"
type: summary
tags: [knowledge-synthesis, llm-wiki, comprehensive, critique, philosophy, history, implementation]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/LLM Wiki：让大模型替你打理知识库的完整指南.md"]
confidence: high
---

# LLM Wiki: Complete Guide (Chinese Comprehensive Analysis)

## Key Points

- **The core problem**: Humans abandon knowledge systems not due to lack of will but because **maintenance cost grows exponentially** - updating cross-references, reconciling contradictions, syncing old data
- **RAG's fatal flaw**: "阅后即焚" (read-then-burn/ephemeral) - no accumulation, knowledge doesn't grow with queries
- **Karpathy's insight**: "Don't optimize retrieval; write better documents from the source"
- **Three-layer architecture**: Raw (immutable sources) → Wiki (LLM-generated) → Schema (control protocol)
- **IDE analogy**: "Obsidian is your IDE, LLM is your programmer, markdown wiki is the codebase you co-maintain"
- **Two index files**: index.md (spatial dimension - catalog) + log.md (temporal dimension - timeline)
- **Idea files paradigm**: Share ideas not code - in LLM agent era, sharing concepts for agents to customize beats sharing rigid implementations
- **NotebookLM comparison**: "Well-equipped library reading room" (session-based) vs "garden tended year after year" (compounding)
- **Data sovereignty**: Local markdown files = you own it forever vs cloud storage with vendor lock-in

## Critical Perspective: Zettelkasten and Cognitive Friction

The deepest critique comes via Extended Brain's comparison to Niklas Luhmann's **Zettelkasten** (card-box method):

**Similarity surface-level:**
- Both separate raw sources from processed knowledge
- Both value connections over content
- Both designed for compound growth

**Fundamental difference:**
- **Luhmann**: Writing in your own words *is* thinking - friction of translation exposes understanding gaps
- **LLM Wiki**: LLM writes smooth syntheses - no struggle, no cognitive integration

**Hormesis concept**: Like muscles needing stress to grow, ideas need the "hormetic" struggle of being expressed in your own words. When your sentence collapses mid-writing because you realize you don't actually understand the concept - **that collapse is the valuable moment**.

**Mixed approach recommended:**
- Use LLM for map layer: interconnection graph, gap detection, index maintenance
- Keep synthesis layer for yourself: write your own arguments, struggle with connections
- Let LLM find inconsistencies but DON'T auto-resolve them - tension itself is valuable
- Wiki becomes quality INPUT to your thinking, not OUTPUT of it - scaffold, not building

## Historical Context: Memex (1945)

Vannevar Bush's 1945 vision in "As We May Think":
- Proposed "Memex" - desktop device storing all books/records/communications
- Fast search + "associative trails" (linked sequences with annotations)
- Core insight: Human thinking operates by association, not alphabetically
- Inspired Engelbart (mouse), Ted Nelson (hypertext 1965), Tim Berners-Lee (WWW 1989)
- But WWW became public/chaotic vs Bush's private/curated vision

**LLM Wiki is closer to original Memex vision**: private, curated, connections as valuable as content.

**The missing piece Bush couldn't solve**: Who does maintenance? Humans quit because burden grows faster than value. **LLM solves this** - never bores, never forgets cross-references, can touch 15 files in one operation.

## Three-Layer Architecture Detail

### Layer 1: Raw Sources (Immutable)
- "Source of truth" - never modified by LLM, only read
- Articles, papers, images, datasets, code repos, meeting notes
- Critical for verification - if LLM makes wiki error, trace back to source

### Layer 2: The Wiki (LLM Domain)
- Summaries, entity pages, concept pages, comparisons, overview, synthesis
- LLM has absolute control - creates/updates/maintains
- You read it; LLM writes it

### Layer 3: The Schema (Control Protocol)
- Configuration document (CLAUDE.md, AGENTS.md) defining structure, tags, workflows
- "Switch that turns chatbot into disciplined knowledge librarian"
- Without it: every new session starts from zero, no consistency
- With it: LLM maintains standards across sessions
- Co-evolves with usage - refine as you discover what works

## Operations Deep Dive

### Ingest (Compile Once, Maintain Forever)
One source ingestion may trigger **联动更新** (cascading updates) across 10-15 pages:
1. Read source completely
2. Create/update summary in wiki/sources/
3. Update relevant concept pages
4. Update relevant entity pages
5. Create new pages for new concepts/entities
6. Add bidirectional links everywhere
7. Update index.md
8. Append to log.md
9. Flag contradictions with existing content

Karpathy prefers one-at-a-time with full involvement, but batch is possible.

### Query (Answers That Add Up)
1. LLM searches index.md for relevant pages
2. Reads full pages
3. Synthesizes answer with citations
4. **Critical step**: File good answers BACK into wiki as new pages
   - Comparison tables → wiki/comparisons/
   - Analysis → wiki/syntheses/
   - New insights → appropriate section
5. This creates **复利循环** (compound loop): sources → wiki → queries → new pages → richer wiki

### Lint (Automated Health Check)
LLM as "tireless operations engineer":
- Detect contradictions between pages
- Find orphan pages (no inbound links)
- List frequently-mentioned concepts lacking own page
- Flag stale conclusions superseded by new sources
- Suggest investigation directions and sources to seek

## Tool Chain

| Tool | Role | Necessity |
|------|------|-----------|
| Obsidian | "Frontend IDE" for browsing wiki | Recommended (any markdown editor works) |
| Obsidian Web Clipper | One-click article → markdown | Recommended for fast capture |
| LLM Agent (Claude Code/Codex) | Wiki maintainer and query interface | **Required** |
| qmd | Local markdown search (BM25 + vector + LLM rerank) | Optional (for large scale) |
| Marp | Generate slides from wiki | Optional |
| Dataview | Query frontmatter → dynamic tables | Optional |
| Git | Version control | Recommended |

**Practical tips:**
- Web Clipper: Browser extension for Chrome/Firefox/Safari, saves to raw/
- Local images: Obsidian setting → attachments to raw/assets/, hotkey (Ctrl+Shift+D) downloads all images
- Graph View: Best way to see wiki shape - hubs, islands, clusters
- Git: Free version history, branches, `git diff` shows ingest changes, `git revert` for bad compiles

**qmd (when scale grows)**: Local markdown search engine by Tobi Lutke (Shopify CEO), combines BM25 full-text + vector semantic + LLM reranking, CLI and MCP Server interfaces.

## Community Reactions

**Enterprise angle**: "Every company has a raw/ directory drowning in unstructured data - Slack logs, internal wikis, PDF reports. No one has time to synthesize. A Karpathy-style enterprise layer would compile a living 'company knowledge bible.'"

**Product attempts**: "Claudeopedia" - weekend project implementing idea file, added /wiki skill for screenshots/downloads, interactive viz with time-range comparison, scheduled tasks for auto-reconciliation with notes and emails.

**Scale challenges**: "Leap from personal research wiki to enterprise ops is the real challenge - thousands of employees, millions of records, contradictory tribal knowledge."

## Comparison Tables

### Wiki vs RAG

| Dimension | RAG | LLM Wiki |
|-----------|-----|----------|
| Processing timing | Query-time (every question) | Ingest-time (once per source) |
| Cross-references | Discovered temporarily per query | Pre-built and maintained |
| Contradiction detection | Might go completely unnoticed | Actively flagged at ingest |
| Knowledge accumulation | None - starts fresh each time | Compound growth - every source/query enriches |
| Output format | Chat replies (ephemeral) | Persistent markdown files (reusable) |
| Maintainer | System black box | LLM (transparent, editable, traceable) |
| Human role | Upload files + ask questions | Curate sources, direct research, ask key questions |

### NotebookLM vs LLM Wiki

| Dimension | NotebookLM | LLM Wiki |
|-----------|------------|----------|
| Metaphor | Library reading room | Garden tended over years |
| Durability | Session resets when you leave | Living system, remembers everything |
| Source updates | Static unless manually replaced | Incremental updates to wiki |
| Autonomous evolution | None - waits for requests | Lint checks, gap detection, self-improvement |
| Data sovereignty | Google cloud, Google terms | Local markdown, full ownership |
| Longevity | Session productivity | Decades-long knowledge infrastructure |

**Key quote**: "Both have value, but only one compounds."

## Implementation Roadmap (0→1)

### Step 1: Directory Structure
```bash
mkdir -p my-wiki/{raw/{articles,papers,assets},wiki/{concepts,entities,sources,comparisons}}
touch my-wiki/wiki/{index,log,overview}.md
cd my-wiki && git init
```

### Step 2: Create Schema File
Create `CLAUDE.md` (or agent-specific config) defining structure, tags, page formats, ingest/query/lint workflows.

### Step 3: Configure Obsidian
1. Install Obsidian, open project folder as Vault
2. Install Web Clipper browser extension
3. Set attachment path → raw/assets/
4. Bind image download hotkey
5. Optional: Marp, Dataview plugins

### Step 4: First Ingest
1. Web Clipper saves article to raw/articles/
2. Tell LLM Agent: "ingest raw/articles/[filename].md"
3. Review summary, guide emphasis, confirm wiki updates
4. Browse in Obsidian, check Graph View
5. `git commit -m "ingest: [article title]"`

### Step 5: 10-Source Test
Start with 10 sources on one topic. After ingesting all, ask a question requiring multi-source synthesis. If the structured wiki yields insights you wouldn't get reading sources individually, **the system is working**. Expand from there.

### Step 6: Continuous Evolution
- Keep ingesting (10-20 sources → start querying; 50+ → consider qmd)
- Weekly lint health checks
- Continuously update schema
- Find rhythm between LLM automation and personal synthesis

## Relevant Concepts

- [[concepts/rag]] - Contrasted as stateless, non-accumulating approach
- [[concepts/knowledge-compilation]] - Core wiki philosophy
- [[concepts/schema-file]] - Layer 3 of architecture
- [[concepts/index-files]] - Spatial navigation mechanism
- [[concepts/wiki-maintenance]] - Why automation matters
- [[concepts/zettelkasten]] (needs creation) - The cognitive friction critique
- [[concepts/hormesis]] (needs creation) - Beneficial struggle concept
- [[concepts/memex]] (needs creation) - 1945 historical precursor
- [[concepts/idea-files]] (needs creation) - New sharing paradigm
- [[concepts/knowledge-graph]] - Emerges from cross-linking

## Relevant Entities

- [[entities/andrej-karpathy]] - Original idea author
- [[entities/obsidian]] - Recommended IDE
- [[entities/claude-code]] - Example LLM agent
- [[entities/notebooklm]] - Compared as session-oriented alternative
- [[entities/niklas-luhmann]] (needs creation) - Zettelkasten inventor
- [[entities/vannevar-bush]] (needs creation) - Memex visionary
- [[entities/qmd]] (needs creation) - Local markdown search tool
- [[entities/marp]] (needs creation) - Slide generation tool
- [[entities/extended-brain]] (needs creation) - Critical analysis author

## Source Metadata

- **Type**: Comprehensive analysis article (Chinese)
- **Author**: lizhongxuan
- **Published**: 2026-04-07
- **URL**: https://juejin.cn/post/7625563529491726378
- **Description**: Complete synthesis of Karpathy's original, community discussion, multiple critiques, historical context, implementation guide
- **Unique contributions**: 
  - Zettelkasten/Hormesis philosophical critique
  - Memex historical framing
  - Idea files paradigm explanation
  - NotebookLM comparison
  - Chinese community perspective
  - Enterprise considerations
- **Depth**: Most comprehensive single source on LLM Wiki concept and implications
