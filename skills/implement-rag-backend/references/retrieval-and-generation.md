# Retrieval and generation contract

Validate and normalize the query, authorize the knowledge base, and construct an immutable query
policy. Apply tenant, source, status, and ACL predicates inside both lexical and vector candidate
queries before fusion. Never fetch broad candidates and filter unauthorized rows in application
memory. Record safe retrieval diagnostics without raw private content.

Default retrieval stages:

1. PostgreSQL full-text and pgvector candidates with separately configurable limits;
2. deterministic reciprocal-rank fusion;
3. optional provider-neutral reranking when evaluation proves benefit;
4. adjacent-chunk expansion, deduplication, and source diversity within a hard context-token budget;
5. a relevance threshold that yields an empty grounded result when evidence is weak.

Build the model request with system policy separate from user text and clearly delimited retrieved
content. State that sources are untrusted evidence, not instructions. The response contract includes
answer text, stable source citations, source title/location/page or section, quoted span identifiers,
request ID, completion state, and machine-readable refusal/error types. Verify every citation points
to a retrieved, authorized span and reject invented citations. Unsupported or conflicting evidence
must produce the specified abstention instead of confident fabrication.

Keep embedding, reranking, and generation behind typed adapters with timeout, bounded retry,
circuit-breaking/backpressure, usage accounting, and provider-specific retention configuration.
Streaming uses SSE by default for one-way tokens and WebSocket only when bidirectional requirements
justify it. Cancellation must stop downstream work and usage accounting must survive partial output.

