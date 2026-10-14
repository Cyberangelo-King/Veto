# Security Model — Veto

## Objectives and assets
Protect synthetic transaction data, user-scoped demo state, pending intents, audit history, model artifacts, credentials, CI permissions, and integrity of risk scores/explanations/actions.

## Actors
Anonymous visitor, authenticated demo user, product owner, CI/dependency scripts, model provider, and attacker controlling transaction descriptions, merchant text, tool arguments, or scenario inputs.

## Required controls
- Authentication and resource authorization are separate.
- Derive ownership from validated identity; enforce it at the data/action boundary.
- Strict schemas and bounded inputs.
- Two-step confirmation for consequential actions, with short-lived one-use intent.
- Idempotency and conditional state updates.
- Non-enumerating errors for unknown/non-owned resources.
- Least-privilege cloud roles and Actions permissions.
- No credentials in source, logs, screenshots, or fixtures.
- No raw sensitive payload logging.
- Review dependencies and workflow changes; do not expose cloud credentials to untrusted PRs.
- Public simulator must not expose privileged mutations without authorization.
- Do not weaken security settings to make CI pass.

## LLM/tool safety
Tool schemas and server-side checks define capabilities. The LLM may request a tool but cannot authorize it. Merchant descriptions, metadata, retrieved text, and model output are untrusted. Separate data from instructions. No credentials, arbitrary SQL/shell, unrestricted URLs, or generic write tools. Narrative cannot override evidence, risk thresholds, or authorization. Ambiguous confirmation denies mutation.

## Audit/logging
Record request ID, pseudonymous actor, action, resource alias, timestamp, outcome, and simulation status. Exclude prompts, tokens, secrets, and unnecessary transaction payloads.

## Repository controls
Recommended: branch protection/ruleset for main, PR review, required passing checks when reliable, limited Actions token permissions, secret scanning/push protection where available, dependency updates, and no long-lived cloud credentials in workflows. Verify settings in GitHub after changes; documentation alone is not proof they are active.

## Release blockers
Cross-user access, forged/replayed confirmation, exposed secrets or real card data, false claims of real financial action, fabricated evidence, untrusted input triggering tools, or service failure reported as success.

A design document, CI pass, or dependency scan is not a security certification. Actual code needs review and tests.
