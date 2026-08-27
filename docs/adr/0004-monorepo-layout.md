# ADR 0004: Use a small monorepo with separate application roots

## Status

Accepted

## Decision

Keep DevLens in one Git repository with separate roots for the backend and frontend.

```text
devlens-ai/
├── backend/        Spring Boot application
├── frontend/       React and TypeScript application
├── infra/          Container and local-environment configuration
├── docs/           Architecture decisions and project documentation
├── compose.yaml    Local service orchestration
├── README.md
└── .gitignore
```

## Rules

- The backend and frontend own their build files, dependencies, tests, and source code.
- `compose.yaml` orchestrates only local infrastructure dependencies; it does not replace each application's development command.
- `infra/` contains infrastructure-specific assets such as database initialization scripts and deployment manifests when they are needed.
- `docs/adr/` records irreversible or costly-to-reverse technical decisions.
- Shared API contracts will be generated or maintained explicitly later; do not create a shared source-code library prematurely.

## Consequences

- A single pull request can change a UI, API, database configuration, and documentation together.
- Application build systems remain independent: Maven for the backend and npm for the frontend.
- The layout remains straightforward to split into separate repositories later if a real need arises.
