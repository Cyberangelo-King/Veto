# Architecture — Veto

**Status:** Proposed logical architecture, not evidence of deployed resources.

## Logical view
Voice client or clearly labelled simulator → TypeScript MCP server (schema validation, identity, ownership, confirmation, idempotency, audit) → Python scoring service and persistence boundary. Structured score/evidence passes to an explanation adapter (LLM or deterministic template), then back to client and dashboard. Dashboard consumes trusted server contracts; it does not decide authorization.

## Trust boundaries
1. Client/server: client arguments and user IDs are untrusted.
2. Orchestration/tools: only registered tools with strict schemas are callable.
3. Scoring/narrative: score and evidence are data, not instructions.
4. Persistence: all reads/writes are scoped to validated identity and resource ownership.
5. External model/cloud: server-side credentials, least privilege, minimal prompt data.
6. Scenario simulator: synthetic generation cannot bypass normal auth/action rules.
7. Repository/CI: dependencies, build scripts, Actions workflows, and artifacts are supply-chain boundaries.

## Read flow
Resolve identity → validate arguments → check ownership → fetch normalized transaction → score exact feature vector → attach model/version/evidence → generate evidence-grounded explanation → return structured result → render same evidence and limitations in UI.

## Consequential action flow
Request action → validate identity/ownership → create short-lived pending intent bound to actor/action/resource/scope → show exact action and ask confirm/cancel → revalidate identity, ownership, expiry, current state, and idempotency → conditional persistence update + audit event → report success only after persistence confirms. Every response/UI must state the action is simulated.

Cancellation, ambiguity, expired intent, mismatch, timeout, or persistence failure means no successful state change.

## Deployment choice
AWS candidates include Lambda, Bedrock, DynamoDB, and possibly AgentCore. The final topology is blocked on current service support, hackathon eligibility, permissions, complexity, and cost verification. A local/client-independent simulator should exercise the same contracts if actual Alexa+ integration is unavailable. Do not misrepresent simulator use as Alexa+ integration.

## Model boundary
Scoring owns numerical prediction. Narrative owns language only. It cannot change a score, invent evidence, claim causality from feature contributions, call a model score proof of fraud, or authorize an action.

## Isolation and audit
Partition records by server-derived user identity. Use at least two test users. Audit actor, action, resource, outcome, timestamp, request ID, and simulation status; omit secrets and unnecessary prompt text.

## Decisions to validate
Client integration; hosting path; dataset license/feature semantics; whether ensemble improves the baseline; and whether persistent storage is required for the first vertical slice. Record evidence and trade-offs in docs/decisions/.
