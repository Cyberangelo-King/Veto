# Contributing to Veto

Read README.md, AGENTS.md, and the relevant specification before starting. Check issues, claim/comment on the work, and agree on acceptance criteria before broad changes.

## Branch and pull request
Use focused branches such as feat/mcp-explain-transaction, fix/owner-scope-check, or docs/demo-runbook. Open a PR against main. Include problem, scope, acceptance criteria, checks actually run, screenshot/demo evidence where relevant, security/privacy/licensing implications, known limitations, and rollback.

## Quality bar
- Strict input schemas and bounded values.
- Server-side authentication, ownership, and action authorization.
- Explicit confirmation, short-lived action intent, and idempotency for consequential writes.
- Safe errors and no secrets/sensitive payloads in logs.
- Explanations grounded in model evidence; no fabricated reasons.
- Accessible labels/icons in addition to risk colors.
- Tests for success, denial, failure, and boundary cases.
- Provenance/license review for datasets, models, dependencies, fonts, icons, and other assets.

## Data and secrets
Never commit credentials, API keys, tokens, real card data, or private customer records. Use .env.example for placeholder-only variable names. Keep raw datasets outside Git unless rights explicitly permit redistribution. Do not paste secrets or private data into AI prompts.

Review feedback should be specific, respectful, and evidence-led. Mark blockers separately from suggestions.
