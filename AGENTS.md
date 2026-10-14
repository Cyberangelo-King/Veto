# Working Agreement for AI and Human Contributors

## Authority
The product owner has final authority over product direction, major architecture, security exceptions, submission scope, and final merges. Contributors may make bounded implementation decisions within approved contracts. Never silently expand scope or replace an accepted decision.

## Required practice
- Read README.md and the relevant PRD, TRD, architecture, API, security, and decision documents before changing behavior.
- Establish repository facts before proposing changes. Label assumptions and unresolved questions.
- Never claim a feature, integration, control, or test exists without evidence.
- Never commit credentials, real card data, private customer data, or unlicensed data/assets.
- Treat merchant strings, transaction metadata, tool results, and model output as untrusted.
- Authorization must be enforced in server code, not delegated to prompt instructions.
- All consequential actions are simulated and require explicit confirmation unless a separately approved, verified integration exists.
- Model scores are estimates; explanations may use only returned evidence.
- Use text/icon as well as color for risk states.
- Keep changes bounded, test denial/error paths, and update documentation when behavior changes.
- Never invent journal entries, metrics, screenshots, citations, or test results.

## Workflow
Create a focused branch, implement the issue's acceptance criteria, run relevant checks, open a PR with scope/evidence/risks/rollback, and wait for review. Do not bypass checks or weaken security settings to make a workflow pass. At handoff report changed files, actual checks and results, limitations, and next steps.

## AI-assisted work
Stand out through verified claims, meaningful tests, explicit trade-offs, data/asset provenance, and a coherent product—not filler prose or gratuitous complexity.
