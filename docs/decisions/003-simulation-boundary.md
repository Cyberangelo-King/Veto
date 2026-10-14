# ADR 003 — Explicit simulation boundary

- Status: Accepted
- Date: 2026-10-14
- Owner: Product owner

## Context
No verified authorized card-issuer/payment-processor connection is established.

## Decision
Freeze, unfreeze, dispute, and merchant trust are simulated state changes. UI and voice disclose this. Server-side ownership, explicit confirmation, idempotency, and audit history are required. Never imply a real bank/card/network changed.

## Consequences
A safe end-to-end simulation is in scope. A future external adapter requires separate authorization, terms, security, and compliance review.

## Revisit
Only when legitimate integration, authorization, and review conditions exist.
