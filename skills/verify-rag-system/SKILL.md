---
name: verify-rag-system
description: Independently evaluate a completed RAG backend, client, or integration against versioned quality, security, resilience, latency, and cost thresholds.
---

# Verify a RAG system

Read `references/evaluation.md`. Do not edit application code or reuse implementer conclusions.
Re-run the relevant project-owned evaluation lane and write `.ai/evidence/rag/<phase>.json` for
`backend`, each selected client, and `integration`. Mark verified only when all required checks and
PRD thresholds pass; otherwise record the failing cases through the workflow issue tracker.

