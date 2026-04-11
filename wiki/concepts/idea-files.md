---
title: "Idea Files"
type: concept
tags: [sharing, collaboration, llm-agents, documentation, paradigm-shift]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/LLM Wiki：让大模型替你打理知识库的完整指南.md", "raw/llm-wiki.md"]
confidence: high
---

# Idea Files

## Definition

An "idea file" is an abstract, implementation-agnostic description of a concept or system, designed to be copied and pasted to an LLM agent so the agent can instantiate it according to the recipient's specific needs and environment. Rather than sharing executable code, configured applications, or detailed documentation, idea files share the **conceptual essence** and let each user's LLM customize the implementation. This represents a paradigm shift enabled by universal access to capable AI agents: **share ideas, not implementations**.

## How It Works

### Traditional Sharing (Code-Based)

1. Developer builds a useful tool/system
2. Shares via GitHub repo, npm package, Docker image, or detailed tutorial
3. Recipient must: clone, configure, install dependencies, adapt to their environment
4. Maintenance burden: author updates code, recipients pull changes
5. Friction: Different OS, versions, preferences require forking and customization

### Idea File Sharing (Concept-Based)

1. Creator describes the system at conceptual level with design principles
2. Shares as markdown/text file (e.g., GitHub Gist)
3. Recipient copies file into conversation with their LLM agent
4. Agent reads concept and implements it for recipient's specific environment
5. No installation, no configuration conflicts - agent adapts to local context
6. Evolution: Each user's agent can extend/modify based on their needs

### Karpathy's LLM Wiki as Example

Karpathy didn't release:
- A configured Obsidian vault
- Scripts in specific languages
- Docker containers
- Step-by-step tutorial

He released an **idea file** describing:
- The three-layer architecture
- The ingest/query/lint operations
- The philosophy behind choices
- The general approach

Then users' LLM agents (Claude Code, Codex, etc.) implement it for their specific:
- Operating system (macOS, Windows, Linux)
- Preferred tools (Obsidian, VS Code, Vim)
- Directory structure preferences
- Workflow customizations

## Key Parameters

- **Abstraction level**: How conceptual vs concrete - too abstract becomes vague, too concrete loses portability
- **Agent capability requirement**: Assumes recipient has capable LLM agent to do implementation
- **Domain specificity**: General patterns vs domain-specific details
- **Evolution model**: Static idea file vs living document that evolves with community feedback

## When To Use

**Share as idea file when:**
- Concept is system/workflow/pattern rather than single-purpose tool
- Target audience has access to LLM agents
- Implementation details vary by environment (OS, tools, preferences)
- Value is in the **approach** more than specific code
- You want recipients to adapt freely without maintaining compatibility

**Traditional code sharing still better when:**
- Building production software requiring exact behavior
- Complex interdependencies that agents can't reliably reproduce
- Performance-critical implementation
- Target audience may not have capable LLM agents
- Need version control and collaborative code development

## Risks & Pitfalls

- **Assumes agent access**: Not everyone has Claude/GPT-4 level agents yet (though increasingly common)
- **Reproduction quality**: Agent-implemented versions may miss subtle details or best practices
- **Learning depth**: Reading code can teach implementation skills; idea files skip that
- **Debugging difficulty**: When agent-built system breaks, harder to trace without seeing canonical implementation
- **Concept creep**: Vague idea files can lead to inconsistent interpretations
- **No collaborative refinement**: Code repos enable PRs and community improvement; idea files are one-way

## Related Concepts

- [[concepts/llm-knowledge-base]] - The system Karpathy shared as an idea file
- [[concepts/schema-file]] - Part of idea file - tells agent how to maintain wiki
- [[concepts/second-brain]] - Concept level shared via idea files, implemented variously

## Comparison to Traditional Documentation

| Dimension | Traditional Docs | Idea File |
|-----------|------------------|-----------|
| Specificity | Step-by-step, concrete | Conceptual, abstract |
| Portability | Specific to tech stack | Adaptable to any stack |
| Maintenance | Author updates, users pull | One-way concept transfer |
| Implementation | User follows instructions | Agent implements based on understanding |
| Customization | Fork and modify | Agent adapts from start |
| Learning curve | Learn specific tools | Learn concepts, agent handles tools |

## Karpathy's Quote

> "In the LLM Agent era, sharing concrete code or applications isn't as necessary. You just share ideas, and the other person's agent will customize and build according to their specific needs."

This reflects a subtle but profound shift: when everyone has a capable AI that can turn concepts into code, **ideas become more portable than implementations**.

## Community Examples

**Successful idea file applications:**
- ".brain folder pattern" - lightweight version for projects, widely adopted with variations
- "Claudeopedia" - weekend product built from LLM Wiki idea file
- Various personal knowledge base implementations from same conceptual source

Each implementation differs in:
- Directory structure
- Tool choices (Obsidian vs VS Code vs Vim)
- Automation level
- Domain focus
- Scale considerations

But all share the core concept, adapted to user context.

## Open Source Implications

Idea files represent **"open ideas"** rather than "open code":
- Not licensed like software (MIT, GPL) but shared as public knowledge
- Cannot be "forked" in git sense, but freely adapted
- No contributor model - more like academic paper than codebase
- Credit flows to original thinker, not maintainers

This may complement rather than replace open source code:
- Idea files for high-level patterns and workflows
- Code repos for production software and complex tools
- Both have roles in knowledge sharing ecosystem

## Related Entities

- [[entities/andrej-karpathy]] - Popularized idea file approach with LLM Wiki
- [[entities/claude-code]] - Agent that can consume and implement idea files
- [[entities/obsidian]] - Tool mentioned in idea files but implementation-agnostic

## Sources

- [[summaries/chinese-comprehensive-guide]] - Section "Idea File: A New Sharing Paradigm"
- [[summaries/llm-wiki]] - The idea file itself

## Future Implications

If idea files become standard:
- **Documentation shifts** from "how to install" to "what it does and why"
- **Learning** focuses on concepts over syntax
- **Collaboration** becomes conceptual dialogue rather than code review
- **Access** democratizes - anyone with agent can use ideas, regardless of technical skill

Counter-pressure: not everyone wants or can afford capable agents, so traditional docs won't disappear. Likely: **hybrid approach** where core ideas shared abstractly, reference implementations shared concretely.
