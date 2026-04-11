---
title: "Andrej Karpathy's LLM Wiki: Bye Bye RAG"
type: summary
tags: [rag, knowledge-synthesis, llm-agents, retrieval, persistence]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/Andrej Karpathy's LLM Wiki  Bye Bye RAG.md"]
confidence: high
---

# Andrej Karpathy's LLM Wiki: Bye Bye RAG

## Key Points

- **RAG is stateless**: Traditional RAG systems search documents on every query, rediscovering knowledge from scratch each time with no accumulation of understanding
- **LLM Wiki builds persistent knowledge**: Instead of repeatedly searching raw documents, the LLM incrementally builds and maintains a structured, interlinked knowledge base first, then queries against it
- **Knowledge compounds over time**: Each new document and query answer can be integrated back into the wiki, creating compound growth similar to compound interest
- **Maintenance is automated**: LLMs excel at tasks humans find tedious - updating multiple pages when new data arrives, maintaining cross-links, keeping consistency, detecting contradictions
- **Concrete workflow difference**:
  - RAG: Search → Answer → Reset (stateless)
  - LLM Wiki: Read → Organize → Link → Improve → Reuse (stateful)
- **Role shift for humans**: Instead of manually organizing knowledge, humans focus on finding quality inputs and asking meaningful questions while the LLM handles structure and maintenance
- **Knowledge graph in natural language**: Over time, scattered files become a connected knowledge graph of clean, structured, interlinked pages

## Relevant Concepts

- [[concepts/rag]] - Contrasted as the stateless alternative that repeats work on every query
- [[concepts/knowledge-compilation]] - The core process of building structured knowledge from raw sources
- [[concepts/persistent-artifact]] - The wiki as a durable, compounding artifact vs ephemeral chat responses
- [[concepts/llm-knowledge-base]] - The overall pattern this article explains
- [[concepts/wiki-maintenance]] - Automated maintenance as a key differentiator
- [[concepts/ingest-workflow]] - Processing new documents to extract and integrate knowledge
- [[concepts/knowledge-graph]] (needs creation) - The interconnected structure that emerges from linking pages

## Analogies Used

- "Like studying for an exam by re-reading all your books every time you get a question" (RAG problem)
- "Raw files are ingredients, LLM Wiki is the cooked meal"
- "With RAG you cook every time you're hungry; with LLM Wiki you build a kitchen that keeps improving its recipes"
- Knowledge compounds "like compound interest"

## Example Scenario

Electric vehicle research with three sources (Tesla annual report, battery technology deep dive, EV market trends blog):
- RAG: Three isolated documents queried independently each time
- LLM Wiki: Creates interconnected pages for "Tesla", "Battery Technology", "EV Market Trends" with cross-references, then queries can be saved as new pages like "Future Leaders in EV Batteries"

## Use Cases Mentioned

- Learning AI deeply (connecting transformers, RAG, agents concepts)
- Creating YouTube content (topics, scripts, linked ideas)
- Building courses (structured modules vs scattered notes)
- Personal knowledge management
- Team knowledge bases in companies

## Source Metadata

- **Type**: Medium article / blog post
- **Author**: Mehul Gupta
- **Published**: 2026-04-07
- **URL**: https://medium.com/data-science-in-your-pocket/andrej-karpathys-llm-wiki-bye-bye-rag-ee27730251f7
- **Target Audience**: General technical audience learning about LLM Wiki concept
- **Style**: Explanatory with concrete examples and simple analogies
- **Relationship to other sources**: Popularization/explanation of Karpathy's original idea from [[summaries/karpathy-x]] and [[summaries/llm-wiki]]
