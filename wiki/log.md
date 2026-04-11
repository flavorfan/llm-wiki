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
