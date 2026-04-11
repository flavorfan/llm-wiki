---
title: "ChatGPT"
type: entity
tags: [tools, openai, llm-agents, rag, ai-products]
created: 2026-04-11
updated: 2026-04-11
sources: ["raw/Andrej Karpathy's LLM Wiki  Bye Bye RAG.md", "raw/LLM Wiki：让大模型替你打理知识库的完整指南.md"]
confidence: high
---

# ChatGPT

## Overview

ChatGPT is OpenAI's conversational AI product, built on the GPT series of large language models. It includes a file upload feature that allows users to attach documents and query them during conversations. This feature uses Retrieval-Augmented Generation (RAG) to search uploaded files and incorporate relevant content into responses.

## Characteristics

- **Vendor**: [[entities/openai]]
- **Architecture**: RAG-based file search combined with conversational interface
- **File handling**: Users can upload PDFs, text files, images, and other documents; ChatGPT searches these at query time
- **State management**: Conversation memory persists within a single session/thread, but document understanding doesn't accumulate across queries
- **Availability**: Web interface, mobile apps, API
- **Access tiers**: Free tier (GPT-3.5), Plus/Pro tiers (GPT-4, higher limits, advanced features)
- **Data location**: Cloud-based, files stored on OpenAI servers during session

## File Upload Feature Behavior

When you upload files to ChatGPT:
1. Files are parsed and indexed for the current conversation
2. Queries trigger retrieval of relevant chunks from uploaded files
3. Retrieved content is included in context for answer generation
4. Each query performs fresh retrieval - no synthesis is preserved
5. Files are session-scoped - not available in new conversations unless re-uploaded

## Comparison to LLM Wiki

| Dimension | ChatGPT File Upload | LLM Wiki |
|-----------|---------------------|----------|
| Document processing | RAG retrieval per query | Pre-compiled structured wiki |
| Knowledge persistence | Session-scoped only | Permanent, growing artifact |
| Cross-document synthesis | Temporary, per query | Pre-built and maintained |
| Output durability | Chat history (ephemeral) | Wiki pages (persistent) |
| Maintenance | None | Automated by LLM agent |
| Format | Conversational responses | Structured markdown |

## As a RAG Example

ChatGPT's file upload feature exemplifies the "阅后即焚" (read-then-burn / ephemeral) experience critiqued in LLM Wiki discussions:
- You ask a question requiring synthesis of five documents
- ChatGPT retrieves, pieces together, and answers
- Tomorrow you ask the same question: same retrieval work repeated
- Knowledge doesn't "grow" - it's rediscovered each time

## When To Use ChatGPT vs LLM Wiki

**Use ChatGPT when:**
- Quick, one-off questions about documents
- Conversational exploration of a topic
- No need to preserve structured knowledge long-term
- Convenience and accessibility matter more than data sovereignty

**Use LLM Wiki when:**
- Knowledge accumulates over weeks/months/years
- You need cross-referenced, interconnected understanding
- Queries should enhance the knowledge base, not disappear into chat logs
- You want local control and portability of your knowledge infrastructure

## Related Entities

- [[entities/openai]] - Organization that created ChatGPT
- [[entities/andrej-karpathy]] - Former OpenAI researcher who articulated alternative to ChatGPT's RAG approach
- [[entities/claude-code]] - Alternative LLM agent designed for local file manipulation, used in wiki workflows
- [[entities/notebooklm]] - Google's similar product with RAG-based document Q&A

## Related Concepts

- [[concepts/rag]] - The retrieval technique underlying ChatGPT's file search
- [[concepts/llm-knowledge-base]] - Alternative pattern addressing ChatGPT's stateless limitations
- [[concepts/persistent-artifact]] - What LLM Wiki provides that ChatGPT file uploads lack
- [[concepts/knowledge-compilation]] - Contrasts with ChatGPT's query-time retrieval

## Strengths

- Highly accessible - no technical setup, polished UI
- Conversational interface feels natural for exploration
- Broad general knowledge from training data
- File upload adds context without complex workflows
- Large user base and ecosystem (plugins, custom GPTs)

## Limitations (Per LLM Wiki Perspective)

- File knowledge is session-scoped and stateless
- No accumulation or compounding of insights
- Answers live in ephemeral chat history, not durable artifacts
- No automated maintenance of cross-document understanding
- Cloud-only, no local data control
- Each complex question repeats the same retrieval and synthesis work
