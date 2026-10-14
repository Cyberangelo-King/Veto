# Friction Log

Record real developer-tool friction encountered while building Veto. Do not manufacture incidents or turn an untested assumption into a report. Each entry should be specific enough for a tool team to reproduce and act on.

## Entry template

### [YYYY-MM-DD] Short, specific title

- **Task attempted:**
- **Tool:** tool/API/SDK name, version, relevant URL or surface
- **Steps taken:** ordered reproduction steps, including relevant setup and inputs (no secrets)
- **Expected result:**
- **Actual result:**
- **Severity:** Critical / High / Medium / Low
- **Workaround used:** exact workaround, or “None”
- **Actionable suggestion:** concrete change that would reduce or eliminate the friction
- **Evidence:** sanitized error text, screenshot, run ID, or minimal reproduction
- **Status:** Open / Workaround / Resolved

## Severity guide

- **Critical:** blocks the core demo or creates a severe security/data-integrity issue with no safe workaround.
- **High:** blocks an important workflow or requires a substantial workaround.
- **Medium:** makes a task materially slower/confusing or causes a recurring failure with a viable workaround.
- **Low:** small inconvenience, documentation gap, or cosmetic inconsistency.

## Rules for useful entries

- Report only observed results. Separate facts from suspected causes.
- Include the tool/version and exact steps needed to reproduce.
- Redact access tokens, account identifiers, private data, and real card/customer details.
- The official hackathon rules describe friction-log submissions as optional and say entries can contribute up to a 10% judging bonus. Keep an honest record; do not invent friction to chase bonus points.

No incidents are recorded in this log yet.
