# ADR 0003: Use a local-first development environment

## Status

Accepted

## Decision

Use the following local development stack:

- Java 21 LTS with Maven Wrapper for the Spring Boot backend.
- Node.js 24 LTS with npm, React, TypeScript, and Vite for the frontend.
- Docker Compose for PostgreSQL with pgvector.
- Native Ollama on the developer's host machine for local chat and embedding models.

## Ollama operating rule

Ollama is an optional local dependency. The backend and frontend must start without it. AI endpoints will report that the AI provider is unavailable until Ollama is running. The choice of host operating system is not an application requirement.

For development on an 8 GB Apple Silicon Mac, begin with `llama3.2:1b` for chat tasks and `nomic-embed-text` for embeddings. This is guidance for the current developer machine, not a product constraint.

## Consequences

- Local development remains free and does not require cloud credentials.
- PostgreSQL is reproducible through Docker Compose.
- Native Ollama can use the host machine's supported hardware acceleration, such as Metal on Apple Silicon.
- AI behaviour can be tested independently from normal application development.
