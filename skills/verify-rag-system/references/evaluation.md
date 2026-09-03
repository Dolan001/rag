# RAG evaluation contract

Version an evaluation dataset with source snapshot/hash, query, accessible tenant/role, relevance
judgments, answerable/unanswerable label, expected facts, expected citations, forbidden disclosures,
and slice tags such as language, format, ambiguity, freshness, or adversarial input. Keep production
content out unless approved and sanitized. Split tuning and release sets to reduce overfitting.

Measure retrieval independently from generation:

- Retrieval: Recall@k or hit rate, MRR/nDCG when ranking matters, ACL leakage count (must be zero),
  duplicate/source-diversity behavior, filtered ANN recall against exact-search baseline, and latency.
- Generation: required-fact coverage, groundedness/faithfulness, citation precision and coverage,
  citation-span validity, abstention precision/recall, harmful/secret disclosure count, and structured
  response validity.
- Operations: ingestion success/retry/dead-letter/delete/reindex behavior, p50/p95/p99 latency,
  concurrency/backpressure, timeout/cancellation, provider degradation, token usage, and per-query
  cost against the PRD ceiling.
- Client/integration: typed contract, stream ordering/recovery, citations and source authorization,
  complete state/error coverage, accessibility, feedback, and safe rendering.

Use deterministic scoring where possible. Model-based judges require a pinned model/prompt, blinded
inputs, structured scores, calibration against human-reviewed examples, and a deterministic fallback;
they never replace ACL, citation, schema, or leakage assertions. Store aggregate metrics and case IDs,
not sensitive source bodies or secrets. Fail the release on any security leak or threshold regression.

