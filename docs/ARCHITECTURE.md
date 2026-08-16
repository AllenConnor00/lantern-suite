# Lantern Suite — Architecture Overview

This document describes the **public, non-proprietary architecture** of Lantern Suite. It intentionally omits implementation details, source code, internal schemas, private assets, and other material that would make the products reproducible from this repository.

## System Shape

Lantern Suite is organized as multiple independently deployable applications built on shared infrastructure:

```text
                    ┌──────────────────────┐
                    │     Lantern Core     │
                    │ shared infrastructure│
                    └──────────┬───────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
        ┌────────▼────────┐         ┌────────▼────────┐
        │  Lanternkeeper │         │   Lanternfall   │
        │ AI copilot/VTT │         │ AI adventure   │
        └─────────────────┘         └─────────────────┘
```

Lantern Core provides versioned shared systems while the released applications keep their own composition roots, application-specific behavior, and user interfaces.

## Shared Core Responsibilities

At a high level, the shared layer handles concerns such as:

- Authoritative campaign/application state
- Persistence and deterministic reconstruction
- Local AI provider integration
- Structured output validation
- Rules and tabletop primitives
- Permission-aware projections
- Shared validation and reliability controls
- Common test infrastructure

The goal is to keep reusable infrastructure reusable while preventing either product from becoming a hidden dependency of the other.

## Authoritative State

Lantern treats shared application state as authoritative server-managed state rather than allowing clients to independently mutate their own truth.

State-changing operations are designed around:

- Revision-aware writes
- Idempotent requests
- Transactional persistence
- Deterministic replay
- Explicit stale-client handling
- Validation before commit

This approach supports recovery, synchronization, multiplayer behavior, and a clear audit trail of meaningful state changes.

## Event-Based Persistence

The private implementation persists typed state changes and reconstructs current state by replaying validated events. The exact schemas and event definitions are proprietary, but the public design goals are straightforward:

1. A requested mutation is authenticated and validated.
2. The current revision is checked.
3. The operation is committed atomically.
4. The resulting event becomes part of durable history.
5. State can be deterministically reconstructed from that history.

Recovery workflows build on this model rather than relying only on opaque mutable snapshots.

## Permission-Aware Projections

A core design principle is that hidden information should not be shipped to clients that are not allowed to know it.

Lantern distinguishes among scopes such as:

- Public/table-visible information
- GM-only information
- Player/actor-scoped information

The server produces viewer-specific projections before serialization. This reduces the risk that sensitive campaign state is merely hidden in the interface while remaining available in network payloads or client memory.

## Local AI Integration

Lantern is designed around locally hosted language models through compatible inference APIs.

The AI layer is separated from authoritative state. Model responses are treated as candidate structured input and are validated before application logic can use them to affect persistent state.

Conceptually:

```text
User / GM intent
      │
      ▼
Application context
      │
      ▼
Local model provider
      │
      ▼
Structured response
      │
      ▼
Validation / policy
      │
      ▼
Preview or authoritative action
```

This separation makes it possible to use generative models without treating their output as trusted system behavior.

## Client Surfaces

Lanternkeeper currently targets multiple role-specific surfaces, including:

- GM Studio
- Clean shared-table display
- Desktop player view
- Mobile player view

Each surface consumes an appropriate projection rather than receiving a single complete campaign object and deciding locally what to hide.

Lanternfall has its own independently deployable client/server composition and consumes only the shared infrastructure it needs.

## Reliability Controls

The implementation includes engineering controls around areas such as:

- Concurrency conflicts
- Duplicate/retried requests
- Invalid or oversized state
- Hidden-data leakage
- Recovery and rollback
- Client/server identity mismatch
- Structured AI output
- Deterministic replay

Automated verification includes Rust and TypeScript tests, browser-based end-to-end flows, concurrency tests, generated invariants, and adversarial serialization checks.

## What Is Intentionally Not Published Here

This showcase does **not** publish:

- Production source code
- Internal event or database schemas
- Proprietary rules-processing implementation
- Prompt/system-instruction internals
- AI orchestration details sufficient to reconstruct the product
- Model assets
- Campaign data
- Private media
- Commercial product assets

The public architecture is meant to demonstrate engineering approach and technical depth without turning the portfolio repository into a redistributable copy of Lantern Suite.
