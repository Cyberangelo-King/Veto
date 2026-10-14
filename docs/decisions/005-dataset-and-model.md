# ADR 005 — Sparkov dataset and stacking model

- **Status:** Accepted
- **Date:** 2026-10-14
- **Decision owner:** Product owner

## Context
Veto needs a synthetic transaction dataset with merchant category, amount, transaction time, cardholder location, merchant location, and fraud labels so the feature engineering and explanation experience can be demonstrated without real customer/card data.

## Decision
Use the Kaggle Sparkov-generated credit-card transaction dataset: fraudTrain and fraudTest. The intended source page is https://www.kaggle.com/datasets/kartik2112/fraud-detection. Keep raw CSVs outside Git.

Use the following engineered model features:
- amount_vs_user_median
- distance_from_home_km
- hour
- is_night
- is_new_merchant
- txn_count_last_1h
- mins_since_last_txn
- category

Use the stacking LR + RF + XGB approach from https://github.com/Cyberangelo-King/Ensemble-Machine-Learning-for-Online-Credit-Card-Fraud-Detection. Use SHAP TreeExplainer to derive model-contribution evidence that is supplied to the narrative layer.

## Required data and feature safeguards
- Record exact Kaggle dataset version, access date, displayed license/terms, attribution requirements, and permitted use when the files are acquired. This decision does not authorize redistribution of raw data.
- Keep fraudTest held out for final evaluation; don't use it to tune model, preprocessing, thresholds, or feature design.
- Compute amount_vs_user_median from the cardholder's prior transactions only. Define a safe fallback for insufficient history.
- Compute distance_from_home_km using the source cardholder and merchant coordinates with a documented distance method.
- Derive hour and is_night from transaction timestamp with a documented timezone assumption.
- Compute is_new_merchant from prior history for a pseudonymous demo user.
- Compute txn_count_last_1h and mins_since_last_txn using only events preceding the transaction being scored, in chronological order.
- Encode category using a training-only pipeline; persist preprocessing and feature order with the model.
- Never use is_fraud as an input feature. Never use future events, raw card number, name, date of birth, street address, or other unnecessary identifying fields as model features or narrative context.
- Replace raw card number with an internal pseudonymous identifier for grouping; don't log or display the source number.
- Evaluate class imbalance and threshold trade-offs; report precision, recall, PR-AUC, confusion matrix, false positives/negatives, and calibration status where supportable.
- Record model artifact provenance, training code commit, preprocessing version, model version, feature order, evaluation split, and threshold.
- SHAP contributions describe the model's behavior, not causation. The narrator must not invent real-world semantics for opaque features or claim that a score proves fraud.

## Consequences
The selected feature set supports a more legible explanation than V1–V28-only features, but requires correct temporal aggregation and leakage tests. The model can be reused only after the Ensemble repository's artifacts and training pipeline are audited for compatibility and provenance. Synthetic-data results are not evidence of production fraud performance.

## Revisit
Revisit if dataset terms disallow the intended use, the chosen files cannot support the features, or evaluation shows the selected stacking approach is too unreliable for the bounded demo.
