# RAG architecture rules

RAG is backend-owned and client-consumed. Separate ingestion from online query execution. Use
PostgreSQL plus pgvector and PostgreSQL full-text search by default; add a new vector service only from
measured requirements. Keep embedding, reranking, and generation provider-neutral. Preserve document
versions and source provenance, enforce authorization before retrieval, and define an explicit
abstention path. Agentic RAG is opt-in and bounded.

