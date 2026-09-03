# Generated RAG structure contract

Do not create an independent application. The selected backend owns a PRD-named domain such as
`knowledge_bases` and splits ingestion, retrieval, generation, providers, and evaluation by
responsibility. DRF follows its models/services/selectors/serializers/views/URLs boundaries; FastAPI
follows models/services/repositories/queries/schemas/dependencies/routes. Clients place RAG screens
inside a PRD-named feature and consume only the generated typed API client.

Original documents use approved object storage. PostgreSQL owns metadata, ACLs, lifecycle, chunks,
embeddings, conversations when required, citations, feedback, and evaluation summaries. Keep large
binary files, secrets, provider traces, and generated vector data out of Git.

