---
title: "MindStudio Practical Guide: LLM Wiki Setup"
type: summary
tags: [implementation, tutorial, claude-code, obsidian, markdown, practical]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/What Is Andrej Karpathy's LLM Wiki How to Build a Personal Knowledge Base With Claude Code.md"]
confidence: high
---

# MindStudio Practical Guide: LLM Wiki Setup

## Key Points

- **Core distinction from traditional apps**: Traditional notes = human navigates manually; LLM wiki = describe needs in plain language, Claude synthesizes across entire corpus
- **Markdown is ideal**: Portable, future-proof, LLMs read it natively (trained on GitHub READMEs, docs), forces clarity, plain text = no lock-in
- **Claude Code advantage**: Reads local filesystem directly - no copy-pasting needed, just point it at wiki folder and ask questions
- **Note template importance**: Consistency makes wiki queryable - every note needs summary line and tags for Claude to quickly assess relevance
- **Organization philosophy**: Start simple (4-5 top-level folders), don't over-engineer, use `/inbox` for rough notes
- **Best practices that matter**:
  - One-line summary at top = Claude decides relevance without reading full file (10 seconds investment, huge query efficiency gain)
  - Consistent terminology across notes (pick "RAG" OR "retrieval augmented generation", not both)
  - Keep notes focused - 10 focused 1K-word notes beat one 10K-word catch-all
  - Link notes with `[[wiki links]]` - gives Claude richer graph to reason over
- **Semantic search is overkill initially**: Direct file-reading scales further than expected, add vector search (LlamaIndex, etc.) only when Claude struggles (hundreds of notes)

## 5-Minute Setup Steps

### 1. Install Obsidian and Create Vault
- Download from obsidian.md
- Create vault (just a folder) at `~/wiki` or `~/Documents/llm-wiki`
- "Vault" = folder, everything is plain markdown

### 2. Define Note Template
```markdown
# [Title]

**Summary**: One sentence describing this note.
**Tags**: #topic1 #topic2
**Created**: YYYY-MM-DDTHH:MM:SS+00:00
**Last Updated**: YYYY-MM-DDTHH:MM:SS+00:00

---

## Content
[Main content here]

## Related Notes
- [[Note Title]]
```

Key: Summary line and tags give Claude quick relevance signals without full read.

### 3. Organize Into Folders
```
wiki/
├── _templates/
├── projects/
├── research/
├── reference/
├── meetings/
└── inbox/    # Rough notes, Claude can help triage later
```

Don't overthink structure initially.

### 4. Write First Notes
- Migrate knowledge you look up repeatedly
- Start with 5-10 notes on most-referenced topics
- Don't bulk-import everything - wiki grows naturally as you add

### 5. Install Claude Code
```bash
npm install -g @anthropic-ai/claude-code
```
Authenticate with Anthropic account.

### 6. Query Your Wiki
```bash
cd ~/wiki
claude
```

Example queries:
- "What notes do I have about machine learning interpretability?"
- "Summarize everything in research folder related to RAG systems"
- "I'm writing a proposal on X — what relevant notes do I have?"
- "Find notes mentioning vendor Acme Corp and summarize key points"

Claude reads markdown files, identifies relevance, answers with citations.

## Best Practices Detail

### Write Summaries, Not Just Content
The one-line summary at top is surprisingly critical:
- Claude reads it to decide if full note is relevant
- Good summary = 10 seconds, saves model from reading irrelevant files
- Bad/missing summary = Claude must read everything or miss context

### Use Consistent Terminology
- "RAG" vs "retrieval augmented generation" - pick one
- Claude can connect variants, but cleaner results with consistency
- Add alias line if concept has multiple common names

### Link Notes to Each Other
- Obsidian's `[[wiki links]]` format creates connections
- Claude can follow links = richer graph than flat file collection
- More links = more paths for Claude to discover relationships

### Keep Notes Focused
- 10 specific 1K-word notes > 1 vague 10K-word note
- Easier for Claude to locate and apply precisely
- If note covers multiple distinct topics, split it

### Use /inbox Pattern for Capture
- Dump rough notes into `/inbox` without organizing
- Periodically ask Claude: "Look at inbox folder, suggest where each note should be filed and what tags it needs"
- Reduces friction of capture while maintaining eventual structure

## When to Add Semantic Search

**Wait until:**
- Wiki has hundreds of notes
- Direct file-reading struggles to find things you know exist
- Query performance degrades noticeably

**Then consider:**
- LlamaIndex for vector indexing over markdown
- Build search layer Claude queries before reading full files
- Most personal wikis never need this - direct reading scales surprisingly far

## Advanced: Team/Public Sharing via MindStudio

For beyond-local-machine needs:

**MindStudio platform:**
- No-code agent builder
- Wrap markdown wiki in queryable web interface
- Connect to Google Drive, Notion, or other storage
- Team members query through UI without touching Claude Code/terminal
- Tracks queries to see what people look for (gap analysis)
- Access to Claude, GPT, Gemini, 200+ models
- 1000+ pre-built integrations (Slack, email, project management)

**Use MindStudio when:**
- Building for team vs just yourself
- Need web UI vs terminal
- Want query logging and analytics
- Connecting wiki to other services (Slack, calendar, etc.)

**Stay with Claude Code direct when:**
- Solo user, local files
- Comfortable with terminal
- Maximum simplicity and control

## Comparison Tables

### Traditional Notes App vs LLM Wiki

| Dimension | Traditional Notes | LLM Wiki |
|-----------|------------------|----------|
| Navigation | Human remembers and browses | Describe needs, Claude finds & synthesizes |
| Structure | Folders, tags, manual organization | Natural language + links |
| Query | Search keywords, click through | Ask questions in plain English |
| Synthesis | Human reads multiple notes and connects | Claude reads, connects, cites sources |

### Claude Code Context Window

Claude 3.5 Sonnet supports ~200,000 tokens = tens of thousands of words in single session.

**Practical capacity**: Few hundred focused notes easily fits. Only need semantic search if wiki is very large or needs sub-second responses on huge corpus.

## FAQ Highlights

**Q: Is Obsidian required?**
A: No. Any markdown editor works (VS Code, Typora, iA Writer, Vim). Obsidian recommended for graph view, backlinks, plugins, but markdown is the actual format - editor is personal preference.

**Q: Can I use other AI models?**
A: Yes. Pattern works with any model that reads files. Claude Code is natural interface for local filesystem. GPT-4, Gemini, other agents can use same markdown wiki with similar frameworks.

**Q: How many notes can Claude Code handle at once?**
A: Claude 3.5 Sonnet's 200K token window = comfortable tens of thousands of words. Most personal wikis (few hundred focused notes) fit easily. Only very large corpora need semantic search pre-filtering.

## Relevant Concepts

- [[concepts/llm-knowledge-base]] - Overall pattern being implemented
- [[concepts/ingest-workflow]] - Migrating notes into wiki = ingest process
- [[concepts/query-workflow]] - Using Claude Code to query wiki
- [[concepts/index-files]] - Mentioned but less emphasized than in other sources
- [[concepts/second-brain]] - Contemporary term for same goal

## Relevant Entities

- [[entities/claude-code]] - Primary tool for querying wiki
- [[entities/obsidian]] - Recommended "IDE" for viewing/editing
- [[entities/andrej-karpathy]] - Original idea source
- [[entities/mindstudio]] (needs creation) - Platform for team-scale deployments

## Source Metadata

- **Type**: Tutorial / How-to guide
- **Author**: MindStudio Team
- **Published**: 2026-04-06
- **URL**: https://www.mindstudio.ai/blog/andrej-karpathy-llm-wiki-knowledge-base-claude-code
- **Target audience**: Beginners wanting to implement LLM wiki
- **Unique contributions**:
  - Concrete 5-minute setup steps
  - Emphasis on note templates and consistency
  - Best practices grounded in query efficiency
  - Clear guidance on when NOT to use advanced features (semantic search)
  - Integration path to team-scale via MindStudio platform
- **Relationship to other sources**: Practical implementation guide for concepts in [[summaries/llm-wiki]] and [[summaries/karpathy-x]]
- **Promotional element**: Includes MindStudio platform pitch for team use cases (legitimate extension but should be noted)
