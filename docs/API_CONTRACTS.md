# API and MCP Contracts — Veto

**Status:** Contract proposal; validate against the selected MCP SDK and hosting integration before implementation.

## Common response
Every tool returns request_id, status (ok / needs_confirmation / denied / error), operation data where appropriate, stable error code and safe message where needed, simulation boolean, and ISO 8601 UTC timestamp. Never return stack traces, secrets, or another user's data.

Identity comes from a trusted session/auth mechanism. A client-provided user_id is not authority. Every resource lookup checks ownership. Unknown and non-owned IDs must not enable enumeration.

## Tool catalogue
| Tool | Input | Output | Side effect / rule |
|---|---|---|---|
| get_card_status | Optional supported card alias | Simulated status, masked demo alias, updated time | Read-only; own card only |
| check_recent_activity | Bounded window/page size | Owned synthetic transaction summaries | Read-only; no raw model/training payload by default |
| explain_transaction | Transaction ID | Score, scale, risk band, model/version, evidence, limitations, explanation | Read/compute only; never auto-act |
| freeze_card / unfreeze_card | Resource alias, then pending intent reference | Pending confirmation or confirmed simulated state + audit ID | Explicit confirmation, owner check, valid transition |
| dispute_transaction | Transaction ID, reason enum, pending intent | Pending intent or simulated dispute + audit ID | Confirmation and idempotency |
| trust_merchant / untrust_merchant | Merchant ID, scope enum, pending intent | Preference state + audit ID | Explicit scope and confirmation |
| get_decision_history | Bounded page size/cursor | User-scoped audit entries | Read-only |

## Confirmation protocol
First create a server-side pending intent containing random opaque ID, action, resource, scope, actor, created/expiry time. Then confirm by referencing that intent. Revalidate identity, ownership, expiry, scope, current state, and idempotency immediately before mutation. Generic client booleans and LLM statements are not confirmation evidence. Cancellation has no side effect; expired, mismatched, stale, or reused intents are rejected.

## Error codes
INVALID_ARGUMENT, UNAUTHENTICATED, NOT_FOUND_OR_NOT_OWNED, ACTION_NOT_ALLOWED, CONFIRMATION_REQUIRED, CONFIRMATION_EXPIRED, STATE_CONFLICT, IDEMPOTENCY_CONFLICT, SCORING_UNAVAILABLE, EXPLANATION_UNAVAILABLE, PERSISTENCE_UNAVAILABLE, RATE_LIMITED, INTERNAL_ERROR.

## Versioning
Version contracts before external integration. Keep JSON examples/schema tests. Validate requests and responses at each boundary. Breaking changes must update server, simulator, dashboard, fixtures, tests, and docs together.
