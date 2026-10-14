# ADR 001 — Documentation-first bootstrap

- Status: Accepted
- Date: 2026-10-14
- Owner: Product owner

## Context
The repository was empty and external integration/data assumptions remain unverified. Unbounded implementation risks rework under a short deadline.

## Decision
Establish requirements, technical boundaries, contracts, data dictionary, design direction, security model, test strategy, and demo plan before broad implementation. Create actionable issues and implement one end-to-end vertical slice first.

## Consequences
Docs define intended behavior but do not imply code exists. Work proceeds through small PRs with explicit acceptance criteria. Avoid features outside the core journey.

## Revisit
When dataset, client integration, and deployment evidence support concrete implementation decisions.
