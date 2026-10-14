# Veto
### Say no to fraud. Out loud.

**Veto is a voice-first fraud decision-support prototype that explains suspicious card activity in plain language and asks before taking consequential action.**

> A hackathon prototype, not a bank, card issuer, payment processor, or live fraud-prevention service.

Veto is being built for the Amazon Developer Hackathon 2026. The intended experience combines a voice-oriented assistant, an explainable fraud-scoring service, explicit user confirmation for consequential actions, and a compact dashboard that makes the evidence inspectable.

## What we are building

- **Ask:** a user asks what happened on their card or about a particular transaction.
- **Inspect:** Veto retrieves only the demo user's authorized transaction records and scoring evidence.
- **Explain:** it presents the model's risk estimate and the evidence behind it, distinguishing evidence from inference.
- **Choose:** the user can request a simulated action such as freeze, dispute, or trust a merchant.
- **Confirm:** consequential actions require explicit confirmation and server-side authorization.
- **Remember:** the demo can retain a user-scoped decision history, with clear boundaries and deletion behavior.

## Project status

**Phase:** foundation and specification.  
**Implementation status:** features are planned until code and tests demonstrate otherwise.  
**Current repository:** documentation-first bootstrap; no functioning fraud-scoring or Alexa+ integration is claimed yet.

See [the product requirements](docs/PRD.md), [technical design](docs/TRD.md), and [architecture](docs/ARCHITECTURE.md) for the source of truth.

## Principles

1. **Evidence before eloquence.** The language model can explain supplied evidence; it must not invent transaction facts, model features, or completed actions.
2. **Human control for consequential actions.** Freeze, unfreeze, dispute, and merchant-trust changes require confirmation in the prototype.
3. **Secure by boundary.** Authentication, resource ownership, authorization, idempotency, and auditability are server responsibilities—not prompt instructions.
4. **Honest simulation.** A simulated state change must never be represented as a real bank or card action.
5. **Useful, not theatrical.** The interface should feel like a considered financial product, not a generic AI chat demo.
6. **Accessible risk communication.** Risk uses labels and icons as well as color.
7. **Small enough to ship.** Prefer one complete, testable end-to-end story over a broad collection of unfinished integrations.

## Intended technical direction

- TypeScript MCP server exposing narrowly scoped tools.
- Python scoring service for model inference and structured evidence.
- A documented model-training/evaluation pipeline using appropriately licensed or synthetic data.
- AWS-first deployment, subject to a verified low-cost path and current service constraints.
- A React dashboard and a client-independent simulator if a real Alexa+ integration cannot be completed and verified in time.

The exact hosting choice, dataset, model, integrations, and deployment topology remain decisions to validate. Do not treat this direction as evidence that those services are already configured.

## Development workflow

- Work on short-lived feature branches.
- Open pull requests for review and merge only after checks and acceptance criteria are satisfied.
- Record meaningful architecture choices in `docs/decisions/`.
- Keep the build journal evidence-based: completed work must link to a commit, test, screenshot, or other artifact.
- Never commit credentials, real payment-card data, customer data, or downloaded datasets without approved licensing and handling rules.

## Repository map

- `docs/PRD.md` — users, product scope, journeys, requirements, and acceptance criteria.
- `docs/TRD.md` — technical requirements and implementation constraints.
- `docs/ARCHITECTURE.md` — components, trust boundaries, and data flows.
- `docs/API_CONTRACTS.md` — tool and service contracts.
- `docs/DATA_DICTIONARY.md` — canonical transaction, score, explanation, and action fields.
- `docs/DESIGN_SPEC.md` — visual system, interaction rules, and accessibility.
- `docs/SECURITY_MODEL.md` and `docs/THREAT_MODEL.md` — security requirements and abuse cases.
- `docs/PRIVACY_AND_COMPLIANCE.md` — data minimization, licensing, and compliance questions to verify.
- `docs/TEST_STRATEGY.md` — test layers and release gates.
- `docs/DEPLOYMENT_RUNBOOK.md` and `docs/DEMO_SCRIPT.md` — deployment and truthful demonstration.
- `docs/BUILD_JOURNAL.md` and `docs/FRICTION_LOG.md` — evidence of progress and real blockers.

## Before contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md), [SECURITY.md](SECURITY.md), and [AGENTS.md](AGENTS.md). Treat all requirements and architecture decisions as reviewable proposals until validated against the actual hackathon rules, dataset terms, and AWS/Alexa+ capabilities.

## License

The project code is intended to use the MIT License. That license does **not** automatically grant rights to datasets, third-party assets, model weights, or services.