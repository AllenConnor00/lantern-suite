# Lantern Suite

**Public engineering showcase for a proprietary, local-first tabletop and adventure software suite.**

Lantern Suite is an in-development family of applications built around shared AI, state-management, rules, and tabletop infrastructure. The production source code is private while the products are developed for potential commercial release; this repository exists as a **public technical showcase** of the architecture, design goals, and engineering work behind the suite.

> **This repository does not contain the proprietary Lantern source code, model assets, campaign data, or implementation required to reproduce the products.**

## Products

### Lantern Core

The shared framework underneath the suite. Lantern Core centralizes reusable infrastructure so individual products can remain independently deployable rather than duplicating AI, persistence, rules, and state logic.

Key areas include:

- Local large-language-model integration
- Structured model output and validation
- Authoritative application and campaign state
- Event-based persistence and deterministic replay
- Rules and tabletop infrastructure
- Permission-aware information delivery
- Shared testing and validation infrastructure

### Lanternkeeper

A **private AI copilot and virtual tabletop for human game masters**.

Lanternkeeper is designed to support—not replace—the GM. It combines tabletop tools, campaign state, rules support, local AI assistance, and role-aware client views while keeping the GM in control of authoritative changes.

Current engineering areas include:

- GM, table-display, desktop-player, and mobile-player surfaces
- Maps, tokens, movement, visibility, fog, lighting, terrain, doors, and initiative
- Dice, conditions, handouts, drawings, measurements, and campaign recovery
- GM approval workflows for actions that require adjudication
- Permission-filtered projections so private campaign information is removed before it reaches unauthorized clients

### Lanternfall

A **local AI-driven adventure simulator**, designed for solo play first and broader group play second.

Lanternfall builds on the same shared infrastructure while remaining an independently distributable application. Its focus is persistent, state-aware interactive adventure play rather than a stateless prompt-and-response experience.

## Engineering Focus

Lantern Suite is intentionally built around a few principles that matter well beyond the tabletop use case:

### Local-first AI

The platform is designed to work with locally hosted language models through compatible inference APIs. Private campaign information does not need to be sent to a cloud-hosted model simply to use core AI functionality.

### Structured inference

Model output is treated as untrusted application input rather than free-form truth. AI-facing workflows use constrained, structured responses that can be validated before they affect authoritative state.

### Authoritative state and replay

The shared architecture uses event-based persistence with deterministic reconstruction, revision checks, idempotent operations, and transactional writes. This allows state changes to be auditable, recoverable, and resistant to stale or competing clients.

### Permission boundaries

Private information is filtered before serialization. Public, GM-only, and player/actor-scoped data are projected separately so hidden information is not merely concealed by the interface—it is omitted from unauthorized payloads.

### Independent products, shared infrastructure

Lanternkeeper and Lanternfall have separate application boundaries and can be built and distributed independently while consuming versioned shared infrastructure from Lantern Core.

## Technology

The current private implementation uses technologies including:

- **Rust** — authoritative backend and shared systems infrastructure
- **TypeScript / React** — application clients
- **SQLite** — local-first persistence and replayable state
- **llama.cpp / OpenAI-compatible local inference APIs** — local LLM integration
- **JSON Schema / structured output** — constrained AI responses
- **Playwright and automated Rust/TypeScript tests** — browser, integration, concurrency, and invariant testing

## Security & Reliability Work

Some of the engineering areas explored in Lantern include:

- Pre-serialization authorization and data minimization
- Optimistic concurrency and stale-client recovery
- Idempotent mutation handling
- Transactional persistence
- Bounded validation and fail-closed behavior
- Deterministic replay and recovery points
- Adversarial tests for hidden-data leakage
- Structured AI-output validation
- Independent client/server identity checks

These systems are part of a broader goal: make AI-assisted applications behave like reliable software systems rather than thin wrappers around a model call.

## Current Status

Lantern Suite is **actively in development**. The private development workspace documents implemented shared infrastructure and ongoing product milestones. Because production source is not published here, implementation and test claims cannot be independently reproduced from this showcase alone.

The private development workspace defines Rust and TypeScript verification, independent product builds, browser-based end-to-end tests, and local-model integration tests. The public showcase does not provide those test suites or independently reproducible results.

Public screenshots and product demonstrations will be added here when the interfaces are ready to represent the products publicly.

## Architecture Overview

A higher-level, non-proprietary architecture description is available in [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).

More detail about the individual products is available in [`docs/PRODUCTS.md`](docs/PRODUCTS.md).

## Why the Source Is Private

Lantern Suite is being developed with the intention of potential commercial release. This showcase is intentionally separated from the production repository so the engineering work can be discussed publicly without publishing the proprietary implementation or making the products clonable from GitHub.

## About

Lantern Suite is designed and developed by **Connor Allen**, a Computer Science graduate focused on artificial intelligence, cybersecurity, local LLM systems, and reliable data-driven applications.

- GitHub: `github.com/AllenConnor00`
- LinkedIn: `linkedin.com/in/connor-allen-4718a0134`

---

**Lantern Suite is proprietary software in development. This repository is documentation and portfolio material, not an open-source distribution of the product.**
