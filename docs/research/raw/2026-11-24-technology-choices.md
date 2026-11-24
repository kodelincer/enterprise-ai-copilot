# متن خام: گزینه‌های فناوری (۱۴۰۵/۰۹/۰۳ — 2026-11-24)

!!! note
    پیام رضا بدون ویرایش. جمع‌بندی در [مؤلفه‌ها و فناوری‌ها](../../architecture/stack.md).

> 10. Technology choices: what would I actually use?
> I wouldn't select every technology immediately. I'd build a small number of well-defined services.
>
> Here is a possible technology stack:
>
> | Layer | Possible technology | Purpose |
> |---|---|---|
> | Original storage | S3-compatible object storage / MinIO | Immutable source files |
> | Metadata and facts | PostgreSQL | Documents, entities, relationships, provenance |
> | Document processing | Docling / Unstructured | PDF, Office, layout extraction |
> | Embeddings | BGE-M3 or another multilingual embedding model | Semantic representations |
> | Full-text search | PostgreSQL FTS / OpenSearch | BM25-style lexical retrieval |
> | Vector search | pgvector / Qdrant | Similarity search |
> | Knowledge wiki | Markdown + Obsidian | Human-readable synthesized knowledge |
> | Markdown search | QMD | Hybrid search over the wiki |
> | Agent | Hermes | Orchestration and tool execution |
> | Agent memory | Honcho | Conversational and task context |
> | Evaluation | Ragas / Haystack evaluators | Quality measurement |
>
> These are candidates, not a requirement to deploy all of them.
>
> A few observations:
>
> PostgreSQL: I'd strongly consider making it the central metadata and relationship database. You can also use pgvector, which avoids operating a separate vector database at the beginning.
>
> QMD: Particularly interesting for the LLM Wiki side because it is designed to search Markdown knowledge bases. I would evaluate it separately from the original-document search system.
>
> GraphRAG: Worth studying when questions require connecting many entities and discovering global patterns across a large document collection. Microsoft describes an architecture that extracts a knowledge graph, builds communities, summarizes them, and uses those structures for retrieval. However, its indexing can be computationally expensive, so I wouldn't start there.
> GraphRAG+1
>
> Haystack: Worth investigating if you want to implement a modular retrieval and agent pipeline in Python. Its documentation distinguishes deterministic pipelines from agents that dynamically decide which steps to take
