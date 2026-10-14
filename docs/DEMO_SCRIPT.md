# Demo Script — Veto

**Target duration:** 3–4 minutes once implemented. Never narrate a feature that does not exist in the submitted commit.

## Setup
Use approved synthetic fixtures. Verify client/simulator and dashboard are connected. Ensure simulation disclosure is visible. Backup screenshots/recordings must accurately match the submitted build.

## Flow
1. **Question:** ask Veto to inspect recent activity and select a suspicious synthetic transaction.
2. **Evidence:** show score, risk band, model version, and structured factors. Explain that the score is a risk estimate, not proof of fraud; disclose opaque features.
3. **Explanation:** ask “Why did you flag this transaction?” Response must map to returned evidence. If scoring/LLM fails, state the limitation rather than inventing a result.
4. **Human control:** request a demo-card freeze or demo-transaction dispute. Veto repeats exact action/scope and says it changes only simulated state. Cancel and prove no change; repeat and explicitly confirm.
5. **Proof:** show dashboard/history reflecting the confirmed simulated action, timestamp, and request/audit reference. If persistence is absent, do not claim this step works.
6. **Close:** “Veto connects risk scoring to evidence, explanation, and a user-controlled response. This prototype does not contact a bank, freeze a real card, or file a real dispute.”

## Judge proof points
Grounded explanation, server-side action boundary, explicit simulation, reproducible scenario, documented evaluation/limitations, and clear trade-offs.

## Fallback
If Alexa+ integration is unavailable or ineligible, use a client-independent simulator with the same MCP contracts and state the limitation plainly.
