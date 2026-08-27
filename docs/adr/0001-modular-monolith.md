# ADR 0001: Start DevLens AI as a modular monolith

## Status

Accepted

## Context

DevLens AI is a solo, local-first project. Its MVP needs authentication, projects, incidents, document ingestion, retrieval-augmented generation, and AI-assisted analysis. These capabilities need clear boundaries, but do not initially require independently deployed services.

## Decision

Build the backend as one Spring Boot application structured as independent business modules. Each module owns its domain model, application use cases, ports, and adapters. Modules communicate through explicit interfaces and domain events rather than reaching into each other's persistence code.

The React application remains a separate frontend. Ollama and the database are separate local infrastructure services. Long-running ingestion work runs as a background job inside the backend at first, backed by durable job records.

## Consequences

- Development, testing, and local deployment stay simple and free.
- The application can use one transactional database while preserving module boundaries.
- A module can be extracted later only when operational scale or team ownership makes that worthwhile.
- No microservices, message broker, or Kubernetes are part of the MVP.

## Module boundary rule

Code in one module must depend only on another module's public application interface, never on its entities, repositories, or database tables.
