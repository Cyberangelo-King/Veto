# ADR 002 — Client-independent MCP with simulator fallback

- Status: Proposed pending platform verification
- Date: 2026-10-14
- Owner: Product owner

## Context
Alexa+ access, MCP transport, account eligibility, and review requirements must be verified. The core demo cannot depend on an unproven integration.

## Options
1. Assume direct Alexa+ integration.
2. Keep MCP contracts client-independent and build a simulator that exercises the same tools; add Alexa+ if official docs/account access support it.
3. Build only a browser mock without real tool contracts.

## Decision
Prefer option 2. The simulator is a tested fallback, not something to misrepresent as Alexa+. Submission copy must describe the delivered integration exactly.

## Revisit
After official docs and account-level proof establish integration path, eligibility, and time/cost trade-offs.
