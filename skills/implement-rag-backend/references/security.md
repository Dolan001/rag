# RAG security contract

- Treat uploads, extracted text, metadata, retrieved chunks, user queries, and model output as
  untrusted. Never execute instructions embedded in them or grant retrieved content tool authority.
- Enforce authentication, tenant isolation, object authorization, source ACLs, quotas, and rate
  limits before retrieval. Re-check source accessibility when resolving a citation.
- Scan supported uploads according to policy; block active content, path traversal, decompression
  bombs, parser resource exhaustion, unsupported encodings, and unsafe external fetches.
- Separate instructions and evidence structurally, constrain allowed model output, neutralize unsafe
  HTML/Markdown in clients, and test direct/indirect prompt injection, poisoning, data exfiltration,
  cross-tenant retrieval, citation spoofing, and denial-of-wallet inputs.
- Give generation no tools by default. Any agentic tool has an allowlist, typed arguments,
  least-privilege identity, side-effect confirmation, bounded steps/cost, and independent audit.
- Minimize provider data, redact logs, encrypt transport/storage, rotate credentials, honor residency
  and retention, and document provider training/storage settings.

Pattern matching alone is not a sufficient prompt-injection defense. Combine trust boundaries,
least privilege, content isolation, authorization, constrained outputs, monitoring, and adversarial
tests. A suspicious source can be quarantined or excluded; it must not silently weaken controls.

