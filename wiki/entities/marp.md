---
title: "Marp"
type: entity
tags: [tools, presentations, markdown, obsidian]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/LLM Wiki：让大模型替你打理知识库的完整指南.md", "raw/karpathy-x.md"]
confidence: high
---

# Marp

## Overview

Marp (Markdown Presentation Ecosystem) is an open-source tool that converts markdown files into presentation slides. In the LLM Wiki context, Marp enables generating slide decks directly from wiki content, allowing knowledge to be shared in presentation format without leaving the markdown ecosystem. LLM agents can write Marp-formatted markdown files that render as professional presentations.

## Characteristics

- **Format**: Markdown with special slide delimiters and directives
- **Output**: HTML slides, PDF, PowerPoint
- **Integration**: Obsidian plugin available, VS Code extension, standalone CLI
- **Philosophy**: Keep presentations as text files, version controllable, LLM-writable
- **Use in LLM Wiki**: Output format for query results that benefit from slide structure

## How It Works

### Marp Markdown Syntax

```markdown
---
marp: true
theme: default
---

# Title Slide

Content of first slide

---

## Second Slide

- Bullet points
- More content

---

# etc.
```

**Key features:**
- Triple-dash `---` creates new slide
- Frontmatter sets theme and options
- Standard markdown syntax for content
- Directives for slide-specific styling

## Common Strategies in LLM Wiki

**Query workflow integration:**
1. User asks question best answered as presentation (e.g., "Compare the three approaches")
2. LLM writes answer in Marp format: `wiki/presentations/comparison.md`
3. User opens in Obsidian with Marp plugin or exports to PDF/HTML
4. Presentation is now **part of the wiki** - can be updated, linked, versioned

**Advantages:**
- Presentations live alongside other wiki content
- Version controlled via git
- LLM can write slide decks as easily as regular pages
- No separate "presentation mode" tool needed
- Can extract slides back to regular pages if useful

## When To Use

**Create Marp presentations for:**
- Comparisons and decision frameworks (table format works well)
- Step-by-step processes (one slide per step)
- Overviews and syntheses (narrative arc benefits from slide structure)
- Sharing wiki content with non-wiki-users (slides are familiar format)
- Visual thinking - laying out concepts spatially

**Regular wiki pages better for:**
- Reference material (needs searchability not narrative)
- Detailed documentation (too much text for slides)
- Interconnected concepts (wiki links more important than linear flow)

## Related Entities

- [[entities/andrej-karpathy]] - Mentioned Marp as output format in original LLM wiki description
- [[entities/obsidian]] - Marp plugin integrates with Obsidian for viewing/exporting
- [[entities/claude-code]] - Can write Marp markdown when asked for presentation output

## Related Concepts

- [[concepts/query-workflow]] - Marp as optional output format for query results
- [[concepts/llm-knowledge-base]] - Presentations as first-class wiki artifacts
- [[concepts/persistent-artifact]] - Slides filed back into wiki become persistent
- [[concepts/idea-files]] - Marp decks can themselves be idea files

## Integration with Wiki Workflow

**Directory structure:**
```
wiki/
  presentations/
    comparison-approaches.md  # Marp format
    overview-llm-wiki.md      # Marp format
```

**Workflow:**
1. Ask LLM to create presentation: "Make a slide deck comparing RAG vs LLM Wiki"
2. LLM writes `wiki/presentations/rag-vs-wiki.md` in Marp format
3. View in Obsidian or export: `marp wiki/presentations/rag-vs-wiki.md -o output.pdf`
4. Update wiki/log.md noting new presentation created
5. Add entry to wiki/index.md under "Presentations" section

**Result**: Presentations are versioned, searchable, maintainable artifacts, not ephemeral PowerPoint files.

## Limitations

- **Linear format**: Slides force linear narrative, wiki is non-linear network
- **Limited cross-linking**: Can link to other wiki pages but presentation flow discourages deep linking
- **Visual simplicity**: Marp is clean but limited compared to Keynote/PowerPoint advanced features
- **Export quirks**: Rendering can vary between Marp implementations

## Comparison to Traditional Presentation Tools

| Dimension | Marp | PowerPoint/Keynote | Google Slides |
|-----------|------|-------------------|---------------|
| Format | Plain markdown | Binary file | Cloud document |
| Version control | Git-native | Difficult | Version history |
| LLM writable | Yes, trivially | No | No |
| Wiki integration | Native | Export/embed | Export/embed |
| Visual power | Basic | Advanced | Moderate |
| Collaboration | Text-based merge | Binary conflicts | Real-time |

**Marp tradeoff**: Less visual sophistication for more integrability with text-based knowledge systems.

## Sources

- [[summaries/chinese-comprehensive-guide]] - Tool chain section lists Marp as optional output format
- [[summaries/karpathy-x]] - "I've played with a few Obsidian plugins to render and view data in other ways (e.g. Marp for slides)"

## Philosophy

Marp exemplifies the **everything-as-markdown** approach:
- No format islands - presentations are wiki pages
- LLM can create presentations as easily as articles
- Knowledge can flow between formats (article → slides → article)
- Version control and searching work across all content types

In LLM Wiki context: **reducing format friction** means ideas can be expressed in whatever structure serves them best, without leaving the ecosystem.
