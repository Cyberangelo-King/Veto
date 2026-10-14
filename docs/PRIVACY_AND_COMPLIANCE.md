# Privacy, Data Licensing, and Compliance

**This document is a verification checklist, not legal advice or a claim of compliance.** See docs/research/P2-legal-and-currency-note.md for consolidated P2 work deferred from the immediate demo path.

## Safe prototype boundary
Use only the selected synthetic Sparkov dataset, subject to the verified source terms. Do not collect real PANs, CVVs, PINs, bank credentials, or customer transaction histories. Keep raw dataset files outside Git. Minimize logs/prompts and personal identifiers. Document reset/deletion behavior if state persists. Clearly label the product and all card/merchant actions as simulated.

## Dataset and model due diligence
Before importing data or reusing model artifacts, record exact dataset/version/source/access date, source-published license/terms, permitted hackathon/training use, attribution requirements, redistribution/derivative-model restrictions, feature dictionary, target definition, and risks. A public download is not proof of unrestricted use. Keep raw data out of Git unless terms explicitly permit it.

For the Ensemble repository, record source commit, training/preprocessing pipeline, model artifacts, feature order, dependencies and their licenses, threshold provenance, and evaluation method. Do not copy artifacts until their provenance and use rights are understood.

## Product claims
Do not claim Veto prevents fraud, guarantees detection, or provides live bank protection. Do not say fraud is confirmed from a model score. Do not claim a real card was frozen or a real dispute filed without a verified authorized system. Synthetic-data performance does not establish real-world performance. Explain score scale, false positives/negatives, and limitations.

## Immediate release checks
- Verify dataset and model-artifact rights required for the demo.
- Review dependencies/assets used by the implemented experience.
- Keep all card/merchant actions simulated and disclose this in voice/UI/README/video.
- Ensure privacy/data-handling copy matches actual data flows.
- Do not place raw dataset records or personal data in logs, commits, screenshots, or AI prompts.
- Verify current hackathon requirements and AWS/Alexa+ terms that directly affect the chosen implementation.

## Deferred P2 legal/currency work
The broader question of applicable Nigerian data-protection/financial-services obligations and any optional USD-to-NGN conversion is consolidated in docs/research/P2-legal-and-currency-note.md. It is deferred for this synthetic-data-only, simulated-action demo and is not a claim that the project is compliant. Full review becomes a blocker before processing real customer data, launching for real users, or integrating with an issuer/payment network. Avoid currency conversion in the demo; display USD explicitly unless a verified product need requires conversion.

## Third-party AI
Send only the minimum synthetic data required to providers. Verify provider terms, retention/training behavior, region, permissions, and account settings before sending transaction-like data. Treat output as untrusted and validate before display/action.

## Retention
Define what persists, for how long, who can access it, and how reset/deletion works. Do not promise deletion guarantees until storage, logs, backups, and provider behavior are understood.

## Checklist
- [ ] Dataset source/version and terms recorded.
- [ ] Model artifacts and dependencies have provenance/license notes.
- [ ] No real card/customer data present.
- [ ] Privacy disclosure matches actual data flows.
- [ ] Simulation disclosure appears in README, UI, and demo.
- [ ] No unsupported performance, security, compliance, or fraud-prevention claims.
- [ ] P2 note explicitly limits the current prototype to synthetic data and simulated actions.
