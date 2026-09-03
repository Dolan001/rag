---
name: design-rag-system
description: Design a production RAG contract when a PRD explicitly requires retrieval-augmented generation, document Q&A, semantic search, grounded answers, or a knowledge-base assistant.
---

# Design a RAG system

1. Read `references/architecture-decisions.md`.
2. Bind every decision and quality threshold to requirement and acceptance IDs. Ask for input only
   when source policy, authorization, retention, provider policy, or measurable success is missing.
3. Default to backend-owned two-step hybrid retrieval using PostgreSQL full-text search plus
   pgvector, with optional reranking behind an adapter. Do not default to an agentic loop.
4. Produce separable ingestion, retrieval, generation, citation, and evaluation task contracts.
5. Activate durable background work when ingestion can outlive an HTTP request; activate object
   storage for original uploads; activate realtime only when the response transport requires it.

