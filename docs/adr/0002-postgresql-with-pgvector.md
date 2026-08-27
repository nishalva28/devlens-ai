# ADR 0002: Use PostgreSQL with pgvector for application and vector data

## Status

Accepted

## Context

DevLens stores relational application data and needs semantic retrieval over uploaded documents and historical incident evidence. The project must remain local-first and free to run for its MVP.

The initial project reference proposed MySQL. Its relational capabilities are sufficient, but adopting a separate vector database alongside it would add unnecessary operational complexity.

## Decision

Use PostgreSQL as the sole relational database and enable the open-source `pgvector` extension for embedding storage and similarity search.

Use Spring AI's `PgVectorStore` integration for initial document retrieval. Store application-owned metadata and permissions in DevLens tables; keep vector-store metadata limited to retrieval filtering fields.

Run PostgreSQL with pgvector locally in a container during development. Use exact retrieval for small development data sets and introduce an HNSW cosine-similarity index only when retrieval volume warrants it.

## Consequences

- One free local database stores transactional data and vector embeddings.
- Retrieval can combine project-scoped metadata filtering with semantic similarity.
- The project avoids operating a separate vector database in the MVP.
- MySQL is not part of the initial implementation, despite the original reference stack.
- Changing embedding models later may require re-embedding documents because vector dimensions and values can differ.
