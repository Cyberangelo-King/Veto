# ADR 004 — Separate scoring from explanation

- Status: Accepted
- Date: 2026-10-14
- Owner: Product owner

## Context
An LLM can make opaque model output sound more certain or interpretable than it is.

## Decision
Scoring returns score, model/version metadata, and structured evidence. Explanation verbalizes only supplied evidence and states uncertainty/limitations. Prediction, explanation, and authorization are separate. Feature contributions are not causal proof.

## Consequences
Explanations are testable against evidence. Opaque features must be disclosed. A deterministic template is an acceptable LLM fallback.

## Revisit
After dataset/model and explanation method are selected and evaluated.
