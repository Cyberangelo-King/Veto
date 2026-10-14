# Veto
### Say no to fraud. Out loud.

**Veto is a voice-first fraud decision-support prototype that connects transaction scoring to evidence, plain-language explanation, and user-controlled simulated actions.**

> Veto is a hackathon prototype. It is not a bank, card issuer, payment processor, or live fraud-prevention service.

## Product direction

Veto is targeting the **Alexa+ track**, together with the **AWS Builder** and **Open Source** mini-challenges. The project is designed around a self-hosted MCP server and a web voice client that connects to it as a real MCP client. It is not presented as a live connection into the Alexa+ assistant.

The hackathon FAQ says the gated Alexa+ developer tools are preview-only and unavailable to hackathon participants. The official rules permit a simulated Alexa+ experience via a web front end; Veto's selected approach goes further by exposing an actual MCP server and exercising its tools over Streamable HTTP from the web client.

Official references:
- [Hackathon rules](https://amazonappdev2026.devpost.com/rules)
- [Hackathon FAQ](https://amazonappdev2026.devpost.com/details/faqs)
- [Official TypeScript MCP SDK](https://github.com/modelcontextprotocol/typescript-sdk)

## Locked technical decisions

These are the selected implementation decisions; they do not mean the application or AWS resources already exist.

- **Dataset:** Kaggle's Sparkov-generated credit-card transaction dataset, using fraudTrain and fraudTest. Raw files stay out of Git. Dataset terms, exact source/version, provenance, and the permitted use of derived artifacts must be recorded before importing data.
- **Features:** amount_vs_user_median, distance_from_home_km, hour, is_night, is_new_merchant, txn_count_last_1h, mins_since_last_txn, and category.
- **Model:** stacking ensemble of logistic regression, random forest, and XGBoost based on the existing [Ensemble repository](https://github.com/Cyberangelo-King/Ensemble-Machine-Learning-for-Online-Credit-Card-Fraud-Detection), with SHAP TreeExplainer for contribution evidence. Reuse must preserve feature-order/version consistency and be backed by an evaluation report.
- **MCP:** self-hosted TypeScript MCP server, MCP spec version 2025-11-25 or later, Streamable HTTP, using the selected @modelcontextprotocol/sdk package at a compatible pinned version.
- **Voice client:** a web voice interface that instantiates a real MCP client, connects to Veto's Streamable HTTP endpoint, discovers/calls tools through MCP, and presents speech input/output. This is not a direct Alexa+ assistant connection.
- **AWS target:** Lambda for the MCP endpoint and FastAPI scoring service (using Mangum for Lambda adaptation), DynamoDB single-table persistence, Amazon Bedrock for evidence-grounded narration (Nova Lite by default; Claude Haiku as an optional configured alternative), and Amazon Polly for voice output.
- **Local development:** the MCP server, scoring API, and web client must run locally. AWS integrations are optional in local mode; use explicit local persistence/dev adapters and deterministic evidence-based narration/browser speech fallbacks when AWS credentials or services are not configured. Local mode must exercise the same tool contracts and action-safety rules.

Read [ADR 005: dataset and model](docs/decisions/005-dataset-and-model.md), [ADR 006: MCP client and transport](docs/decisions/006-mcp-client-and-transport.md), and [ADR 007: AWS and local runtime](docs/decisions/007-aws-and-local-runtime.md).

## Core experience

1. Ask Veto about recent synthetic card activity.
2. Inspect a transaction and its risk score, model metadata, evidence, and limitations.
3. Get an explanation grounded in the model's actual output.
4. Test a prompt-injection string embedded in merchant text; Veto treats it as data, not an instruction.
5. Request a demo-card freeze, cancel it, and verify there is no state change.
6. Request the freeze again, explicitly confirm, and verify the simulated state and decision history change.

All card and merchant actions remain simulated. They must never be described as real bank or card-network actions.

## Status

**Current state:** documentation and workflow foundation. The product code, model service, MCP endpoint, web client, and AWS resources are not yet claimed to be implemented or deployed. Features become complete only when code, tests, and a reproducible demo prove them.

The submission checklist is in [docs/SUBMISSION_CHECKLIST.md](docs/SUBMISSION_CHECKLIST.md). The demo must remain below the official three-minute video limit; Veto's target script is capped at 2 minutes 50 seconds.

## Design principles

- Evidence before eloquence: the language model may explain evidence, not invent it.
- Human control: consequential actions need explicit, server-verified confirmation.
- Secure by boundary: prompts do not replace authorization, validation, or ownership checks.
- Honest simulation: every demo action is explicitly simulated.
- Accessible risk communication: text/icons accompany red, amber, and green indicators.
- Deliberate visual identity: a restrained charcoal/slate foundation, careful typography, amber attention, green lower-risk, and red high-risk/blocked states. Avoid generic AI-dashboard patterns and decorative filler.

## Development workflow

- Use short-lived branches and a pull request for review.
- Keep decisions in docs/decisions and evidence in docs/BUILD_JOURNAL.md.
- Test denial, cancellation, replay, and failure paths alongside the happy path.
- Never commit credentials, real payment-card data, private customer data, or raw datasets unless the rights and handling policy explicitly permit it.
- Do not add app code in a documentation-only change.

## Repository map

- docs/PRD.md — product requirements and acceptance criteria.
- docs/TRD.md — locked implementation stack and technical constraints.
- docs/ARCHITECTURE.md — components, trust boundaries, and data flow.
- docs/API_CONTRACTS.md — MCP tool contracts.
- docs/DATA_DICTIONARY.md — transaction, score, evidence, and action fields.
- docs/DESIGN_SPEC.md — visual system and accessibility.
- docs/SECURITY_MODEL.md and docs/THREAT_MODEL.md — security controls and abuse cases.
- docs/TEST_STRATEGY.md — test layers and release gates.
- docs/DEMO_SCRIPT.md and docs/SUBMISSION_CHECKLIST.md — demo and submission requirements.
- docs/PRIVACY_AND_COMPLIANCE.md and docs/research/ — data handling and evidence-based research notes.
- docs/BUILD_JOURNAL.md and docs/FRICTION_LOG.md — actual work evidence and tool friction.

## Before contributing

Read CONTRIBUTING.md, SECURITY.md, and AGENTS.md. Requirements describe intended behavior until verified by working implementation and tests.

## License

The repository's source code is licensed under the standard MIT License in LICENSE, with copyright © 2026 Faith Akinola Boyejo. **That license does not automatically cover datasets, trained model artifacts, third-party code, fonts, icons, images, brand assets, or external services.** Each retains its own applicable license and terms. The Sparkov dataset and the origin/rights of model artifacts must be documented separately. Do not redistribute raw data or artifacts until permitted use is verified.
