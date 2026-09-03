# Tooling and observability

Use the fewest dependencies that satisfy the declared sources and providers:

- PostgreSQL `vector` extension plus the maintained `pgvector` Python integration for the selected
  ORM. Keep PostgreSQL full-text search in the same authorized query boundary.
- The existing Celery/Redis/outbox stack for durable ingestion. Do not add another queue merely for
  RAG.
- Format-specific parsers only for accepted MIME bytes: for example PyMuPDF or pypdf for PDFs,
  python-docx for DOCX, Beautiful Soup/lxml for HTML, and a safe Markdown parser for Markdown. Select
  one maintained parser per format and pin it. OCR, spreadsheets, archives, audio, and images are
  separate declared capabilities with resource and security limits; do not silently pretend an
  extraction succeeded.
- The official SDK for each selected embedding, reranking, or generation provider behind local typed
  adapters. Prefer small explicit pipeline code over a general orchestration framework. Add
  LangChain, LlamaIndex, or similar only when a requirement uses capabilities that justify its
  dependency, abstraction, and upgrade surface.
- The project's OpenTelemetry and structured-metrics boundary. Do not introduce a second telemetry
  system.

Record model/parser/chunker versions, request IDs, stage duration, candidate counts, selected chunk
IDs, empty-result/abstention outcome, provider status, usage units, estimated cost, cache outcome,
and error class. Never log raw private source text, complete prompts, embeddings, credentials, or
provider responses by default.

Expose metrics for ingestion queue age/depth, stage failures and retries, documents/chunks by state,
embedding throughput/rate limits, retrieval latency and empty-result rate, filtered exact-vs-ANN
recall samples, reranker/generation latency, abstention and citation-invalid rates, provider errors,
usage/cost, and deletion/reindex lag. Trace parse, chunk, embed, lexical retrieval, vector retrieval,
fusion, rerank, context assembly, generation, citation validation, and streaming as separate spans
using IDs and counts rather than content.

Set alerts and dashboards from PRD service levels. Cap upload size/pages, extracted characters,
chunks per document, query length, candidate counts, context units, output units, concurrent
requests, retries, wall time, and per-user/tenant usage so malformed documents or prompts cannot
create unbounded cost.
