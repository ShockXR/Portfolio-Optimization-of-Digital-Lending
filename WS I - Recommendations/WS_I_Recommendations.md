# Recommendations — Digital Lending Portfolio Optimization

**Prepared by:** Anwesha , Shreyan and Arjun
**Date:** 12 June 2026
**Status:** Draft v1
**Inputs:** WS D (channel economics), WS E (segmentation), WS G (policy scenarios). WS F (EWS thresholds) pending — qualitative placeholder included.

---

## 1. Executive Summary

We recommend a four-lever portfolio reshape that delivers **+₹17.85 cr improvement in book contribution at baseline**, rising to **+₹18.80 cr under +3pp macro stress**. Three defensive levers shrink loss-making slices of the book; one offensive lever replaces most of the lost volume with higher-quality origination.

Net effect:

- Book size reshaped by approximately 4% (−₹59.18 cr origination)
- Portfolio contribution improved by ~₹15.5 cr
- Recommendation *strengthens* under stress — the defensive levers dominate, so worse macro conditions amplify (not erode) the gain
- All four levers are operationally implementable using data already in the application pipeline

---

## 2. Strategic Context

Analysis of 49,600 loans (₹1,398 cr origination across six segments) reveals concentrated value destruction in three segments:

- **BNPL** (17,236 loans, ₹25.9 cr origination): 77.7% of loans loss-making. The damage concentrates in Digital ads and DSA channels (mean per-loan loss of −₹1,326 and −₹1,096; default rates 11.06% and 10.80%).
- **Personal Subprime D-E** (5,844 loans, ₹72.5 cr): segment profitable overall (+₹2.99 cr), but 12.6% of loans are loss-makers. A clean behavioural cutoff (`cashflow_consistency_mean < 0.6`) separates losers from winners.
- **SME Non-prime C-D-E** (5,461 loans, ₹536.4 cr): segment highly profitable overall (+₹22.37 cr), but 7% of loans loss-making with disproportionate rupee impact due to large ticket sizes (~₹9 lakh average). The same `cashflow_consistency` signal applies.

Meanwhile, **SME Prime A-B** (4,558 loans, +₹14.68 cr total contribution) is the cleanest segment in the book — only 2.6% loss-making, 2.74% default rate — and undersized relative to its unit economics.

The strategic posture this analysis supports: **shrink the worst, surgically clean the borderline, grow the best.**

---

## 3. Headline Recommendation — Contain SME Non-prime C-D-E

**Lever:** Decline new SME applications where `origination_risk_grade ∈ {C, D, E}` AND `cashflow_consistency_mean < 0.65`.

**Quantified impact:**

| Macro condition | Net Δ in book contribution |
|---|---|
| Baseline (0pp) | **+₹12.97 cr** |
| +2pp stress | +₹13.86 cr |
| +3pp stress | +₹14.30 cr |

**Operational scope:** ~950 applications declined annually, ₹88.67 cr origination foregone (17% of current SME C-D-E flow).

**Implementation owner:** SME Underwriting.

**Guardrail metric:** Monitor SME C-D-E decline rate weekly. Expected stable rate ~17-18% of incoming flow. Deviation >2pp from this band triggers re-calibration.

**Why it's the headline:**

1. Largest absolute impact (~7x Lever 1, ~5x Lever 2)
2. Monotonically increases under stress — the lever does its best work exactly when the macro environment turns
3. Surgical, not segment-wide — only 9% of SME C-D-E declined; the remaining 91% (~4,963 loans, profitable) continue unchanged
4. Uses signals already observable at the application window (grade from underwriting model, cashflow consistency from bank statements via account aggregator)

---

## 4. Supporting Lever 1 — Tighten Personal Subprime D-E

**Lever:** Decline new Personal applications where `origination_risk_grade ∈ {D, E}` AND `cashflow_consistency_mean < 0.6`.

**Impact:**
- Baseline: +₹2.33 cr
- +2pp stress: +₹2.44 cr
- +3pp stress: +₹2.50 cr

**Scope:** 767 loans declined annually, ₹9.39 cr origination foregone (~13% of Personal D-E flow).

**Owner:** Personal Underwriting.

**Guardrail:** Personal D-E decline rate stable at ~13% of incoming flow.

**Rationale:** Same behavioural signal as the headline; demonstrates the rule generalizes across product lines, not just SME.

---

## 5. Supporting Lever 2 — Cease BNPL via Digital Ads and DSA

**Lever:** Discontinue BNPL acquisition through Digital ads and DSA channels. Existing book runs off naturally; no early write-off.

**Impact:**
- Baseline: +₹1.08 cr
- +2pp stress: +₹1.24 cr
- +3pp stress: +₹1.31 cr

**Scope:** 8,610 loans/year no longer acquired, ₹12.95 cr origination foregone.

**Owner:** BNPL Marketing + DSA Channel Management.

**Guardrail:** Monitor remaining BNPL channels (Partner-embedded, Referral, Organic) for volume drift and unit-economic deterioration. If mean per-loan value_proxy in any of these turns more negative than −₹600, escalate.

**Rationale:** Digital ads (−₹1,326/loan) and DSA (−₹1,096/loan) are structurally loss-making. CAC paid through these channels exceeds the loans' lifetime contribution. Pause acquisition is cleaner than re-pricing because the unit economics are too far underwater to fix with APR alone.

---

## 6. Offensive Lever — Grow SME Prime A-B by 10%

**Lever:** Increase SME A-B acquisition by ~456 loans annually (10% of current 4,558).

**Impact:**

| Macro condition | Net Δ |
|---|---|
| Baseline (0pp) | +₹1.47 cr |
| +2pp stress | +₹0.95 cr |
| +3pp stress | +₹0.69 cr |

**Scope:** 456 new loans, ₹51.83 cr origination added.

**Owner:** SME Sales + Business Development.

**Guardrail:** SME A-B default rate must stay below 3.0% as volume grows. Re-evaluate growth target quarterly.

**Note on asymmetry:** Unlike the three defensive levers, this lever weakens under stress because new loans take stressed losses. We include it because:

1. It replaces ~80% of volume given up by the defensive levers (₹52 cr added vs ₹68 cr removed), making the recommendation a *reshape* rather than a *shrink*.
2. SME A-B is the only segment where growth is safe under stress — its 2.74% default rate and ₹32,204 per-loan margin provide enough cushion that the lever stays positive even at +3pp.
3. Without this lever, every other segment's growth would actively destroy value under stress. Demonstrating that we modelled this is itself a signal to the CRO of analytical rigour.

---

## 7. Supporting Lever (Qualitative) — Early Warning System

**Status:** Pending Workstream F threshold calibration.

**Description:** Implement a behavioural Early Warning System (EWS) to flag loans drifting toward default *before* they hit 90+ DPD. Primary signals: `cashflow_consistency_mean`, `balance_volatility_mean`, `nach_bounce_total`, `spending_shock_rate`. Bands: Green (no action), Amber (soft SMS/email outreach), Amber-High (agent call within 7 days), Red (immediate restructure offer). Specific thresholds, expected precision/recall, and average lead time to be calibrated in Workstream F.

**Why include qualitatively:** The four levers above act *at underwriting* — they prevent bad loans from being made. The EWS acts *during the loan lifecycle* — it catches loans that pass underwriting but deteriorate later. The two failure modes are different; both need addressing.

**Expected role in final recommendation:** Quantification will land in WS F. Provisional belief is that EWS captures an additional ₹3-5 cr of avoided losses annually (~30-50% reduction in loss severity for flagged loans), but this is to be confirmed.

---

## 8. Combined Portfolio Impact

| Macro condition | Net Δ in book contribution |
|---|---|
| Baseline (0pp) | **+₹17.85 cr** |
| +2pp stress | **+₹18.49 cr** |
| +3pp stress | **+₹18.80 cr** |

**Volume change:** -₹58.18 cr (~4.2% of book)

**Key insight — monotonic stress improvement:** Portfolio gain *increases* with stress severity. This is rare and powerful — most policy recommendations weaken under stress; this one strengthens because the three defensive levers (avoiding losses) overpower the one offensive lever (taking risks). The book is reshaped to be more resilient, not just more profitable.

**Per-lever breakdown:**

| Lever | Baseline | +2pp | +3pp | Volume Δ |
|---|---|---|---|---|
| L1: Cease BNPL Digital+DSA | +₹1.08 | +₹1.24 | +₹1.31 | -₹12.95 cr |
| L2: Tighten Personal D-E | +₹2.33 | +₹2.44 | +₹2.50 | -₹9.39 cr |
| L4: Grow SME A-B (10%) | +₹1.47 | +₹0.95 | +₹0.69 | +₹51.83 cr |
| L5: Contain SME C-D-E | +₹12.97 | +₹13.86 | +₹14.30 | -₹88.67 cr |
| **Combined** | **+₹17.85** | **+₹18.49** | **+₹18.80** | **-₹58.18 cr**|

---

## 9. Implementation Roadmap

| Phase | Lever | Owner | Effort | Notes |
|---|---|---|---|---|
| Month 1 | Cease BNPL Digital/DSA | BNPL Marketing | Low | Turn off ad spend, freeze DSA acquisition pipeline. Existing book runs off naturally. |
| Month 1-2 | Tighten Personal D-E | Personal Underwriting | Medium | Code the decline rule in the underwriting system; update applicant-facing decline reasons. |
| Month 2-3 | Contain SME C-D-E | SME Underwriting | Medium | Code the decline rule; brief sales/BDs on the new policy and expected decline volumes. |
| Month 3-6 | Grow SME A-B | SME Sales + BD | High | Sales ramp, partner activation, marketing investment. Takes a full quarter to reach 10% growth. |

The tightening/ceasing levers (L1, L2, L5) take effect immediately on new applications. The growth lever (L4) takes a quarter to fully ramp due to sales cycle length in SME.

---

## 10. Risks and Mitigations

**1. Volume optics.** Total origination shrinks ~₹16 cr (1% of book). Mitigation: internally reframe as "reshape," not "shrink." Highlight per-loan economic improvement and the fact that L4's growth offsets ~80% of the shrink.

**2. Channel competitor risk.** Declining more applications may shift volume to competitors. Mitigation: monitor portfolio-level approval rate; if drop is sharper than expected, calibrate cutoff downward (e.g., 0.55 instead of 0.6) to recover some volume.

**3. Stress assumption.** +2pp / +3pp stress (A003) is the engagement-mandated band. If actual stress is *worse*, the defensive levers gain MORE; if *milder*, the recommendation still wins by ~₹15 cr. Tested in detail in WS H.

**4. Operational implementation.** Underwriting rule changes require ~2 weeks of engineering. No new data sources needed — `cashflow_consistency_mean` is already derived from bank statements pulled at application.

**5. Behavioural response from sales.** SME BDs may push back on declining 9% of SME C-D-E flow. Mitigation: pair the lever with the Grow SME A-B target — sales has a positive growth lever to compensate for the declines.

**6. Cutoff calibration drift.** The 0.6 threshold was derived empirically from current data. As applicant mix changes, the threshold may need updating. Recommend quarterly review of the cutoff against fresh segment loss-making rates.

---

## 11. Sensitivity Commentary

Headline recommendation tested against:

- Extended macro stress (0pp to +5pp): combined net Δ rises monotonically; robust beyond engagement-mandated +3pp band.
- **LGD ±10pp (50% to 70% for unsecured retail; 40% to 60% for SME):** Combined net Δ ranges +₹14 cr to +₹17 cr. Recommendation robust.
- **CoF ±1pp (8% to 10%):** Combined net Δ moves less than ₹0.5 cr. Insensitive.
- **Macro stress 0pp to +3pp:** Combined net Δ monotonically improves from +₹15.48 to +₹15.79 cr. Robust under stress.
- **Cashflow cutoff 0.5 to 0.7:** At 0.5 the lever shrinks (~₹8 cr combined defensive impact); at 0.7 it grows (~₹13 cr) but declines too many marginal loans. 0.6 is the empirical optimum where sign-flip is cleanest.
- **L4 growth rate 5% to 20%:** Net Δ scales linearly at baseline but disproportionately under stress (more new loans = more stressed losses). 10% is conservative; 20% would deliver +₹2.9 cr at baseline but only +₹0.4 cr at +3pp.

Full sensitivity matrix in WS H.

---

## 12. Appendix: Assumptions Used

| ID | Assumption | Value | Source |
|---|---|---|---|
| A001 | Cost of Funds | 9.0% | NBFC sector benchmark (Bajaj Finance investor presentations, CARE NBFC sector reports) |
| A002 | LGD — unsecured retail (Personal, BNPL) | 60% | RBI Financial Stability Report; industry standard for unsecured retail |
| A002b | LGD — SME | 50% | RBI FSR; partial collateral/personal guarantee improves recovery |
| A003 | Macro stress band | +2pp / +3pp default rate | Engagement brief mandate |
| A004 | Operating cost | 1.5% of ticket | NBFC opex/AUM benchmark, typical 2-4% annual → ~1.5% per loan at typical tenures |
| A005 | CAC by channel | Per Workstream D output | Internal channel economics analysis |

---

## 13. Open Items / Pending Inputs

- **WS F EWS thresholds** — Section 7 to be quantified once Workstream F completes calibration. Expected ~mid-Week 2.
- **WS H sensitivity tables** — full sensitivity matrix referenced in Section 11. Currently summarized; full tables in WS H output.
- **Implementation owner sign-offs** — each lever's named owner needs to acknowledge the implementation effort and timeline before final lock.

---


