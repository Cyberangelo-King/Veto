# Data Dictionary — Veto

**Status:** Canonical proposal. Do not assume dataset-specific fields before source/license and feature semantics are verified.

## Transaction
| Field | Type | Meaning |
|---|---|---|
| transaction_id | UUID/string | Stable synthetic identifier, not a payment-network ID |
| owner_id | internal string | Derived from trusted identity, never trusted from client |
| event_time | ISO 8601 UTC | Fixture event time |
| amount | decimal-safe | Exact amount with explicit currency |
| currency | ISO code | Never implicit |
| merchant_id | string | Normalized synthetic merchant ID |
| merchant_display_name | string | Untrusted text; escape on render |
| channel | enum/optional | Use only if source supports it |
| location | optional structured | Synthetic/coarse only; don't infer missing data |
| source | enum | synthetic_fixture or approved_dataset |
| simulation | boolean | True for prototype-generated state |

## Scoring result
score, score_scale (min/max/direction/interpretation), risk_band, model_id, model_version, scored_at, calibration_status, evidence array, limitations array. Each evidence item may contain feature name, human label, observed value, direction/contribution if supported, and provenance. Contribution is not causation. Never invent semantics for opaque features.

## Action intent and audit
intent_id (server-generated, short-lived), actor_id (validated principal), action_type, resource_id, scope, created_at, expires_at, confirmation_status, idempotency_key, outcome, simulation boolean, request_id. Record only necessary metadata.

## Currency
Persist explicit currency. If model values are USD and UI displays NGN, document rate source/date and label conversion presentation-only. Never silently convert model inputs. Use decimal-safe arithmetic and round only at a documented display boundary.

## Feature provenance
For every feature, document source column, meaning, unit/range, availability at decision time, missing-value policy, transformation, leakage risk, display label, and source/license. Opaque fields can support prediction but cannot honestly be narrated as intuitive facts.

## Minimization
Store only synthetic records needed for the demo. Avoid full prompts, raw logs, unnecessary identifiers, and personal data. Define reset/deletion behavior before claiming memory. Raw data/model artifacts remain outside Git by default.
