# Technical Requirements Document — Veto

**Status:** Selected architecture. Implementation and service availability still require engineering verification; this document does not claim deployed functionality.

## 1. Locked stack and deployment targets

| Layer | Selected implementation |
|---|---|
| MCP server | TypeScript, selected @modelcontextprotocol/sdk package pinned to a compatible release |
| MCP protocol | 2025-11-25 or later, Streamable HTTP |
| Voice client | Web client using a real MCP Client + Streamable HTTP transport, with voice input/output |
| Scoring | Python FastAPI, adapted to AWS Lambda with Mangum |
| AWS MCP endpoint | AWS Lambda with an HTTP front door/adapter compatible with Streamable HTTP |
| Persistence | Amazon DynamoDB, single-table design |
| Narration | Amazon Bedrock Nova Lite by default; Claude Haiku optional when configured |
| Voice output | Amazon Polly in AWS mode |
| Local development | Local MCP HTTP server, FastAPI/uvicorn, local persistence/dev adapter, browser voice adapter, deterministic narration fallback |

The web client connects to Veto's MCP server. It is not a live Alexa+ assistant integration: the hackathon FAQ states that gated Alexa+ developer tools are unavailable to participants and permits a web-based simulated experience. The self-hosted MCP server remains the actual primary-track technical surface.

## 2. Dataset and model — decision locked

Use Kaggle's Sparkov-generated credit-card transaction dataset with the fraudTrain and fraudTest files, subject to the documented dataset-terms gate before import/redistribution. Raw datasets must not be committed to Git.

The selected engineered features are:
- amount_vs_user_median
- distance_from_home_km
- hour
- is_night
- is_new_merchant
- txn_count_last_1h
- mins_since_last_txn
- category

Build or reuse the stacking ensemble of logistic regression, random forest, and XGBoost from the existing Ensemble repository; use SHAP TreeExplainer for model-contribution evidence. Audit repository artifacts, training provenance, feature order, preprocessing, threshold, and evaluation before reuse. No model metric may be claimed without a reproducible evaluation artifact.

Feature engineering must be time-safe:
- Calculate user medians and merchant novelty from transactions available before the transaction being scored.
- Sort per-user events chronologically before computing rolling one-hour counts and time-since-last-transaction.
- Never include the fraud label, post-event information, future transactions, names, addresses, or raw card identifiers as model features.
- Keep the provided test file as a held-out final evaluation set; never tune thresholds or preprocessing against the final test result.
- Treat category as categorical data using a documented training-only encoding pipeline.
- Generate a pseudonymous demo-user key; do not persist/display the source dataset's raw card number.
- Record feature provenance, missing-value handling, preprocessing, split strategy, model version, calibration status, and limitations.

SHAP contribution is evidence about model output, not causal proof. If an input/feature cannot support an honest user-facing statement, label it as opaque rather than inventing a plain-language meaning.

## 3. MCP server and client

The MCP server registers a small, typed tool allowlist: get_card_status, check_recent_activity, explain_transaction, freeze_card, unfreeze_card, dispute_transaction, trust_merchant, untrust_merchant, and get_decision_history. All tool input schemas are strict and bounded.

The web voice client must:
- instantiate an MCP Client using the selected TypeScript SDK;
- connect via StreamableHTTP transport to the self-hosted MCP endpoint;
- complete the MCP initialization/capability handshake and use MCP tool discovery/call operations;
- not call hidden business functions directly as a substitute for MCP;
- display connection/error state and use server responses as the source of truth;
- support typed text fallback when speech recognition is unavailable;
- distinguish user confirmation from generated or quoted text.

Browser-to-server connectivity must handle CORS/allowed origins, session scope, authentication, MCP protocol/session headers, cancellation, and transport errors. Never expose AWS credentials to the browser. If the selected package's browser/runtime support requires a same-origin backend adapter, that adapter must preserve real MCP protocol traffic and be documented—not silently downgrade to ordinary REST calls.

## 4. Authorization and state-changing actions

Server-side authorization, resource ownership, short-lived pending intents, explicit confirmation, expiry, and idempotency are required. A client boolean or LLM statement is not proof of confirmation. Recheck identity, ownership, action scope, current state, expiry, and idempotency immediately before mutation. Cancellation and ambiguous confirmation have no state-changing effect. Every result and UI state clearly labels the action as simulated.

## 5. FastAPI scoring service

The local FastAPI application runs through Uvicorn. The deployed scoring handler is adapted for Lambda using Mangum. It validates normalized transaction fields and returns:
- score and explicit scale;
- risk band and threshold/version metadata;
- model ID/version and scored timestamp;
- structured contribution evidence;
- calibration state and limitations.

The scoring endpoint must fail safely when artifacts, feature values, or preprocessing are unavailable. The exact scoring schema is shared by local client, MCP server, tests, and deployed Lambda.

## 6. DynamoDB single-table design

DynamoDB is the selected AWS persistence target. Define a single-table access-pattern document before implementing the schema. Use composite partition/sort keys to scope transactions, card state, pending action intents, merchant preferences, and audit history to a server-derived demo-user identity. Use conditional writes for state transitions and idempotency. Avoid client-controlled partition ownership and cross-user queries.

Local run must not require paid AWS resources. Provide a local adapter (in-memory or DynamoDB Local) implementing the same repository interface; AWS mode uses the DynamoDB repository. The test suite must run against the local adapter without cloud credentials.

## 7. Bedrock narration and Polly voice

Amazon Bedrock Nova Lite is the default AWS narration model; Claude Haiku is an optional configured alternative. Prompts contain only necessary synthetic transaction fields and structured evidence. Merchant strings are treated as untrusted data. The LLM summarizes evidence but cannot change the model score, invent features, decide authorization, or trigger an action without server-side checks.

When Bedrock is unconfigured or unavailable locally, use a deterministic evidence-based template. Amazon Polly is the AWS voice-output adapter; local development uses a local/browser voice adapter so core flows remain runnable without AWS credentials. A voice-service failure must not block inspection or turn into a fabricated success.

## 8. Lambda/HTTP runtime

AWS Lambda is the selected target for the MCP HTTP endpoint and FastAPI scoring service. Use an HTTP adapter compatible with MCP Streamable HTTP semantics and validate request/response content types, MCP session behavior, cancellation, and any required streaming endpoints against the chosen Lambda front door. Mangum adapts FastAPI; it is not the MCP transport by itself.

Local and AWS entry points should share tool schemas and application services. Local execution must work using documented environment variables and no AWS credentials; AWS mode is opt-in/configured separately. Any deployment requires a cost review, least-privilege IAM, safe logging, and teardown instructions.

## 9. Contracts and failure behavior

Use versioned JSON contracts and UTC timestamps. Money requires explicit currency and decimal-safe representation. Missing data remains unknown rather than zero. Use stable errors: INVALID_ARGUMENT, UNAUTHENTICATED, NOT_FOUND_OR_NOT_OWNED, ACTION_NOT_ALLOWED, CONFIRMATION_REQUIRED, CONFIRMATION_EXPIRED, STATE_CONFLICT, IDEMPOTENCY_CONFLICT, SCORING_UNAVAILABLE, EXPLANATION_UNAVAILABLE, PERSISTENCE_UNAVAILABLE, RATE_LIMITED, INTERNAL_ERROR.

Invalid arguments are rejected; non-owned resources do not leak existence; scoring failure yields no invented score; Bedrock failure uses template fallback; persistence failure never reports success; duplicate writes return a prior idempotent result or safe conflict; authorization ambiguity denies.

## 10. Quality and release criteria

Tests must cover model/schema contracts, time-safe features, two-user isolation, forged/expired/replayed confirmation, prompt-injection merchant strings, cancellation, successful simulated freeze, persistence failure, and local no-cloud execution. Test AWS adapters separately when configured. Track precision, recall, PR-AUC, confusion matrix and threshold trade-offs, calibration status, false positives, and false negatives where supported. Synthetic performance does not prove real-world fraud performance.
