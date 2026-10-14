# API and MCP Contracts — Veto

**Status:** Selected contract target. Implement and test against MCP specification 2025-11-25 or later over Streamable HTTP.

## Transport and client contract
The TypeScript MCP server uses the selected @modelcontextprotocol/sdk release that supports the required protocol revision. The web voice client is a genuine MCP client: it initializes through the protocol handshake, discovers tools through MCP, and invokes them over Streamable HTTP. Direct business-function calls or ordinary REST routes are not substitutes for MCP tool calls. The exact dependency version, browser support, CORS/session behavior, and Lambda HTTP adapter must be verified during implementation.

## Common tool result
Use the MCP protocol response shape. Structured results should include a stable data object containing request_id, status (ok / needs_confirmation / denied / error), operation data where appropriate, safe error code/message where needed, simulation boolean, and UTC timestamp. Where supported, expose machine-readable structured content and readable text content without duplicating sensitive data. Never return stack traces, secrets, or another user's data.

Identity must come from a trusted session/auth mechanism. A client-provided user_id is not authority. Every resource lookup checks ownership. Unknown/non-owned IDs must not enable enumeration.

## Tool catalogue
| Tool | Input / output | Rules |
|---|---|---|
| get_card_status | Optional supported alias → simulated status, masked demo alias, updated time | Read-only; own card |
| check_recent_activity | Bounded window/page size → owned synthetic summaries | Read-only |
| explain_transaction | Transaction ID → score/scale/risk band/model/version/evidence/limitations/explanation | Read/compute only; no auto-action |
| freeze_card / unfreeze_card | Resource, then pending intent → confirmation preview or simulated state + audit ID | Owner check; explicit confirmation; allowed transition |
| dispute_transaction | Transaction ID, reason enum, pending intent → simulated dispute | Confirmation and idempotency |
| trust_merchant / untrust_merchant | Merchant ID, scope enum, pending intent → preference + audit ID | Explicit scope and confirmation |
| get_decision_history | Bounded page size/cursor → user-scoped audit entries | Read-only |

## Confirmation protocol
Create a server-side pending intent with opaque ID, action, resource, scope, actor, and creation/expiry. Confirm by referencing that intent. Revalidate identity, ownership, expiry, scope, current state, and idempotency immediately before mutation. Client booleans and LLM statements are not confirmation evidence. Cancel has no side effect; stale, reused, or mismatched intents are rejected.

## Errors
INVALID_ARGUMENT, UNAUTHENTICATED, NOT_FOUND_OR_NOT_OWNED, ACTION_NOT_ALLOWED, CONFIRMATION_REQUIRED, CONFIRMATION_EXPIRED, STATE_CONFLICT, IDEMPOTENCY_CONFLICT, SCORING_UNAVAILABLE, EXPLANATION_UNAVAILABLE, PERSISTENCE_UNAVAILABLE, RATE_LIMITED, INTERNAL_ERROR.

Version contracts before external integration. Keep schema examples and tests. Validate requests/responses at each boundary. Breaking changes update server, web voice client, scoring service, fixtures, tests, and docs together.
