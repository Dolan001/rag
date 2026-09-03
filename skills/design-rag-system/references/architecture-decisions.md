# RAG architecture decisions

Define these before implementation:

- Product mode: semantic search, document Q&A, conversational knowledge assistant, or explicit
  agentic investigation.
- Sources: accepted formats, maximum size/pages, trusted owners, language/OCR requirements,
  malware handling, parsing-quality rejection, retention, legal deletion, and version behavior.
- Access: tenant boundary, roles, source ACL inheritance, public/private visibility, and when ACL or
  group changes invalidate indexed authorization metadata.
- Ingestion: content hash, parser/version metadata, deterministic normalization, structure-aware
  chunking, overlap policy, chunk/source offsets, idempotency key, retry/dead-letter policy, and
  observable states from uploaded through ready/failed/deleted.
- Embeddings: provider adapter, model identifier, dimensions, distance metric, normalization,
  batching, rate limits, cache policy, migration/re-embedding plan, and prohibition on silently
  mixing incompatible embeddings.
- Retrieval: lexical and vector candidate counts, metadata/ACL filters, fusion method, optional
  reranker, diversity/deduplication, context-token budget, score cutoffs, and empty-result behavior.
- Generation: model adapter, structured prompt boundary, context treated as quoted untrusted data,
  answer schema, inline citations, grounded refusal/abstention, streaming, timeout, retry, and
  provider data-retention policy.
- Evaluation: versioned representative and adversarial cases, relevance judgments, answerable and
  unanswerable queries, retrieval metrics, groundedness/citation checks, latency percentiles, per-
  query cost ceiling, regression tolerance, and release thresholds.

Use exact search as a recall baseline before choosing HNSW or IVFFlat. At scale, benchmark filtered
recall and latency on production-shaped tenant distributions; PostgreSQL approximate indexes can
lose candidates after filters. Prefer indexed scalar ACL/tenant columns, iterative scans or
partitioning where measurements support them. Use RRF or a measured reranker for hybrid fusion.

