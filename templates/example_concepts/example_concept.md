
---
type: Concept
title: RAG vs Compiled Knowledge
description: Two paradigms for LLM-powered knowledge retrieval: retrieval-at-query-time vs incremental wiki-building.
tags:
  - llm
  - knowledge-management
  - architecture
generated:
  by: reference_agent/lumo-v2
  at: 2026-10-01T09:30:00Z
verified:
  - by: human:lrm
    at: 2026-10-01T10:00:00Z
status: stable
stale_after: 2027-10-01T00:00:00Z
sources:
  - id: llm-wiki-pattern
    resource: ../../specs/llm-wiki.md
    title: LLM Wiki - Building Personal Knowledge Bases Using LLMs
    author: llm-wiki-author
    last_modified: 2026-09-15T00:00:00Z
  - id: rag-overview
    resource: https://www.pinecone.io/learn/rag/
    title: Retrieval-Augmented Generation Overview
    author: pinecone-team
    last_modified: 2026-08-10T00:00:00Z
---

# Definition

Two competing architectures for building AI-augmented knowledge systems:

| Aspect | RAG (Retrieval-Augmented Generation) | Compiled Knowledge (Wiki) |
|--------|-------------------------------------|---------------------------|
| **Storage** | Raw documents unchanged | Synthesized into structured pages |
| **Processing** | At query time | During ingestion |
| **Cross-references** | Discovered per-query | Built incrementally |
| **Maintenance Cost** | Low (no synthesis) | Low (handled by agent) |
| **Answer Quality** | Varies with retrieval accuracy | Consistent (pre-synthesized) |

## RAG Approach

In a RAG system:
1. Documents remain immutable in a vector database
2. When queried, relevant chunks are retrieved via embeddings
3. The LLM synthesizes an answer from retrieved fragments
4. Each query re-discovers knowledge independently

**Strengths:** Simple to implement; no content modification required  
**Weaknesses:** No accumulation; subtle questions requiring synthesis of 5+ documents struggle

## Compiled Knowledge Approach

In a compiled knowledge system (see [LLM Wiki](Knowledge%20Base/specs/llm-wiki.md)):
1. New sources are ingested and analyzed
2. Key information is extracted into wiki pages
3. Cross-references and contradictions are flagged during ingestion
4. The wiki grows richer with each source

**Strengths:** Compounding value; consistent synthesis; built-in contradiction detection  
**Weaknesses:** Requires disciplined ingestion workflow

## Practical Implications

For long-term knowledge projects (months to years), compiled knowledge typically outperforms RAG because the maintenance burden is borne by agents rather than humans. See [Memex](./memex.md) for the historical antecedent of this vision.

---

[^llm-wiki-pattern]: LLM Wiki - Building Personal Knowledge Bases Using LLMs
[^rag-overview]: Retrieval-Augmented Generation Overview