# Technical Requirements Document — Veto

**Status:** Proposed. Update when verified platform constraints or repository evidence changes the design.

## System boundaries
1. Voice/client adapter: actual Alexa+ integration only if verified; otherwise clearly labelled simulator.
2. TypeScript MCP server with a narrow allowlist of typed tools.
3. Python scoring service for training, inference, and structured evidence.
4. Explanation adapter that verbalizes supplied evidence without inventing facts.
5. Persistence for synthetic transactions, simulated state, and audit history.
6. React dashboard for inspection.
7. AWS deployment only after service support, cost, permission, and teardown review.

## Technology direction
TypeScript/MCP, Python model service, React + TypeScript dashboard, AWS where demonstrably useful. Lambda, Bedrock, DynamoDB, FastAPI, Lambda Function URL, and AgentCore are candidates, not confirmed deployed choices. Choose the smallest architecture that can be tested and demonstrated.

## MCP server requirements
- Strict input schemas and bounded strings/arrays/enums.
- Identity from a trusted session/auth mechanism.
- Ownership and action authorization at the server/data boundary.
- Server-issued short-lived pending intent for consequential actions.
- Idempotency and conditional writes for mutations.
- Request IDs and stable safe error codes.
- No LLM-controlled authorization, arbitrary SQL, shell, unrestricted URL fetch, or generic write capability.

## Scoring service requirements
- Validate normalized transaction schema, units, ranges, and missing values.
- Return score, explicit scale, risk band, model/version, timestamp, calibration status, evidence, and limitations.
- Fail safely on invalid input, model-load failure, or inference failure.
- Never return arbitrary filesystem paths, raw training data, or secrets.

## Explanation adapter
Receives minimum required transaction fields and structured evidence. Produces a short summary, supporting factors, uncertainty, and safe next step. Merchant descriptions and model output are untrusted data. Narrative cannot change score, invent factors, or authorize tools. Deterministic template fallback is acceptable.

## Persistence
Use a stable server-derived user partition. Store only synthetic data. Keep audit events append-oriented where practical. Use conditional writes/version checks. Provide fixtures, reset path, and documented deletion/retention behavior. Do not store unnecessary raw prompts.

## Contracts
Use versioned JSON across boundaries and ISO 8601 UTC timestamps. Money must use explicit currency and decimal-safe representation. Scores require declared scale and calibration metadata. Missing values remain unknown, not zero. Validate both requests and responses at service boundaries.

## Model pipeline
1. Verify source, license, permitted use, redistribution, feature definitions, and target.
2. Keep raw data out of Git unless explicit terms permit it.
3. Split data before fitting preprocessing or resampling; resample inside training folds only.
4. Review target leakage, post-event features, identifiers, and duplicates.
5. Compare a simple baseline before accepting an ensemble.
6. Report precision, recall, PR-AUC, confusion matrix at selected threshold, false-positive/negative trade-offs, and calibration where relevant.
7. Use held-out test data once for final evaluation.
8. Version preprocessing, feature order, model artifact, provenance, and evaluation metadata.
9. Explanations must align with the exact model and feature vector scored.
10. State that synthetic-data performance does not establish real-world performance.

## Failure behavior
Invalid arguments rejected before downstream calls. Unknown/non-owned resources get non-enumerating denial. Scoring failure produces no invented score. LLM failure uses evidence-based template or safe fallback. Persistence failure never reports success. Duplicate writes return prior result or safe conflict. Authorization ambiguity denies.

## Operations
Structured logs: request ID, operation, status, duration, non-sensitive error code. Least-privilege IAM. Separate dev/test/demo configuration. Document local run, tests, deploy, teardown, and recovery before public exposure. Never claim production readiness without independent review and real-world validation.
