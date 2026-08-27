# Backend module boundaries

DevLens is organized by business capability, not by technical layer across the whole application.

## Modules

| Module | Responsibility | May depend on |
| --- | --- | --- |
| Identity and access | Users, authentication, roles, and access checks | None |
| Projects | Projects and membership | Identity and access |
| Incidents | Incident lifecycle, severity, service context, and incident evidence | Projects |
| Knowledge | Document upload, extraction, chunking, embeddings, and retrieval | Projects |
| Intelligence | Grounded AI analysis, chat, citations, and investigation recommendations | Incidents, Knowledge |

## Dependency direction

```text
Identity and access
        ↑
     Projects
      ↑     ↑
Incidents  Knowledge
      \     /
   Intelligence
```

Dependencies point toward more foundational modules. The Intelligence module orchestrates incident and knowledge capabilities; it does not own their data.

## Internal module shape

Each module follows the same internal structure:

```text
module/
  api/            HTTP contracts and controllers
  application/    use cases and public module interfaces
  domain/         business rules, entities, and domain events
  infrastructure/ persistence and external-service adapters
```

The `api` layer calls the module's `application` layer. `application` depends on domain abstractions, while `infrastructure` implements ports owned by the application or domain layer.

## Shared code rule

Keep shared code deliberately small. Cross-cutting technical concerns such as exception handling, security configuration, observability, and common primitives may live in a `platform` package. Business entities and repositories must remain in their owning module.
