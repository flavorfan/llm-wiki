---
title: "Defuddle"
type: concept
tags: [tools, web-scraping, markdown, token-optimization, obsidian]
created: 2026-04-12
updated: 2026-04-12
sources: ["raw/Obsidian 必装 Skills.md"]
confidence: high
---

## Definition

Defuddle is a web content extraction tool that converts web pages into clean Markdown format by removing navigation bars, sidebars, advertisements, and other non-content elements. It's designed as both a command-line tool and an [[concepts/agent-skills|Agent Skill]] for [[entities/claude-code]] and other AI agents.

## How It Works

**Process Flow**:
1. Receives a URL as input
2. Fetches the web page HTML
3. Uses readability algorithms to identify main content
4. Strips navigation, ads, footers, sidebars
5. Converts remaining HTML to clean Markdown
6. Returns plain text suitable for LLM processing

**YouTube Support**: Recent versions support YouTube video URLs, extracting transcripts via YouTube's official API (not `yt-dlp` or third-party scrapers).

**Token Savings**: A typical blog post might be:
- Raw HTML: 50,000+ characters (ads, navigation, scripts)
- Defuddle output: 5,000 characters (pure content)
- Token reduction: 90%+

## Key Features

**Content Extraction**: Identifies and preserves:
- Article body text
- Headings (converted to Markdown `#` syntax)
- Images (as Markdown image links)
- Code blocks (with language tags)
- Lists and tables

**Noise Removal**: Strips:
- Navigation menus
- Sidebars
- Footer links
- Cookie notices
- Advertisement blocks
- Social media widgets
- Comment sections

**Format Preservation**: Maintains:
- Document structure (headings, paragraphs)
- Semantic formatting (bold, italic, code)
- Links (converted to Markdown syntax)

## When To Use

**Ideal for**:
- Reading online articles/blog posts with AI
- Capturing web documentation into [[entities/obsidian]]
- Processing newsletters or medium posts
- Extracting YouTube video transcripts
- Reducing token costs when analyzing web content

**Works best with**:
- Standard HTML pages (news, blogs, documentation)
- YouTube videos with transcripts
- Well-structured content sites

**Not suitable for**:
- Login-required pages (paywalled content)
- Single-page apps with heavy JavaScript rendering
- Image-heavy content where visual layout matters
- Interactive web apps where functionality is the content

## Risks & Pitfalls

**Content Loss**: Readability algorithms might incorrectly classify important content as noise and remove it. Always verify critical content is preserved.

**Copyright**: Extracting paywalled or copyrighted content may violate terms of service or laws. Use responsibly.

**Dynamic Content**: Pages that load content via JavaScript after initial render may not be fully captured.

**Formatting Edge Cases**: Complex layouts (multi-column, embedded widgets) may not convert cleanly to linear Markdown.

**YouTube Limitations**: Only works for videos with available transcripts. Auto-generated captions may have accuracy issues.

## Installation

**As Command-Line Tool**:
```bash
npm install -g defuddle
```

**As Agent Skill**:
- Claude Code: Place in `.claude/skills/defuddle/`
- OpenCode: Place in `~/.opencode/skills/defuddle/`
- Maintained by [[entities/steph-ango]] at `kepano/obsidian-skills`

## Dependencies

- **Node.js**: Required for installation and execution
- **Internet connection**: Needs to fetch URLs

## Usage Example

**Command Line**:
```bash
defuddle https://example.com/article > article.md
```

**Agent Skill** (triggers automatically):
```
User: "Read this article and summarize: https://example.com/article"
Agent: [Invokes defuddle] → clean Markdown → summarizes
```

## Related Concepts

- [[concepts/agent-skills]] — Defuddle is implemented as a Skill
- [[concepts/token-optimization]] — Primary use case: reduce web scraping token costs
- [[concepts/obsidian-web-clipper]] — Alternative approach: browser extension for clipping
- [[concepts/llm-knowledge-base]] — Web scraping as part of ingest workflow

## Related Entities

- [[entities/steph-ango]] — Creator and maintainer
- [[entities/claude-code]] — Primary agent that uses this Skill

## Sources

- [[summaries/obsidian-essential-skills]] — Skill catalog entry
