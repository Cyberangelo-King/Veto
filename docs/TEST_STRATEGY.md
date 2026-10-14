# Test Strategy — Veto

## Layers
**Unit:** schemas, amount/currency formatting, risk-band mapping, preprocessing, explanation formatting, pending-intent expiry/scope, idempotency and state transitions.

**Contract:** MCP request/response schemas, scoring schema/model metadata, stable errors, UI states.

**Integration:** owned transaction read; score→evidence→explanation; confirmation→conditional simulated mutation→audit history; template fallback on LLM failure; persistence failure never reports success; reset/reseed determinism.

**Security:** unknown user denied; user A cannot read/write user B; forged/expired/reused/mismatched intent denied; prompt injection does not trigger tools; owner ID cannot bypass auth; sensitive sentinels absent from logs; malicious merchant text renders safely; malformed/oversized input rejected; retries do not duplicate actions.

**Model:** split before fitting/resampling; resampling only inside training folds; baseline comparison; leakage review; precision/recall/PR-AUC/confusion matrix/threshold trade-offs; calibration or explicit unknown; explanations match model/version/feature vector; claims link to evaluation artifacts.

**End-to-end:** recent activity; inspect/explain transaction; cancel action and prove no change; confirm simulated action and prove history; induce controlled scoring/persistence failure; show simulation disclosure.

## Fixtures
At least two isolated users; low/review/high examples; missing feature; malicious merchant text; duplicate/expired intent; scoring and persistence failure. Expected labels are test scenario expectations, not real-world ground truth.

## Release gates
Blocking: cross-user access, forged confirmation, fabricated evidence, secret leak, false real-action claim, unsafe write during failure, or undemonstrable P0 journey. Optional Alexa+ integration may be non-blocking only if simulator uses the same tested contracts and submission states the limitation honestly.

## Evidence
Record command, environment, date, result, and artifact/commit. Do not say “all tests pass” unless all relevant tests actually ran. Performance results need reproducible method and assumptions.
