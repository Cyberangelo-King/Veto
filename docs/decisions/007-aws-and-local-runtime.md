# ADR 007 — AWS deployment architecture with local parity

- **Status:** Accepted
- **Date:** 2026-10-14
- **Decision owner:** Product owner

## Context
Veto is entering the AWS Builder mini-challenge, but local development must stay possible on constrained hardware and must not require ongoing AWS spend for ordinary testing.

## Decision
The target AWS deployment is:
- AWS Lambda for the TypeScript MCP HTTP endpoint.
- Python FastAPI scoring service deployed to Lambda through Mangum.
- Amazon DynamoDB using a single-table design for user-scoped synthetic transactions, demo card state, action intents, merchant preferences, and audit history.
- Amazon Bedrock with Nova Lite as the default evidence-grounded narration model.
- Claude Haiku as an optional, explicitly configured alternative for narration.
- Amazon Polly for voice output in AWS mode.

Local mode is a first-class requirement, not an afterthought:
- Run the TypeScript MCP server and its Streamable HTTP endpoint locally.
- Run FastAPI with Uvicorn without Mangum.
- Use an in-memory repository or DynamoDB Local behind the same persistence interface.
- Use deterministic evidence-grounded template narration when Bedrock credentials/service access are unavailable.
- Use a local/browser speech adapter when Polly is not configured.
- Keep the same MCP tool schemas, authorization checks, confirmation rules, idempotency, and audit behavior in local and AWS modes.

## Consequences
- The implementation should have clear adapters for persistence, narration, and voice.
- Local mode must run with no AWS credentials and no paid cloud resource.
- AWS mode requires least-privilege IAM, service/model availability checks, budget/cost review, safe logging, and teardown.
- Lambda's HTTP front door must be tested for MCP Streamable HTTP compatibility, including content types, session behavior, and streaming semantics. Mangum adapts FastAPI; it is not itself the MCP HTTP transport.
- No feature or service is considered deployed until it is configured, exercised, and verified. The AWS Builder claim must describe the integrations actually demonstrated.

## Revisit
Revisit only if the selected service path cannot meet the MCP/latency/cost requirements, a service is unavailable in the target account/region, or an evaluation demonstrates a safer and more practical path.
