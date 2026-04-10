---
title: "Obsidian Web Clipper"
type: concept
tags: [tools, obsidian, ingest, chrome-extension]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/karpathy-x.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# Obsidian Web Clipper

## Definition

Obsidian Web Clipper is a Chrome browser extension that converts web articles to markdown format and saves them directly into an [[entities/obsidian]] vault. It's the primary tool for rapidly capturing web content into the `raw/` directory for later processing through [[concepts/ingest-workflow]].

## How It Works

**Basic operation:**

1. Install extension from Chrome Web Store
2. Configure target vault and default folder (typically `raw/`)
3. While viewing any web page, click extension icon
4. Choose vault location (or use default)
5. Click "Add to Obsidian"
6. Extension scrapes text and images into markdown file

**Configuration options:**

- **Default folder**: Set to `raw/` to align with [[concepts/llm-knowledge-base]] structure
- **Template**: Customize frontmatter and formatting
- **Image handling**: Choose whether to embed images or link externally
- **Naming**: Configure file naming pattern
- **Hotkeys**: Set keyboard shortcuts for quick clipping

**Image downloading:**

- Web clipper initially embeds images as URLs
- In Obsidian settings, configure attachment folder (e.g., `raw/assets/`)
- Bind hotkey to "Download attachments for current file"
- After clipping, hit hotkey to download all images locally
- Allows LLM to view images directly rather than relying on external URLs

## Key Parameters

- **Source selection**: Full page, selected text, or specific elements
- **Formatting**: How to handle tables, code blocks, lists
- **Metadata**: What frontmatter to include (URL, date, author)
- **Vault targeting**: Which vault to send to if managing multiple

## When To Use

**Ideal for:**
- Research articles and blog posts
- Documentation pages
- News articles and analyses
- Tutorial and how-to content
- Reference materials and specifications

**Workflow integration:**

1. **Browse and clip**: Collect interesting articles throughout day/week
2. **Batch process**: Later run [[concepts/ingest-workflow]] on all clips
3. **Mobile sync**: Clip on desktop, or use mobile Obsidian app
4. **Automated ingest**: Use [[concepts/loop-automation]] to auto-process clips periodically

**Alternatives:**
- **Summarize tool**: For YouTube videos (transcript extraction)
- **Manual markdown**: Copy-paste and format manually
- **Browser bookmarks**: Save URLs then fetch later with web tools
- **RSS feeds**: Automated article capture

## Risks & Pitfalls

- **Paywall content**: May not capture full text behind paywalls
- **Dynamic content**: JavaScript-heavy sites may not clip correctly
- **Formatting loss**: Complex layouts may lose structure
- **Image bloat**: Downloading all images can consume significant disk space
- **Dead links**: External images may break if not downloaded locally
- **Over-clipping**: Easy to capture more than you'll actually process
- **Context loss**: Clipping without noting why it's interesting reduces value

## Related Concepts

- [[concepts/ingest-workflow]] — Next step after clipping content
- [[concepts/llm-knowledge-base]] — System that web clipper feeds
- [[entities/obsidian]] — Application that web clipper extends
- [[concepts/second-brain]] — Workflow pattern using web clipper for capture

## Sources

- [[summaries/llm-wiki]] — Web clipper in tips and tricks
- [[summaries/karpathy-x]] — Web clipper for converting articles to markdown
- [[summaries/claude-karpathy-second-brain-video]] — Web clipper setup and demonstration
