---
name: implement-rag-backend
description: Implement secure ingestion, PostgreSQL/pgvector retrieval, grounded generation, citations, and evaluation in a selected DRF or FastAPI backend when a feature activates RAG.
---

# Implement the RAG backend

Read the selected backend vertical-slice skill first, then:

- Read `references/data-and-ingestion.md` for uploads, parsing, schema, jobs, deletion, or reindexing.
- Read `references/retrieval-and-generation.md` for search, answering, streaming, citations, or
  provider integration.
- Read `references/security.md` for every RAG slice.

Keep one PRD-derived domain owner and split `ingestion`, `retrieval`, `generation`, `providers`, and
`evaluation` by responsibility as complexity grows. Use framework migrations for `vector` extension,
tables, constraints, and indexes. Provider secrets remain in backend environment settings and never
cross API responses. Produce `.ai/evidence/rag/backend.json` during independent backend verification.

