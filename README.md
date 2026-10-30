# Nudge: AI Follow-Up Executor

---

## One-Sentence Thesis

An AI assistant for commercial real-estate (CRE) brokers shouldn't just flag a stalled deal. It should turn verified deal signals into one broker-approved action that is executed and logged in the shared workflow.

---

## Hypothesis

Brokers don't need another AI tool that generates a to-do list. They need a system that:
1. Detects which deal is genuinely at risk of stalling (not just "any" deal),
2. Shows exactly why, grounded in existing CRM/listing/engagement data,
3. Proposes one specific action instead of ten generic tips,
4. Lets the broker review, edit, and approve before anything is sent,
5. Closes the loop by logging the outcome back into the CRM.

The design principle: data entered once should flow across prospecting, CRM, marketing, transactions and commissions without re-entry, so the assistant executes rather than merely recommends.

---

## Workflow (mapped to the CRE brokerage lifecycle)

| Stage | What the prototype demonstrates |
|---|---|
| Prospecting → CRM | Buyer requirement profile and contact history pulled from a single connected record |
| Marketing | Listing facts and OM engagement (views, last viewed date) feed the risk signal |
| Transaction | Deal stage, days in stage, expected close, and seller marketing window drive urgency |
| Commission-adjacent | Activity logging and next-step scheduling keep the pipeline data accurate for downstream reporting |

The core interaction loop is: **Deal card → Momentum alert → Why this action? → Draft outreach → Recipient controls → Freshness check → Approve → Activity logged.**

---

## Controls (what makes this a controllable system, not a chat assistant)

- **Grounding panel ("AI used / AI did not use")** — every recommendation discloses its exact sources (CRM contact history, buyer requirement profile, listing facts, engagement data) and explicitly excludes unverified property facts, unsourced market claims, and personal data outside CRM permissions.
- **Interpretable scoring, not a black-box number** — the UI shows "Momentum at risk: High/Medium/Low," never a raw score like "83/100." The underlying contributors (buyer silence, seller marketing window, buyer-asset match, engagement signals) are visible only inside a "Why this action?" drawer, framed explicitly as an initial, calibratable model — not ground truth.
- **Freshness revalidation before send** — a visible "Data checked N min ago · Listing active · Recipient permissions verified" strip sits directly above the approval button, with a manual re-check control, because buyer activity and listing state can change between recommendation and execution.
- **Hard permission enforcement** — contacts outside CRM marketing permission (e.g., an assistant with no deal authority) are rendered as disabled, unchecked, and labeled "Excluded—no marketing permission." They cannot be included in a send unless a fictional, explicit permission-grant action occurs first. This is enforced in the send logic, not just a UI warning.
- **Approval as a hard boundary** — nothing is sent, logged, or scheduled until the broker explicitly clicks "Approve & send." The button disables after send to prevent duplicate actions.
- **Feedback loop ("Not relevant")** — brokers can dismiss a recommendation with a specific reason (buyer no longer active, deal status outdated, wrong recommendation), which suppresses that recommendation and logs the feedback — the mechanism that would retrain prioritization thresholds over time.

---

## Initial Metrics (synthetic, illustrative)

- 4 mock deals modeled across Industrial, Office, and Retail asset types.
- 3 of 4 deals triggered a Medium or High momentum alert under the interpretable scoring rules.
- 1 recommendation was marked "not relevant" during testing, demonstrating the feedback path back into the system.
- 1 of 5 total mock contacts was correctly blocked from outreach due to missing marketing permission, without requiring the broker to manually catch it.

These are demonstration figures only, meant to show the shape of instrumentation this product would need in production (alert precision, dismissal-reason distribution, permission-block rate) — not real performance claims.

---

## Next Steps If This Were Real

1. Validate whether each scoring signal (silence days, OM views, requirement match, window proximity) actually predicts a meaningful deal-stage transition, using historical CRM data.
2. Calibrate thresholds by asset type, brokerage segment, and deal stage rather than using one fixed rule set.
3. Replace the fictional permission-grant flow with a real CRM permission and consent model.
4. Expand the feedback loop (Not Relevant reasons) into a lightweight model-retraining signal.

---

## 60-Second Walkthrough Script

"This is Nudge — an AI Follow-Up Executor for CRE brokers. Instead of a to-do list, it surfaces one deal at risk of stalling and tells you why: buyer silence, seller window closing, requirement match, engagement signals — all sourced from CRM and listing data, shown as 'Momentum at risk: High' rather than a fake precision score. Clicking 'Why this action?' shows the actual contributing signals — this model is intentionally interpretable, not a black-box propensity score; the next step would be validating each signal against real deal-stage transitions. The broker edits the drafted outreach, but notice this contact is technically blocked — no marketing permission, not just a warning. Before sending, the system re-checks data freshness, because buyer activity and listing state can change between recommendation and execution. Approve, and it logs the activity and schedules the next follow-up — closing the loop back into the CRM."

---

## Disclaimer

All deals, contacts, companies, and CRM entries are synthetic and fictional, created for demonstration only. This is an independent prototype exploring AI follow-up workflows in CRE brokerage.

_Personal project; not affiliated with or endorsed by any company._ License: MIT
