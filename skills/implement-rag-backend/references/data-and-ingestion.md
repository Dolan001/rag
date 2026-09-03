# Data and ingestion contract

Model at least the concepts required by the PRD: knowledge base, source document, immutable document
version, ingestion job/attempt, chunk, embedding record, and source ACL. Add conversations, messages,
feedback, or evaluation runs only when consumed. Store stable IDs, tenant/owner, lifecycle state,
content hash, parser/chunker/embedding versions, source locator, page/section/offset provenance,
language, token count, timestamps, and soft/hard deletion state as applicable.

Enforce unique idempotency and version constraints, foreign keys, check constraints, cascade policy,
and indexes for tenant/ACL/status/source/version/filter paths. Keep the original binary in approved
object storage and durable metadata in PostgreSQL; avoid storing large binaries in vector rows.

The worker pipeline is resumable and idempotent:

1. authorize and validate upload metadata, size, MIME bytes, checksum, quota, and malware policy;
2. persist a version and enqueue only after transaction commit;
3. extract text with a format-specific parser, preserving page/section provenance;
4. normalize without erasing meaning and reject unusable extraction with a visible reason;
5. chunk by document structure and configured token bounds;
6. batch embeddings behind a rate-limited adapter and upsert by content/model/version key;
7. publish `ready` atomically only after completeness checks;
8. retry transient failures with jitter and limits, dead-letter permanent failures, and expose status;
9. make cancellation, replacement, reindexing, ACL changes, and deletion deterministic.

Never mix vectors from different models or dimensions in one index path. A model/chunker/parser
change creates a new indexed version with shadow evaluation and atomic promotion; do not mutate a
serving corpus partially. Deletion must remove object, chunks, embeddings, caches, and retrievability
within the PRD deadline while retaining only explicitly required audit facts.

