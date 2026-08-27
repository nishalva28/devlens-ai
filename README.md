# DevLens AI

DevLens AI is a production-incident intelligence platform that helps engineering teams investigate incidents using logs, stack traces, documentation, deployment information, and historical incidents.

## Status

This repository is being built incrementally. The first milestone is a local-first MVP using Java, Spring Boot, React, PostgreSQL with pgvector, Spring AI, and Ollama.

## Project principles

- Build the MVP before post-MVP integrations and agent features.
- Keep the application local-first and use free, self-hosted tooling where practical.
- Keep AI responses grounded in retrievable project evidence and distinguish facts from hypotheses.
- Never commit secrets, credentials, or real production data.

## Branching

`main` contains stable, runnable work. Development happens in short-lived branches named `feature/...`, `fix/...`, or `chore/...`, then returns to `main` through a pull request.
