---
title: "Activity Log"
type: log
---

# Activity Log

Append-only record of all wiki changes.

## Format

Each entry follows this format:
```
### YYYY-MM-DD HH:MM — [Action Type]
- **Source/Trigger**: what initiated the action
- **Pages created**: list of new pages
- **Pages updated**: list of updated pages
- **Notes**: any contradictions flagged, decisions made
```

---

### 2026-04-08 00:00 — Setup

- **Source/Trigger**: Repository initialized
- **Pages created**: index.md, log.md, dashboard.md, analytics.md, flashcards.md
- **Pages updated**: none
- **Notes**: Empty knowledge base ready for first source ingestion

---

### 2026-04-10 — Ingest | Three foundational sources on LLM knowledge bases

- **Source/Trigger**: Ingested raw/llm-wiki.md, raw/karpathy-x.md, raw/Claude + Karpathy's Second Brain is INSANE.md
- **Pages created**:
  - **Summaries (3)**: llm-wiki.md, karpathy-x.md, claude-karpathy-second-brain-video.md
  - **Concepts (14)**: llm-knowledge-base.md, second-brain.md, knowledge-compilation.md, ingest-workflow.md, query-workflow.md, lint-workflow.md, graph-view.md, obsidian-web-clipper.md, persistent-artifact.md, index-files.md, wiki-maintenance.md, rag.md, loop-automation.md, schema-file.md
  - **Entities (4)**: andrej-karpathy.md, obsidian.md, claude-code.md, openai.md
- **Pages updated**: index.md (added 21 pages), log.md (this entry)
- **Notes**:
  - All three sources describe the same underlying pattern from different perspectives: llm-wiki.md is the abstract "idea file," karpathy-x.md is the originator's personal workflow, and the video is a practical tutorial implementation
  - Core innovation: knowledge **compilation** (persistent, maintained wiki) vs. **retrieval** (RAG-style query-time search)
  - Key workflows established: ingest, query, lint
  - Three-layer architecture: raw sources (immutable) → wiki (LLM-maintained) → outputs (query results)
  - Obsidian serves as IDE frontend; Claude Code (or other AI harness) as maintenance agent
  - Works at moderate scale (~100 sources, ~400K words) without embedding-based RAG
  - All 17 pages have high confidence given clear, consistent descriptions across multiple sources
  - No contradictions found - sources are highly aligned
  - Foundation established for future ingestion of additional sources on this topic

---

### 2026-04-11 — Ingest | Three comprehensive analyses and practical guides

- **Source/Trigger**: Ingested raw/Andrej Karpathy's LLM Wiki  Bye Bye RAG.md, raw/LLM Wiki：让大模型替你打理知识库的完整指南.md, raw/What Is Andrej Karpathy's LLM Wiki How to Build a Personal Knowledge Base With Claude Code.md
- **Pages created**:
  - **Summaries (3)**: bye-bye-rag.md, chinese-comprehensive-guide.md, mindstudio-practical-guide.md
  - **Concepts (5)**: knowledge-graph.md, zettelkasten.md, hormesis.md, memex.md, idea-files.md
  - **Entities (8)**: notebooklm.md, chatgpt.md, niklas-luhmann.md, vannevar-bush.md, extended-brain.md, qmd.md, marp.md, mindstudio.md
- **Pages updated**: 
  - rag.md (added stateless vs stateful section, hormesis framework, updated with Bye Bye RAG source)
  - index.md (added 16 new pages to catalog)
  - log.md (this entry)
- **Notes**:
  - **Bye Bye RAG source** provides clear pedagogical comparison emphasizing stateless (RAG) vs stateful (LLM Wiki) distinction, using EV/Tesla example and compound interest analogy
  - **Chinese comprehensive guide** is deepest single source, adding:
    - **Historical context**: Memex (1945, Vannevar Bush) as conceptual ancestor
    - **Philosophical critique**: Zettelkasten (Niklas Luhmann) and hormesis concept from Extended Brain - argues LLM automation may remove beneficial cognitive friction
    - **Idea files paradigm**: Shift from sharing code to sharing concepts that agents customize
    - **Tool ecosystem**: qmd (local search), Marp (presentations), detailed implementation roadmap
    - **NotebookLM comparison**: "Library reading room" (session-based) vs "garden tended over years" (compounding)
  - **MindStudio guide** focuses on practical implementation: 5-minute setup, note templates, best practices for query efficiency, when NOT to use advanced features
  - **New conceptual depth**: Zettelkasten and hormesis introduce important counterpoint - automation of synthesis may aid information organization but could hinder deep learning/cognitive integration. Recommended hybrid: LLM builds map layer, human writes synthesis layer
  - **Historical framing strengthened**: Memex (1945) → Hypertext (1960s-80s) → WWW (1989+, lost private/curated vision) → LLM Wiki (2026, returns to private/curated but with automated maintenance)
  - **Product/tool landscape clarified**: ChatGPT and NotebookLM positioned as RAG systems with ephemeral experience; qmd and Marp as optional scaling tools; MindStudio as team-scale deployment path
  - No direct contradictions, but tension acknowledged between efficiency (LLM compilation) and understanding depth (manual Zettelkasten). Sources agree this is goal-dependent tradeoff, not absolute superiority
  - Wiki now spans: foundational pattern, practical implementation, philosophical critique, historical context, tool ecosystem, scaling considerations
  - Total corpus: 6 sources ingested (3 today + 3 previous)
  - Confidence levels: All new pages high confidence (well-documented across sources) except Extended Brain (medium - single reference), qmd (medium - brief mentions), MindStudio (medium - primarily from one promotional source)

---

### 2026-04-11 — Ingest | AutoResearch comprehensive tutorial

- **Source/Trigger**: Ingested raw/The only AutoResearch tutorial you'll ever need.md
- **Pages created**:
  - **Summaries (1)**: autoresearch-tutorial.md
  - **Concepts (9)**: auto-research.md, three-file-architecture.md, recursive-self-improvement.md, autonomous-agents.md, experiment-loop.md, metric-driven-optimization.md, git-based-rollback.md, fixed-time-budget.md, vibe-coding.md
  - **Entities (7)**: david-andre.md, puppeteer.md, cursor.md, eric-seu.md, harrison-chase.md, vs-code.md, oxylabs.md
- **Pages updated**:
  - andrej-karpathy.md (added AutoResearch framework creation, Tesla Autopilot role, "vibe coding" term invention, predictions about AI future)
  - claude-code.md (added AutoResearch implementation strategy, bypass/Yolo mode usage, autonomous experimentation capabilities)
  - index.md (added 18 new pages to catalog, updated 2 entity entries)
  - log.md (this entry)
- **Notes**:
  - **New domain**: First source outside pure LLM knowledge base pattern - introduces **AutoResearch** as autonomous AI experimentation framework
  - **Core innovation**: AI agents that autonomously run experiments, evaluate results, keep what works (git commit), discard what doesn't (git reset), operating on **three-file architecture** (program.md for goals, train.py for optimization target, prepare.py for evaluation metric)
  - **Key constraints**:
    - Fixed time budget per experiment (fair comparison, prevents "cheating by training longer")
    - One scalar metric (objective evaluation)
    - Immutable goal and eval files (prevents agent from gaming the system)
    - Git-based rollback (clean binary decision: commit success or reset failure)
  - **Karpathy connection**: AutoResearch is another Karpathy innovation alongside LLM Wiki - both represent shift toward AI autonomy (Wiki maintenance and experimental optimization)
  - **Broad applications**: Tutorial emphasizes AutoResearch extends far beyond ML training:
    - Trading strategies (Sharpe ratio optimization)
    - Marketing (A/B testing at 1,200x scale: 30 experiments/year → 36,000/year)
    - Code performance (website optimization: 50ms → 25ms in 4 minutes)
    - Prompt engineering (system instruction optimization)
    - Any domain with clear metric + automated evaluation + fast feedback
  - **Future predictions**:
    - All LLM frontier labs will use AutoResearch ("final boss battle")
    - Execution becomes "basically free" - value shifts to metric selection and constraint design
    - Mobile AI: Sonnet 4.6 quality on iPhones in 3-4 months
    - SETI@home model for AI research (distributed autonomous experimentation)
    - "We might be in the early stages of the singularity"
  - **New concept introduced**: **Recursive self-improvement** - AI improving itself autonomously, with each improvement enabling better improvements (though current AutoResearch is more "iterative improvement" than true recursion)
  - **Tool ecosystem**: Demonstrates Claude Code and Cursor in bypass/Yolo mode for autonomous operation, Puppeteer for web benchmarking, git for experiment management
  - **Where it fails**: Subjective metrics (UX, brand design, pricing), slow feedback loops, bad metric definition leads to confident wrong optimization
  - **Philosophical insight**: Not "better chatbots" but "real autonomous loops doing meaningful work" - represents evolution from conversational AI to task-driven agents
  - **Cross-domain synthesis opportunity**: AutoResearch (continuous optimization) + LLM Wiki (knowledge compilation) together represent shift toward autonomous AI systems that both maintain knowledge and improve performance without human intervention
  - **Confidence levels**:
    - High confidence (14 pages): Core AutoResearch concepts well-explained with concrete examples and demonstrations
    - Medium confidence (3 pages): cursor.md, eric-seu.md, harrison-chase.md (brief mentions, limited detail)
    - Low confidence (1 page): vibe-coding.md (term mentioned as Karpathy invention but not defined in source)
  - No contradictions with existing wiki content - AutoResearch complements LLM Wiki pattern rather than conflicting
  - Total corpus: 7 sources ingested
  - Wiki statistics: 55 total pages (28 concepts, 19 entities, 7 summaries, 0 syntheses)

---

### 2026-04-12 — Ingest | Obsidian CLI and Skills ecosystem

- **Source/Trigger**: Ingested raw/Obsidian CLI.md, raw/Obsidian 官方 CLI 命令全景速查表.md, raw/Obsidian 必装 Skills.md
- **Pages created**:
  - **Summaries (3)**: obsidian-cli-core-principles.md, obsidian-cli-command-reference.md, obsidian-essential-skills.md
  - **Concepts (6)**: obsidian-cli.md, agent-skills.md, token-optimization.md, defuddle.md, automation-workflows.md, obsidian-bases.md
  - **Entities (2)**: steph-ango.md, n8n.md
- **Pages updated**:
  - obsidian.md (added CLI feature, Bases feature, leadership info, privacy philosophy, updated sources)
  - claude-code.md (added Skills integration, CLI integration, token efficiency notes)
  - index.md (added 11 new pages to catalog, updated 2 entity entries, revised statistics)
  - log.md (this entry)
- **Notes**:
  - **Domain expansion**: First sources focused on **tooling layer** rather than pure LLM Wiki pattern - these cover the infrastructure (CLI, Skills) that enables LLM-Obsidian integration
  - **Obsidian CLI** (v1.12+): Official command-line interface that communicates with running Obsidian process rather than direct file I/O
  - **Key innovation - Token optimization**: CLI queries internal indices (~100 tokens) vs scanning entire vault (500,000+ tokens) - 99.98% reduction in token consumption
  - **Two paradigms identified**:
    - **Modern (CLI-based)**: Token-efficient, preserves graph integrity, auto-updates wikilinks (recommended)
    - **Legacy (file I/O)**: Token-intensive, risk of broken links and sync corruption (deprecated)
  - **Skills ecosystem**: Agent capabilities are packaged as Skills (SKILL.md files) with directory structure `.claude/skills/<skill-name>/`
  - **Official Skills** by [[entities/steph-ango]] (Obsidian CEO, kepano):
    - obsidian-cli: Wraps CLI commands for agents
    - obsidian-bases: Creates Notion-like database views with formulas
    - obsidian-markdown: Writes Obsidian-flavored Markdown
    - defuddle: Web scraping to clean Markdown, YouTube transcripts
    - json-canvas: Creates whiteboard files (now deprecated)
  - **Community Skills**:
    - Axton (axtonliu): canvas-creator, mermaid-visualizer, excalidraw-diagram
    - RoundTable02: tutor-setup + tutor (learning system with quizzes)
    - EESJGong: scholar-skill (L1-L3 academic paper reading, 2.5+ hour deep loops, $100+ token costs)
  - **Seven automation workflow patterns** documented:
    1. Flash capture (instant append to daily note)
    2. Media knowledge extraction (YouTube → structured notes)
    3. AI inbox sorting (batch categorization + metadata normalization)
    4. Local RAG assistant (search:context + backlinks, no vector DB needed)
    5. Database integration (external webhooks → Bases records)
    6. Historical revival (random old note → AI cross-links → daily reflection)
    7. Bulk metadata cleaning (normalize inconsistent YAML properties)
  - **Obsidian Bases**: New native database feature (v1.12+), creates dynamic views (table/cards/list/map) with filters and formulas over note properties
  - **Privacy philosophy clarified**: Obsidian team (CEO Steph Ango, co-founders Erica Xu & Shida Li) maintains strong local-first stance - will never force cloud AI, CLI as "open external interface"
  - **n8n integration**: Local workflow automation tool, requires `NODES_EXCLUDE=[]` to enable shell commands for Obsidian CLI access
  - **Installation methods**: BRAT (Beta Reviewers Auto-updater Tool) for auto-updating beta plugins, manual installation for offline scenarios
  - **Risk awareness**: Scholar-skill L3 mode can consume $100+ per paper with frontier models, uses deprecated file I/O approach (risk of data corruption during sync)
  - **Platform compatibility**: CLI works across Windows/Mac/Linux but requires running Obsidian process (not suitable for headless servers)
  - **Cross-wiki connections**: Token optimization concept bridges to existing [[concepts/rag]] - both address retrieval efficiency but via different mechanisms (CLI indices vs vector embeddings)
  - **Complementary to existing content**: These sources describe the **implementation layer** (how to actually integrate AI with Obsidian) while previous sources described the **pattern layer** (what LLM Wiki pattern is conceptually)
  - **No contradictions found**: Sources are internally consistent and align with established wiki content
  - **Confidence levels**: All 11 new pages high confidence (well-documented with concrete examples, command references, and multiple corroborating details)
  - Total corpus: 10 sources ingested (3 today + 7 previous)
  - Wiki statistics: 66 total pages (34 concepts, 21 entities, 10 summaries, 0 syntheses)
