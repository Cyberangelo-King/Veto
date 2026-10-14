# Design Specification — Veto

## Intent
A considered financial decision tool: calm, precise, legible, distinctive. Avoid generic AI-dashboard tropes, gradient-heavy hero sections, decorative chat bubbles, robot mascots, excessive rounded cards, and filler copy. Evidence—not the assistant—is the visual hero.

## Visual direction
Charcoal/slate foundation, warm amber for attention, green for lower-risk/verified states, red for high-risk/blocked states. Red, amber, and green must always have explicit text and/or icon indicators. Use custom hierarchy and deliberate spacing rather than a grid of generic cards.

## Semantic states
| State | Visual treatment | Required text/icon |
|---|---|---|
| Low risk | Calm green accent | LOW RISK + check/neutral icon |
| Needs review | Amber accent | REVIEW + alert icon |
| High risk | Red accent | HIGH RISK + warning icon |
| Action pending | Neutral/amber | AWAITING CONFIRMATION + clock |
| Simulated success | Green/neutral | SIMULATED ACTION COMPLETE + check |
| Denied/failed | Red/neutral | Explicit error and next step |
| Unknown evidence | Neutral | UNKNOWN / NOT AVAILABLE; never zero |

## Screens
**Activity:** recent synthetic transactions, timestamp, merchant, amount/currency, risk text label, synthetic-data disclosure, empty/loading/stale/error states.

**Transaction detail:** transaction facts, risk band/score scale/calibration, structured evidence, explanation and limitations, model/version, clearly simulated actions.

**Confirmation:** exact action/resource/scope, consequence, explicit Confirm and Cancel, no default focus on Confirm, ambiguous response means no mutation.

**History:** chronological action, outcome, timestamp, simulation label, request/audit reference; no unnecessary raw prompt.

**Scenario simulator:** named synthetic scenarios, controls separate from product actions, no path to bypass authorization.

## Voice style
Result first, one or two evidence points, uncertainty, safe next step. Do not read raw feature vectors by default. Say “I marked the demo card as frozen,” not “Your card has been frozen.” Confirmation example: “I can mark this demo card as frozen. This changes only Veto's simulated state. Should I proceed?”

## Accessibility
Meet WCAG AA contrast targets where applicable; accessible names and visible keyboard focus; keyboard-only inspection/confirmation/cancel; risk never color-only; announce status changes to assistive technology; responsive narrow layouts; reduced-motion support; errors not communicated only by color. Verify font and asset licenses before bundling.
