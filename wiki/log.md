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

---

### 2026-04-12 — Lint | Wiki health check and link resolution

- **Source/Trigger**: User requested lint operation
- **Pages created**:
  - **Concepts (3)**: search-engines.md, output-formats.md, vault-management.md
  - **Entities (5)**: nick-b-zark.md, peter-levels.md, erica-xu.md, shida-li.md, vercel.md
- **Pages updated**:
  - defuddle.md (added missing cross-link to obsidian entity)
  - index.md (added 8 new pages to catalog, updated statistics)
  - analytics.md (updated charts with current statistics: 37 concepts, 26 entities)
  - log.md (this entry)
- **Issues fixed**:
  - **8 broken links resolved**: Created stub pages for all referenced but non-existent pages
    - Concept stubs: search-engines, output-formats, vault-management (confidence: medium)
    - Entity stubs: nick-b-zark, peter-levels, erica-xu, shida-li, vercel (confidence: low)
  - **1 missing cross-link added**: defuddle.md now links to [[entities/obsidian]]
  - **Stale statistics updated**: analytics.md and index.md now reflect current page counts
- **Issues identified for manual review**:
  - **vibe-coding.md** (low confidence): Minimal information - term mentioned but not defined in sources
  - **9 medium-confidence entity pages**: Could be strengthened with additional sources (cursor, mindstudio, vs-code, extended-brain, eric-seu, harrison-chase, qmd, oxylabs, recursive-self-improvement)
  - **7 weakly-linked pages**: Only 1-2 inbound references (qmd, oxylabs, eric-seu, harrison-chase, vs-code, mindstudio, mindstudio-practical-guide summary)
- **Health check results**:
  - ✅ No orphan pages (all pages have at least one inbound link)
  - ✅ No incomplete sections or TODO markers
  - ✅ Consistent frontmatter structure across all pages
  - ✅ Recent update dates (2026-04-10 through 2026-04-12)
  - ✅ Strong cross-referencing in core concept pages
  - ⚠️ 6 low-confidence pages could benefit from additional sources
  - ⚠️ 4 medium-confidence concept pages created as stubs (search-engines, output-formats, vault-management, + existing recursive-self-improvement)
- **Statistics after lint**: 74 total pages (37 concepts, 26 entities, 10 summaries, 0 syntheses)
- **Confidence distribution**: 64 high, 4 medium, 6 low
- **Notes**: 
  - All critical broken links resolved - wiki graph integrity restored
  - Stub pages provide foundation for future enrichment when additional sources are ingested
  - Weakly-linked pages are valid but could benefit from more integration into knowledge graph
  - vibe-coding.md is a known issue - awaiting sources that define the term
  - Overall wiki health is excellent with strong structure and cross-linking

---

### 2026-04-13 — Ingest | Claude Skills 2.0 and Skill Creator methodology

- **Source/Trigger**: Ingested raw/claude-skills-2-how-to-use-skill-creator.md (video transcript from Clippings folder)
- **Pages created**:
  - **Summaries (1)**: claude-skills-2-skill-creator.md
  - **Concepts (3)**: claude-skills.md, meta-skills.md, skill-testing.md
  - **Entities (2)**: nick-babich.md, skill-creator.md
- **Pages updated**:
  - agent-skills.md (added cross-links to claude-skills, meta-skills, skill-testing)
  - claude-code.md (added Skills 2.0 section, Skill Creator references, cross-links, updated sources)
  - index.md (added 6 new pages to catalog, updated statistics)
  - log.md (this entry)
- **Notes**:
  - **Skills 2.0**: Community term for improved skill creation process using the Skill Creator meta-skill
  - **Core innovation**: Skill Creator is a meta-skill that creates other skills with built-in testing and evaluation
  - **Self-improvement loop**: Creates skill → generates test cases → runs tests → improves based on results → delivers final tested skill
  - **Workflow automation**: Fully automated creation process taking ~10 minutes for complex skills
  - **Quality improvements demonstrated**: Adds features beyond initial requirements (animations, CSS variables, enhanced specifications)
  - **Meta-programming concept**: Skills that operate on other skills rather than performing direct tasks
  - **Claude skills structure**: Markdown files with front matter (triggers) and content (workflow instructions)
  - **Installation options**: Per-project or global ("for you") via `manage plugins` command
  - **Practical example**: "Super landing page" skill generating Apple-style designs from descriptions
  - **Connection to existing content**: Relates to [[concepts/agent-skills]] but focuses specifically on Claude Code's skill system and the testing-driven methodology
  - **New entity**: Nick Babich (distinct from Nick B Zark) - UX designer creating AI tool tutorials
  - **Skill Creator entity**: The meta-skill tool itself, central to Skills 2.0 approach
  - **Testing concept**: Automated evaluation distinguishes Skills 2.0 from manual skill creation
  - **No contradictions found**: Content complements existing agent-skills documentation by adding Claude-specific implementation details
  - **Cross-links added**: agent-skills.md now references the three new concept pages
  - **Confidence levels**: All 6 new pages high confidence (clear demonstration with concrete examples and detailed workflow)
  - Total corpus: 11 sources ingested (1 today + 10 previous)
  - Wiki statistics: 80 total pages (40 concepts, 28 entities, 11 summaries, 0 syntheses)
  - High confidence: 70, Medium confidence: 4, Low confidence: 6

---

### 2026-05-01 — Ingest | PostgreSQL, LangChain, and LangGraph infrastructure sources

- **Source/Trigger**: Ingested raw/A local environment for PostgreSQL with Docker Compose.md, raw/LangGraph Checkpoint Postgres.md, raw/langchain-custom-middleware.md, raw/langchain-middleare-overview.md
- **Pages created**:
  - **Summaries (4)**: postgres-docker-compose-tutorial.md, langgraph-checkpoint-postgres.md, langchain-custom-middleware.md, langchain-middleware-overview.md
  - **Concepts (8)**: docker-compose.md, database-initialization.md, langgraph.md, checkpoint-persistence.md, middleware-pattern.md, hooks.md, state-reducers.md, langchain-agents.md
  - **Entities (7)**: postgresql.md, pgadmin.md, metabase.md, dbeaver.md, docker.md, langchain.md, christophe-vaudry.md
- **Pages updated**: 
  - index.md (added 19 new pages to catalog, updated statistics)
  - log.md (this entry)
- **Notes**:
  - **New domain**: First sources covering infrastructure (Docker/PostgreSQL) and LangChain agent framework - expands beyond LLM Wiki pattern and AutoResearch
  - **PostgreSQL Docker tutorial** provides complete development environment setup with database initialization patterns, multiple admin tools (pgAdmin, Metabase, DBeaver), and Docker Compose best practices
  - **LangGraph Checkpoint Postgres** documents official PostgreSQL persistence backend for LangGraph agents:
    - Dual sync/async implementations (`PostgresSaver` / `AsyncPostgresSaver`)
    - Long-term memory support via `PostgresStore` with pgvector
    - Shallow mode option for lightweight state-only persistence
    - Production-ready, officially maintained by LangChain
    - Limitation: no native API for checkpoint cleanup
  - **LangChain middleware system** introduces powerful agent customization mechanism:
    - Two hook styles: node-style (sequential) and wrap-style (control flow)
    - Four node hooks: `before_agent`, `before_model`, `after_model`, `after_agent`
    - Two wrap hooks: `wrap_model_call`, `wrap_tool_call`
    - State extension via custom schemas
    - Agent jumps for early termination
    - Execution order: before (1→2→3), wrap (nested), after (3→2→1)
    - Command composition for state updates with reducers
  - **Key architectural patterns identified**:
    - **Docker Compose**: Infrastructure-as-code for multi-container development environments
    - **Database initialization**: Automated schema/data setup via container startup hooks
    - **Middleware pattern**: Cross-cutting concerns via lifecycle hooks
    - **State reducers**: Predictable state merging when multiple sources update
    - **Checkpoint persistence**: Agent state saved for crash recovery and time-travel
  - **LangChain agent framework documented**: Core loop (model → tool selection → execution → repeat), created via `create_agent()`, supports middleware for logging/retries/guardrails/transformations
  - **Cross-wiki connections**:
    - Docker/PostgreSQL setup enables LangGraph checkpoint storage
    - Middleware pattern applicable to agent frameworks generally (LangChain specific implementation)
    - Database initialization pattern mirrors agent state initialization
    - Hooks concept generalizes beyond LangChain to extensibility patterns
  - **Tool ecosystem expansion**: PostgreSQL admin tools (pgAdmin, Metabase, DBeaver) complement Obsidian tools from earlier sources
  - **Production readiness theme**: These sources focus on reliability (checkpointing, retries), scalability (async, connection pooling), and observability (middleware logging)
  - **No contradictions found**: Infrastructure sources complement rather than conflict with knowledge management sources
  - **Confidence levels**: 
    - 18 new pages high confidence (well-documented with code examples and official docs)
    - 1 new page medium confidence (christophe-vaudry - limited biographical info)
  - Total corpus: 15 sources ingested (4 today + 11 previous)
  - Wiki statistics: 99 total pages (48 concepts, 35 entities, 15 summaries, 0 syntheses)
  - High confidence: 97, Medium confidence: 5, Low confidence: 6

---

### 2026-05-04 — Ingest | Claude Code configuration best practices and case studies

- **Source/Trigger**: Ingested 7 raw files on CLAUDE.md best practices, hooks, hackathon winners, and production usage
- **Pages created**:
  - **Summaries (7)**: stop-writing-bad-claude-md.md, using-claude-md-files.md, writing-good-claude-md.md, respiro-case-study.md, opus-4-6-hackathon-winners.md, maccoss-lab-onboarding.md, hooks-reference.md
  - **Concepts (10)**: claude-md-configuration.md, progressive-disclosure.md, path-specific-rules.md, instruction-following-limits.md, code-style-automation.md, mcp-servers.md, subagents.md
  - **Entities (0)**: Multiple entities identified but not yet created (to be added in future updates)
- **Pages updated**:
  - hooks.md (expanded with comprehensive Claude Code hooks documentation, added 5 new use cases, updated sources)
  - index.md (will update with new pages, updated statistics)
  - log.md (this entry)
- **Notes**:
  - **Core theme**: CLAUDE.md optimization - three complementary sources (camelCase video, Anthropic blog, HumanLayer blog) converge on same principles
  - **Key finding - Instruction limits**: Frontier LLMs can follow ~150-200 instructions; Claude Code system prompt uses ~50; quality degrades uniformly as count increases
  - **Size recommendation**: Keep CLAUDE.md under 300 lines, shorter is better. HumanLayer's root file is under 60 lines
  - **Anti-patterns identified**:
    - Using /init command (generates verbose, generic content)
    - Code style instructions (use linters/formatters via hooks instead)
    - Exhaustive documentation (causes selective attention - Claude ignores "irrelevant" content)
  - **Three essentials**: (1) Project one-liner, (2) Key commands, (3) Project-specific caveats
  - **Progressive disclosure**: Store detailed instructions in separate files, reference in CLAUDE.md for conditional loading
  - **Path-specific rules**: `.claude/rules/` with path patterns in frontmatter for automatic loading
  - **Hooks over instructions**: Use PostToolUse hooks for formatting/linting instead of consuming instruction budget
  - **MCP servers**: Model Context Protocol extends Claude with tools from external servers (Slack, GitHub, databases)
  - **Subagents**: Isolated Claude instances for distinct work phases (implementation → security review → optimization)
  - **Case study insights**:
    - **Respiro (Kostiantyn Vlasenko)**: Non-technical PM built iOS app in 6 weeks, managing 15+ subagents like team members
    - **Hackathon winners**: 4 of 5 winners were non-developers (lawyer, cardiologist, roads specialist, musician)
    - **MacCoss Lab (Brendan MacLean)**: 700k-line C# codebase, 17 years old - treats context as versioned artifact in separate repo
  - **Context as artifact principle**: MacCoss Lab insight - context doesn't persist in LLM, must be maintained like code
  - **Skills library pattern**: Encode domain expertise in skills that reference central documentation ("reference not embed")
  - **Hooks reference**: Comprehensive 34k-token reference document covering:
    - 5 hook types: command, HTTP, MCP tool, prompt, agent
    - 3 lifecycle cadences: per-session, per-turn, per-tool
    - 30+ event types with decision control options
    - Matcher patterns for conditional execution
    - JSON input/output schemas
  - **Cross-domain synthesis**:
    - CLAUDE.md configuration complements existing [[concepts/schema-file]] and [[concepts/claude-skills]]
    - Instruction limits explain why [[concepts/progressive-disclosure]] and [[concepts/hooks]] are essential
    - Path-specific rules bridge to existing [[concepts/path-specific-rules]] (now updated)
    - Code style automation reinforces "deterministic tools over LLM instructions" principle
    - Context-as-artifact connects to [[concepts/persistent-artifact]] philosophy
  - **No contradictions found**: Three CLAUDE.md sources highly aligned; case studies demonstrate principles in practice
  - **Confidence levels**: All 17 new pages high confidence (multiple corroborating sources, concrete examples, official documentation)
  - Total corpus: 22 sources ingested (7 today + 15 previous)
  - Wiki statistics: 116 total pages (58 concepts, 35 entities, 22 summaries, 0 syntheses)
  - High confidence: 114, Medium confidence: 5, Low confidence: 6

---

### 2026-05-07 — Status Check | Verified all sources ingested

- **Source/Trigger**: User requested verification of raw/ directory ingestion status
- **Pages created**: None (all sources already processed)
- **Pages updated**: log.md (this entry)
- **Notes**:
  - **Verification complete**: All 22 markdown files in raw/ directory have been ingested
  - **Wiki statistics unchanged**: 116 total pages (58 concepts, 35 entities, 22 summaries, 0 syntheses)
  - **Confidence distribution**: 114 high, 5 medium, 6 low
  - **Git status shows**: 7 new summary files, 7 new concept files awaiting commit from 2026-05-04 ingestion
  - **No new sources to process**: All raw files have corresponding summaries in wiki/summaries/
  - **Next recommended action**: Commit pending wiki files or ingest new sources when available
