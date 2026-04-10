---
title: "RAG (Retrieval Augmented Generation)"
type: concept
tags: [retrieval, llm-agents, advanced]
created: 2026-04-10
updated: 2026-04-10
sources: ["raw/llm-wiki.md", "raw/Claude + Karpathy's Second Brain is INSANE.md"]
confidence: high
---

# RAG (Retrieval Augmented Generation)

## Definition

Retrieval Augmented Generation (RAG) is an approach where LLMs retrieve relevant document chunks from a corpus at query time using search (typically embedding-based vector search), then generate answers based on those retrieved fragments. This contrasts with [[concepts/knowledge-compilation]], where knowledge is pre-compiled into a structured wiki that persists between queries.

## How It Works

**Standard RAG pipeline:**

1. **Indexing phase**:
   - Chunk documents into segments (paragraphs, pages)
   - Generate embeddings for each chunk
   - Store in vector database with metadata

2. **Query phase**:
   - User asks a question
   - Question embedded as vector
   - Semantic search finds top-K relevant chunks
   - Chunks passed to LLM as context
   - LLM generates answer from retrieved fragments

**Common RAG systems:**

- **NotebookLM**: Upload files, query with retrieval
- **ChatGPT file uploads**: Similar retrieval-based approach
- **Claude Projects**: Can work as RAG with many documents
- **Enterprise search**: Large-scale RAG over company docs

## Key Parameters

- **Chunk size**: How to segment documents (sentences, paragraphs, pages)
- **Embedding model**: Which model to use for vectorization
- **Top-K**: How many chunks to retrieve per query
- **Reranking**: Whether to use LLM to reorder retrieved chunks
- **Hybrid search**: Combining vector search with keyword (BM25)
- **Index scope**: What documents are included in search

## When To Use

**RAG advantages:**

- **Scale**: Works with very large document collections (millions of docs)
- **Freshness**: New documents immediately available without reprocessing entire corpus
- **Simplicity**: No need to maintain complex wiki structure
- **Storage**: Only stores embeddings, not full compiled knowledge
- **Flexibility**: Same corpus supports many query styles

**Prefer RAG over [[concepts/llm-knowledge-base]] when:**

- Corpus is very large (1000+ documents, multi-million words)
- Documents change frequently (daily/hourly updates)
- Queries are unpredictable and diverse
- No need for synthesis or cross-document relationships
- Simple Q&A rather than knowledge building
- Multiple users with different information needs

**[[concepts/llm-knowledge-base]] advantages over RAG:**

- **Synthesis**: Relationships and contradictions already identified
- **Compounding**: Knowledge accumulates rather than being re-derived
- **Cross-references**: Explicit links vs. implicit similarity
- **Low latency**: No retrieval search needed
- **Quality**: Contradictions resolved, confidence tracked
- **Insight preservation**: Query answers can be filed back

## Risks & Pitfalls

- **Chunking issues**: Important context may be split across chunks
- **Retrieval failures**: Relevant content may not be retrieved if embedding doesn't match query
- **Context window limits**: Can only retrieve limited chunks per query
- **No synthesis**: Each query re-derives knowledge from raw fragments
- **Contradiction blindness**: Conflicting information in different chunks not flagged
- **Cost**: Embedding generation and vector search infrastructure
- **Lost connections**: Relationships between documents not captured

## Related Concepts

- [[concepts/llm-knowledge-base]] — Alternative compilation-based approach
- [[concepts/knowledge-compilation]] — Core difference in philosophy
- [[concepts/query-workflow]] — Similar query goal, different mechanism
- [[concepts/second-brain]] — Personal knowledge at scale between simple RAG and full LLM wiki

## Sources

- [[summaries/llm-wiki]] — Distinguishes LLM wiki from RAG approaches
- [[summaries/claude-karpathy-second-brain-video]] — RAG as advanced tier beyond second brain
