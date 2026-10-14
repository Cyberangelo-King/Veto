# Build Journal

Evidence log, not marketing copy. Add entries only after work is complete. Link commits, PRs, tests, screenshots, research, or other artifacts. Never invent friction, metrics, or test results.

## Entry template
### YYYY-MM-DD — Objective
- Goal:
- Completed:
- Evidence:
- Decisions:
- Verification actually run:
- Blockers/uncertainty:
- Next action:
- Status: complete / partial / blocked

## 2026-10-14 — Repository foundation
- Goal: Establish product and workflow foundations.
- Completed: README, contribution/security guidance, environment template, ignore rules, product/technical specifications, architecture/API/data contracts, design/accessibility specification, threat/security/privacy documents, test strategy, deployment/demo runbooks, research register, decision records, AI workflow, issue/PR templates, and repository-hygiene workflow added on docs/project-foundation.
- Evidence: https://github.com/Cyberangelo-King/Veto/pull/1 ; branch docs/project-foundation.
- Decisions: Documentation-first; client-independent MCP with simulator fallback; simulated-only consequential actions; separate scoring from explanation. Hosting, dataset, and client integration later locked by ADRs 005–007 on the follow-on branch.
- Verification actually run: Repository metadata and public visibility checked; FraudGuard-Simulation and FraudGuard-Demo inspected read-only; no files in those repositories changed. GitHub Actions CI run #1 passed for PR #1.
- Blockers: PR #1 remains open/draft as of this journal update. The follow-on documentation branch must not be opened as PR #2 until PR #1 is merged. Application code is not implemented or validated.
- Next action: Review/merge PR #1; then open PR #2 from docs/lock-decisions-rules, review CI and documentation consistency, then proceed with demo-path implementation issues.
- Status: partial — foundation is in PR #1; decision-lock/submission updates are staged separately and no app code has been added.

## 2026-10-14 — Decision lock and submission alignment (follow-on branch)
- Goal: Align the selected architecture and docs with official event requirements before implementation.
- Completed: Read official Devpost rules and FAQ; verified MCP/server-versus-web-simulator requirements, video length, tool-by-tool product feedback, Open Source and AWS Builder mini-challenges, and friction-log optional bonus; prepared ADRs 005–007, updated README/TRD/architecture, reduced demo script to 2:50, standardized friction-log fields, and added submission checklist/P2 note.
- Evidence: official rules https://amazonappdev2026.devpost.com/rules ; FAQ https://amazonappdev2026.devpost.com/details/faqs ; follow-on branch docs/lock-decisions-rules.
- Decisions: Sparkov/fraudTrain/fraudTest + engineered features and Ensemble stacking/SHAP; real Streamable HTTP MCP server + genuine web MCP client; Lambda/FastAPI+Mangum/DynamoDB/Bedrock/Polly with local no-cloud mode.
- Verification actually run: Official rules/FAQ search-result/page content checked; current PR #1 metadata confirms state=open and draft=true; no PR #2 opened. CI has not yet run on the follow-on branch because it is not a pull request.
- Blockers/uncertainty: Verify exact dataset terms/version when accessed; audit Ensemble artifacts and feature generation; verify selected SDK/Protocol compatibility and AWS Lambda HTTP adapter/cost at implementation time; repo administration writes are unavailable through the current connector.
- Next action: Re-triage issues so P0 contains only the working demo path, document legal/currency as P2, then wait for PR #1 to merge before opening PR #2.
- Status: partial — documentation changes are on the follow-on branch, not yet merged; no application code was added.
