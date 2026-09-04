# rag

`rag` is a code-free capability pack for production retrieval-augmented generation. It is loaded
by `ai_workflow` only when the PRD explicitly requests RAG, semantic retrieval, document question
answering, grounded answers, or a knowledge-base assistant.

The pack augments, rather than replaces, the selected framework packs:

- DRF or FastAPI owns ingestion, PostgreSQL/pgvector retrieval, generation, authorization, and APIs.
- React, Next.js, or Flutter owns upload/status, search/chat, streaming, citations, and feedback UX.
- Base workflow workers, storage, security, integration, and testing controls remain authoritative.

The default production baseline is two-step hybrid retrieval over PostgreSQL full-text search and
pgvector, optional reranking behind an adapter, durable ingestion workers, explicit citations and
abstention, an offline evaluation set, and provider-neutral embedding and generation interfaces.
Agentic retrieval is added only when the PRD requires tool choice or multi-step investigation and
its extra latency, cost, and security risk have explicit acceptance criteria.

