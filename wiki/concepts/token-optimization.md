---
title: "Token Optimization"
type: concept
tags: [token-efficiency, cost-optimization, ai-agents, obsidian, llm-agents]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian CLI.md"]
confidence: high
---

## Definition

Token optimization is the practice of minimizing the number of tokens consumed by AI agents when interacting with knowledge bases or external systems, typically by leveraging pre-built indices rather than scanning raw content.

## How It Works

**The Problem**: Traditional AI agent workflows scan entire files or directories to answer queries, converting all text to tokens and sending to LLM APIs. For a 1,000-note [[entities/obsidian]] vault (~500,000 words), finding backlinks to a single note might require:
- Reading all 1,000 files
- ~600,000+ tokens sent to API
- Cost: ~$3-15 per query (depending on model pricing)
- Time: 10-30 seconds processing

**The Solution**: Use [[concepts/obsidian-cli]] to query Obsidian's internal indices:
- Obsidian maintains pre-built graph of links, backlinks, tags
- CLI queries this index directly
- `obsidian backlinks file=Note` → ~100 tokens
- Cost: ~$0.01 per query
- Time: <1 second

**Comparison Table**:

| Dimension | Direct File Scan | CLI Index Query |
|-----------|-----------------|----------------|
| **Tokens** | 500,000+ | ~100 |
| **Cost** | $3-15 | $0.01 |
| **Time** | 10-30 seconds | <1 second |
| **State Awareness** | Text only | Graph, metadata, plugins |
| **Data Consistency** | Risk broken links | Auto-updates references |

## Key Strategies

**1. Index-First Architecture**: Store data in systems with query APIs (databases, search engines, Obsidian) rather than flat files.

**2. Lazy Loading**: Only read full content when actually needed. Start with metadata/summaries:
```bash
# Bad: Read all files first
for file in vault/*; do obsidian read file=$file; done

# Good: Query index, then read only relevant files
obsidian search query="AI agents" | while read file; do
  obsidian read file=$file
done
```

**3. Cached Context**: For repeated queries, maintain a working context rather than re-scanning:
- LLM Wiki pattern: Compile knowledge once → query compilation (not raw sources)
- Session state: Load relevant pages into chat context at session start

**4. Scoped Queries**: Use filters to narrow search space:
```bash
# Bad: Search entire vault
obsidian search query="API"

# Good: Search specific folder with file type filter
obsidian search query="API" folder="code" ext=md
```

**5. Structured Extraction**: Use CLI to extract specific fields rather than full file content:
```bash
# Bad: Read entire file (2,000+ tokens)
obsidian read file=Project

# Good: Extract just properties (50 tokens)
obsidian property:read name=status file=Project
obsidian property:read name=deadline file=Project
```

## When To Use

**High-value scenarios**:
- Large vaults (500+ notes, 200K+ words)
- Frequent queries (>10/day)
- Graph navigation (backlinks, related notes)
- Metadata operations (YAML properties, tags)
- Production workflows with budget constraints

**Low-value scenarios**:
- Small vaults (<50 notes)
- One-time operations
- Full-text analysis actually needed (summarization, deep reading)
- Systems without query APIs

## Risks & Pitfalls

**Over-Optimization**: Spending more time optimizing than you'd save in token costs. Rule of thumb: if optimization takes >1 hour to implement and you'll save <$10/month, skip it.

**Premature Optimization**: Building complex index systems before knowing actual usage patterns. Start simple, measure, then optimize bottlenecks.

**Index Staleness**: Pre-built indices can be out of sync with file content. Obsidian CLI solves this by querying live process, but custom index systems need refresh strategies.

**Capability Loss**: Some operations (full-text semantic search, cross-document synthesis) legitimately need full content. Don't sacrifice quality for token savings.

**Complexity Overhead**: CLI-based approach requires:
- Running Obsidian process (not suitable for servers)
- Learning CLI command syntax
- Handling errors when Obsidian not running

## Measurement

Track these metrics to quantify optimization impact:

**Token Consumption**:
```bash
# Before: scan vault manually, note token count
# After: CLI queries, compare token count
```

**Cost Savings**:
```
Monthly savings = (old_tokens - new_tokens) × queries_per_month × token_price
```

**Query Speed**:
```bash
time obsidian search query="test"
# vs
time find . -name "*.md" -exec grep -l "test" {} \;
```

## Related Concepts

- [[concepts/obsidian-cli]] — Primary tool for Obsidian token optimization
- [[concepts/agent-skills]] — Skills use CLI for token efficiency
- [[concepts/llm-knowledge-base]] — Pattern that benefits from optimization
- [[concepts/rag]] — RAG systems need token optimization at scale

## Sources

- [[summaries/obsidian-cli-core-principles]] — CLI architecture comparison
