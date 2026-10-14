# Product Requirements Document — Veto

**Status:** Initial specification. Reconcile with official hackathon rules, platform capabilities, and actual implementation.  
**Target:** Submit by 22 October 2026; stated official deadline is 23 October 2026, 12:00 PDT / 20:00 Lagos.

## Product thesis
Veto is a voice-first fraud decision-support agent that explains suspicious card activity in plain language and keeps the user in control of consequential actions. Tagline: **“Say no to fraud. Out loud.”**

## Problem and audience
Fraud models can produce a score without an understandable reason or clear next step. A voice interface can make a consequential action feel deceptively simple. Veto connects detection, evidence, explanation, user choice, and an auditable simulated result.

Primary user: a cardholder in a synthetic demo who wants to understand activity and choose a response. Secondary users: hackathon judges and developers assessing explainability, agent safety, and engineering quality.

Out of scope: live card networks, actual card freezes, real dispute filing, production fraud prevention, financial advice, real payment credentials, and real customer transaction histories.

## Core journey
1. User asks about recent activity or a specific demo transaction.
2. Server resolves trusted demo identity and retrieves only owned synthetic records.
3. Scoring returns risk estimate, model/version, timestamp, and structured evidence.
4. Veto explains what evidence supports, what is uncertain, and why the score is not proof of fraud.
5. User can inspect details in a dashboard.
6. User requests a simulated freeze/unfreeze, dispute, or merchant trust change.
7. Veto repeats the exact action/scope and asks for confirmation.
8. Server rechecks identity, ownership, state, expiry, and idempotency before writing.
9. Success is reported only after persistence is confirmed.
10. Decision history shows the simulated result.

## Goals
- Explain model evidence in voice and on screen.
- Separate model prediction, narrative explanation, and action authorization.
- Demonstrate constrained, typed MCP tools.
- Require explicit confirmation for consequential actions.
- Preserve inspectable user-scoped demo history.
- Ship a coherent, reproducible vertical slice with honest limitations.

## Functional requirements
| ID | Requirement | Priority | Acceptance |
|---|---|---:|---|
| FR-01 | Resolve demo identity | P0 | Unknown identity denied; client user ID alone is not authority. |
| FR-02 | Recent activity | P0 | Only owned synthetic records, ordered by event time. |
| FR-03 | Explain transaction | P0 | Every factual reason maps to returned evidence; missing evidence is not invented. |
| FR-04 | Score transaction | P0 | Score scale, risk band, model/version, timestamp, evidence and limitations returned. |
| FR-05 | Request action | P0 | Exact action and scope previewed; awaits confirmation. |
| FR-06 | Confirm/cancel | P0 | Cancel has no side effect; confirmation revalidates server-side. |
| FR-07 | Persist action | P0 | History reflects successful simulated action; persistence failure is not success. |
| FR-08 | Dashboard | P0 | Shows transaction, risk label, evidence, action state, simulation disclosure. |
| FR-09 | Decision history | P1 | User-scoped timestamped action history. |
| FR-10 | Cross-session memory | P1 | Minimal approved state only; isolation and deletion documented. |
| FR-11 | Merchant trust | P1 | Explicit scope and confirmation; simulation disclosed. |
| FR-12 | Scenario simulator | P1 | Synthetic inputs; cannot bypass normal authorization. |
| FR-13 | Accessibility | P0 | Text/icon as well as color; keyboard focus/navigation. |
| FR-14 | Graceful failure | P0 | Model, LLM, or storage failure never fabricates score or success. |

## Non-functional requirements
Security: server-side authorization, strict schemas, minimal permissions, secret hygiene. Explainability: distinguish facts, model contributions, and interpretation. Reliability: deterministic fixtures, idempotent writes. Accessibility: semantic labels, contrast, keyboard use, responsive layout. Cost: no expensive resources without owner approval. Portability: simulator can exercise the same client-independent contracts if actual Alexa+ integration is unavailable.

## Voice and interaction
Lead with result, then strongest evidence, then a safe next step. Avoid “fraud confirmed” based only on a score. Ask one confirmation question at a time. Ambiguous “yes”, cancellation, or timeout must not mutate state. Clearly say “demo card” or “simulated action” unless a verified authorized external integration exists.

## Success evidence
Demonstrate: a complete explanation; denied cross-user access; cancellation with no state change; confirmed simulated action in history; safe model/storage failure; accessible risk labels; and a documented evaluation if a model is trained. Numeric targets require a documented dataset, baseline, protocol, and measurement.

## Risks
Alexa+/MCP feasibility and rules require official-source verification. Dataset license/features require review. USD-to-NGN conversion is display-only and needs a dated source. Synthetic-data performance does not establish live-world performance. Deployment needs least privilege, cost bounds, and teardown.

## Definition of done
Acceptance criteria met; relevant tests pass; implementation reviewed; security implications addressed; docs match actual behavior; submission includes setup, architecture, demo script, known limitations, data/license provenance, and simulation disclaimer.
