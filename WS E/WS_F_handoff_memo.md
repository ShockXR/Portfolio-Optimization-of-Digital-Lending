# Workstream E → F Handoff Memo
### Building the Early Warning System (EWS)

**From:** Workstream E (Segmentation) · **To:** Workstream F (Early Warning System)
**Depends on:** C (data), D (EDA), **E (this handoff)** · **Feeds:** G (optimization), I (recommendation), dashboard

---

## 1. What F inherits from E

1. **The frozen 6-segment scheme + assignment table** (`E_final_segment_assignments.csv`, `loan_id`/`customer_id` → segment). F builds early-warning *within and across* these segments, and reports flag rates per segment.
2. **The seed signal — the "C4" behavioural-distress finding (most important).** E's clustering surfaced a group, defined purely by *behaviour*, that defaults at ~66%: **8× the payment-bounce rate (≈8 vs 0.5), 7× the spending-shock rate (22% vs 3%), credit utilisation 63% vs 35%, low cashflow consistency.** E correctly **refused to use this as a segment** because those signals appear only as a borrower is *already failing* — useless at origination. **That group is exactly what F exists to catch.** It is the prototype of the EWS signal; operationalise it into a live score.
3. **The behavioural panel** (`behaviour_monthly`): `cashflow_consistency`, `balance_volatility`, `credit_utilisation`, `nach_bounce_count`, `spending_shock_flag`, `bureau_inquiry_velocity`, `app_engagement` — F's primary raw material, plus `repayments` for the DPD/default timeline.

---

## 2. Three lessons from E that F must carry (read before modelling)

- **Point-in-time / leakage discipline — the #1 risk for F.** E kept behaviour *out* of segmentation precisely because it's post-origination. F's whole job *is* behaviour — but the trap that made C4 unusable (defining a flag using signals that *coincide* with default) is the same trap F must avoid in its own training. **To predict default at month _t_, use only signals observable strictly before _t_.** Features must *lead* the outcome, not move with it. Validate with an **out-of-time test** (train on older loans/months, test on newer), which the backtest reviewer showed is the real proof.
- **Seasoning / censoring.** `default_flag` = "ever 90+ DPD (sticky)", mechanically impossible before ~3 months on book. F's labels need a defined performance window, and short-tenure BNPL needs care (a 2-month loan can't reach 90+). Do **not** use a naïve fixed-early-window default rate — fast write-offs vanish early and make risky pools look safe (survivorship illusion).
- **Risk ≠ value.** Segment value is driven by product/ticket size, not creditworthiness. F is about *risk timing*, not value — keep them separate.

---

## 3. F's mandate

Build a **dynamic, point-in-time early-warning score** that flags *performing* loans heading toward default, refreshed monthly, with usable **lead time** before 90+ DPD. Concretely:

- Start feature set from the C4 drivers (bounces, shocks, utilisation, volatility, cashflow consistency) plus the rest of the panel, all lagged to be point-in-time.
- Output a per-loan/per-customer **watchlist flag + score**, with a tunable threshold (precision/recall trade-off the business can set).
- Connect back to E: report early-warning rates **by segment**, with priority on the **Contain** segment (#3, Personal Non-prime) and **Subprime BNPL (#6)**, and surface the behavioural-distress cohort as the top watchlist.

---

## 4. Acceptance gate (Gate 4 — EWS review)

- **Lead time:** flags fire *before* default, not coincident with it (measured lag).
- **No leakage:** point-in-time validated; passes an out-of-time test.
- **Actionable:** precision/recall trade-off is usable at a business-chosen threshold; flag volume is operationally manageable.
- **Stable:** performance holds across cohorts and resamples.

---

## 5. Inputs checklist for F

- `behaviour_monthly` (the 7 signals, monthly panel) · `repayments` (DPD/default timeline) · `loans` (origination + outcome) · `customers` (profile)
- `E_final_segment_assignments.csv` (segment per loan) · the frozen frames (`loan_frame`, `customer_frame`)
- Seasoned-basis convention (MOB ≥ 3) and the point-in-time rule above
- `_true_latent_risk_VALIDATION_ONLY.parquet` — for sanity-checking only; **never a feature** (creditworthiness-oriented, higher = safer)

---

## 6. One-line summary

**E sorted the book by who borrowers *are* (product × grade). F's job is to watch how they *behave* over time and ring the alarm before a loan goes bad — using the behavioural-distress pattern E found but couldn't act on, turned into a leakage-clean, point-in-time early-warning score.**
