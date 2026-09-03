# Before a RAG write

Keep retrieval, embeddings, privileged prompts, and provider credentials in the backend. Confirm
tenant/source ACL predicates are inside candidate queries and retrieved content has no instruction or
tool authority. Reject writes outside the task contract.

