# Lantern Suite — Product Overview

Lantern Suite currently consists of three named layers/products: **Lantern Core**, **Lanternkeeper**, and **Lanternfall**.

This is a public portfolio description. It intentionally describes capabilities and engineering direction without publishing the proprietary source or internal implementation.

## Lantern Core

Lantern Core is the shared framework used by the suite.

Its purpose is to centralize reusable infrastructure such as:

- Local AI provider integration
- Structured model responses
- Authoritative state and persistence
- Rules/tabletop primitives
- Permission-aware data delivery
- Shared validation and testing

Keeping these systems in a shared layer allows Lanternkeeper and Lanternfall to remain separate applications without duplicating their core infrastructure.

## Lanternkeeper

Lanternkeeper is a **private AI copilot and full virtual tabletop for human game masters**.

The product is designed around the idea that the GM remains authoritative. AI can assist with planning, interpretation, suggestions, content generation, and table support, but consequential changes can remain previewable and reviewable before they affect shared state.

Current/implemented system areas include:

- Role-specific GM, display, desktop-player, and mobile-player clients
- Authoritative maps and tokens
- Movement and collision
- Doors, lighting, line-of-sight, and fog-of-war systems
- Terrain and movement-cost handling
- Initiative and turn state
- Dice and lightweight conditions/meters
- Handouts and journal-style artifacts
- Drawings, pings, templates, and measurement tools
- Campaign backup/recovery workflows
- Private/public/player-scoped information boundaries

The product is still in development; the public repository should not be interpreted as a final feature list or release commitment.

## Lanternfall

Lanternfall is a **local AI-driven adventure simulator** designed for solo play first and group play second.

Where Lanternkeeper supports a human GM, Lanternfall is oriented around persistent AI-assisted adventure play. It is being designed as a stateful application rather than a disposable chat session, allowing world, character, rules, and adventure context to persist as part of the application's authoritative state.

Lanternfall shares Lantern Core infrastructure but has its own application boundary and can be built/distributed independently from Lanternkeeper.

## Shared Design Goals

Across the suite, the product direction emphasizes:

- Local/private model inference where practical
- Persistent, authoritative application state
- Structured and validated AI output
- Clear permission boundaries
- Recoverable and replayable state changes
- System-neutral tabletop/rules infrastructure
- Independent packaging of products built on shared foundations

## Development Status

Lantern Suite is **actively under development** and is not yet being presented as a finished commercial release.

The private codebase contains substantial implemented infrastructure and automated testing, while higher-level product workflows, rules support, user experience, and AI-assisted features continue to evolve.

Public screenshots, walkthroughs, and sanitized demonstrations will be added here once the interfaces are ready for portfolio presentation.

## Proprietary Status

Lantern Suite is proprietary software in development with potential commercial-release intent. This showcase exists to communicate the technical work publicly without releasing the product source code or exposing implementation details that would allow the applications to be cloned from GitHub.
