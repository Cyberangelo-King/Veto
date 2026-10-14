# P2 Note — Broader legal/privacy applicability and currency presentation

- **Priority:** P2 for the current hackathon prototype.
- **Status:** Deferred and consolidated from research items R-06 (broader legal/privacy questions) and R-08 (FX conversion).
- **Date consolidated:** 2026-10-14.

## Why this is P2 for the demo
The selected demo is synthetic-data-only and its card/merchant actions are simulated. The demo does not contact a bank, payment network, card issuer, or real customer account. That keeps broad production legal analysis off the immediate working-demo path; it does not establish compliance or waive future obligations.

## Required boundary
- Do not collect real payment-card credentials or customer transaction history.
- Do not represent Veto as a production financial service or claim regulatory compliance.
- Any future use of real personal data, production users, a live issuer/payment integration, or real action execution is blocked until an appropriate privacy, security, legal, and financial-services review is completed.
- Retain a clear privacy/data-handling disclosure that matches the actual synthetic demo behavior.

## Currency decision
Use the dataset's USD amount and label it USD in the hackathon demo. Do not convert it to NGN unless there is a specific verified user need. If conversion is later introduced, record the authoritative rate source, date/time, method, and display rounding; the conversion is presentation-only and must not change the model input.

## Research register reconciliation
R-06 and R-08 in docs/research/README.md are consolidated here. This P2 note can be revisited if the demo begins collecting real data, if a live financial integration is proposed, or if the product requires currency conversion.
