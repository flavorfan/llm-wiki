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
