# Privacy, Data Licensing, and Compliance

**This is a verification checklist, not legal advice or a claim of compliance.**

## Safe prototype boundary
Use synthetic or explicitly approved data only. Do not collect real PANs, CVVs, PINs, bank credentials, or customer histories. Minimize logs/prompts and personal identifiers. Document reset/deletion behavior if state persists. Clearly label prototype and simulated actions.

## Dataset due diligence
Before use, record exact dataset/version/source/access date, owner, license/terms, permitted research/commercial/hackathon use, redistribution and derivative-model restrictions, attribution, privacy/re-identification risk, feature dictionary, target definition, and whether raw files can be placed in public GitHub. A public download is not proof of an open license. Keep raw data out of Git unless terms explicitly permit it.

## Claims
Do not claim Veto prevents fraud, guarantees detection, or provides live bank protection. Do not say fraud is confirmed from a model score. Do not claim a real card was frozen or a real dispute filed without a verified authorized system. Synthetic benchmark performance does not establish real-world performance. Explain false positives/negatives and score meaning.

## Research required
Verify current official sources for:
- Amazon Developer Hackathon 2026 rules, track criteria, deadline, judging rubric, open-source mini-challenge and branding restrictions.
- Alexa+ and MCP support/account eligibility.
- AWS service terms, regions, pricing, quotas, data retention, and deployment constraints.
- Dataset terms and licenses.
- Applicable Nigerian data protection requirements and regulator guidance; seek qualified legal advice if needed.
- Financial/card-network obligations if a real integration is ever considered.
- Licenses for packages, models, fonts, icons, images, and all assets.

Record official source URLs, access date, relevant clauses summarized in your own words, decision impact, and approver in docs/research/README.md. Do not treat this checklist as completed research.

## Third-party AI
Send only minimum synthetic data to providers. Verify terms, retention/training behavior, region, and settings before sending transaction-like data. Treat outputs as untrusted and validate before display/action.

## Retention
Define what persists, for how long, who can access it, and how reset/deletion works. Do not promise deletion guarantees until storage, logs, backups, and provider behavior are understood.

## Release checklist
- [ ] Dataset and asset licenses reviewed.
- [ ] No real card/customer data.
- [ ] Privacy disclosures match actual data flows.
- [ ] Simulation disclosure appears in README, UI, and demo.
- [ ] Current hackathon/AWS/Alexa+ terms verified from official sources.
- [ ] Applicable data-protection questions verified.
- [ ] No unsupported security, compliance, performance, or fraud-prevention claims.
