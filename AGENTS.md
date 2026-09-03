# Retrieval-augmented generation behavior pack

This repository contains AI behavior only. Never add a runnable application, copied framework
source, model weights, document fixtures, credentials, or generated indexes. Agents consume this
pack alongside exactly one backend pack and any selected client packs while writing original code
inside a separate target monorepo.

RAG is a requirement-triggered capability, not a framework. Keep retrieval and provider secrets in
the backend. Enforce authorization before ranking, preserve source provenance, treat retrieved text
as untrusted data, require measurable retrieval and answer quality, and fail closed when evidence is
missing. PostgreSQL with pgvector is the default vector store; do not introduce another vector
database without an explicit scale, isolation, or operational requirement.

