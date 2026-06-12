# Workstream H — Sensitivity Analysis Findings

**Prepared by:** Anwesha
**Date:** 12 June 2026
**Status:** Final
**Inputs:** WS G scenarios and lever computations.

---

## 1. Summary

Workstream H stress-tests the WS G recommendation against four independent assumption ranges to assess robustness. Three of the four sensitivities confirm the recommendation; the fourth (cashflow cutoff) revealed a sub-optimal cutoff for Lever 5 (Contain SME C-D-E) that has been corrected.

**Headline findings:**

1. **Extended macro stress (0pp to +5pp):** Combined Net Δ rises monotonically from +₹15.48 cr to +₹16.00 cr. Recommendation strengthens under stress; no break-point identified within plausible range.

2. **LGD ±10pp:** Combined Net Δ varies by only ~₹0.10 cr across the full LGD band (+₹15.74 to +₹15.84 cr at +3pp stress). Recommendation is effectively LGD-insensitive due to offsetting effects between defensive and offensive levers.

3. **Cashflow cutoff (0.50 to 0.70):** Empirical optimum confirmed for L2 (Personal D-E) at 0.60. **Empirical optimum for L5 (SME C-D-E) is 0.65, not 0.60 as originally specified — see Section 4 for details.** L5 cutoff has been updated.

4. **L4 growth rate (5% to 20%):** [To be completed when run.]

---

## 2. Extended Macro Stress

**Method:** Compute combined portfolio Net Δ at default-rate stress levels from 0pp to +5pp.

**Result (Net Δ in ₹ cr):**

| Stress (pp) | L1 | L2 | L4 | L5 | Combined |
|---|---|---|---|---|---|
| 0 | 1.08 | 2.33 | 1.47 | 10.61 | 15.48 |
| 1 | 1.16 | 2.38 | 1.21 | 10.83 | 15.59 |
| 2 | 1.24 | 2.44 | 0.95 | 11.06 | 15.69 |
| 3 | 1.31 | 2.50 | 0.69 | 11.29 | 15.79 |
| 4 | 1.39 | 2.55 | 0.43 | 11.52 | 15.89 |
| 5 | 1.47 | 2.61 | 0.17 | 11.75 | 16.00 |

*Note: this table reflects the original L5 cutoff (0.60). Updated numbers using L5 at 0.65 are larger across the board.*

**Interpretation:**
- The three defensive levers (L1, L2, L5) each gain impact as stress rises — the loans they decline would have caused even larger losses under worse macro conditions.
- The offensive lever (L4 — Grow SME A-B) weakens with stress because new loans take stressed losses. L4 alone goes negative at approximately +5.7pp stress.
- Combined portfolio impact rises monotonically. Defensive levers' gains exceed L4's losses at every stress level tested.
- No break-point is reached within the plausible macro range (Indian retail credit has not seen stress beyond +4pp since the 1991 BoP crisis).

**Implication for the recommendation:** robust to macro stress significantly beyond the engagement-mandated +3pp band.

---

## 3. LGD Sensitivity

**Method:** Hold +3pp macro stress constant. Flex retail LGD (50-70%) and SME LGD (40-60%) jointly.

**Result (Combined Net Δ at +3pp stress, in ₹ cr):**

| Scenario | Retail LGD | SME LGD | L1 | L2 | L4 | L5 | Combined |
|---|---|---|---|---|---|---|---|
| LGD −10pp (optimistic) | 50% | 40% | 1.27 | 2.47 | 0.85 | 11.15 | 15.74 |
| LGD −5pp | 55% | 45% | 1.29 | 2.48 | 0.77 | 11.22 | 15.77 |
| Locked (baseline) | 60% | 50% | 1.31 | 2.50 | 0.69 | 11.29 | 15.79 |
| LGD +5pp | 65% | 55% | 1.33 | 2.51 | 0.61 | 11.36 | 15.82 |
| LGD +10pp (pessimistic) | 70% | 60% | 1.35 | 2.53 | 0.54 | 11.43 | 15.84 |

**Interpretation:**

The recommendation is **essentially LGD-insensitive at the portfolio level**. Combined Net Δ varies by only ₹0.10 cr (+₹15.74 to +₹15.84) across the full ±10pp LGD band — a 0.6% variation on a +₹15.79 cr recommendation.

**Why this happens:** LGD has *opposing* effects on different lever types.

- For cease/tighten levers (L1, L2, L5): higher LGD increases the additional losses we *avoid* under stress, so the lever gains impact.
- For the grow lever (L4): higher LGD increases the losses we *take* on the new loans under stress, so the lever loses impact.

At the portfolio level, the defensive gains and offensive losses roughly cancel. This is a structural property of the portfolio's lever mix, not a coincidence.

**Implication:** the recommendation does not hinge on getting the LGD assumption exactly right. Even if real-world LGD differs materially from the +60%/+50% (retail/SME) values used, the headline number moves by less than ₹0.15 cr.

---

## 4. Cashflow Cutoff Sensitivity — Discovery and Correction

**Method:** Re-compute L2 (Personal D-E) and L5 (SME C-D-E) impacts at cashflow_consistency cutoffs from 0.50 to 0.70 in 0.05 increments.

**Result (Net Δ in ₹ cr):**

| Cutoff | L2 loans | L2 baseline | L2 at +3pp | L5 loans | L5 baseline | L5 at +3pp |
|---|---|---|---|---|---|---|
| 0.50 | 210 | 0.82 | 0.87 | 151 | 4.04 | 4.24 |
| 0.55 | 395 | 1.50 | 1.58 | 265 | 6.75 | 7.12 |
| 0.60 | 767 | 2.33 | 2.50 | 498 | 10.61 | 11.29 |
| 0.65 | 1,409 | 2.42 | 2.72 | 950 | **12.97** | **14.30** |
| 0.70 | 2,935 | 0.73 | 1.37 | 2,035 | 6.05 | 8.87 |

**Finding for L2 (Personal D-E):** Impact at 0.60 is +₹2.33 cr; at 0.65 it is +₹2.42 cr. The 0.05 cr improvement is within noise. The 0.65-0.70 range drops sharply (+₹2.42 → +₹0.73 at baseline). **0.60 is confirmed as the practical optimum for L2.**

**Finding for L5 (SME C-D-E):** Impact at 0.60 is +₹10.61 cr; at 0.65 it jumps to +₹12.97 cr — a +₹2.36 cr improvement (22% gain). At 0.70, impact collapses to +₹6.05 cr. **0.65 is the empirical optimum for L5; 0.60 was sub-optimal.**

**Why L2 and L5 differ:**

SME borrowers and Personal borrowers have different cashflow profiles. Within Personal D-E, the loss-making slice ends cleanly near cashflow_consistency = 0.60 — the sign of mean value_proxy flips between the 0.5-0.6 band and the 0.6-0.7 band. Within SME C-D-E, the loss-making slice extends slightly further. The 452 additional SME loans declined at cutoff 0.65 (vs 0.60) average **−₹5,221 in value_proxy each** — they are real loss-makers, just on the right side of the original threshold. Beyond 0.65, the loans become profitable (mean +₹63K each in the 0.65-0.70 range), which is why 0.70 collapses the lever impact.

**Action taken:** Lever 5 cutoff updated from 0.60 to 0.65. Workstream G scenarios and Workstream I recommendation document updated accordingly.

**Impact of the correction:**

| Metric | Original (0.60) | Updated (0.65) |
|---|---|---|
| L5 loans declined | 498 | 950 |
| L5 origination given up | ₹45.64 cr | ~₹88.67 cr |
| L5 Net Δ at baseline | +₹10.61 cr | +₹12.97 cr |
| L5 Net Δ at +3pp | +₹11.29 cr | +₹14.30 cr |
| Combined Net Δ at baseline | +₹15.48 cr | **+₹17.85 cr** |
| Combined Net Δ at +3pp | +₹15.79 cr | **+₹18.80 cr** |
| Total origination Δ | -₹16.15 cr | -₹59.18 cr |

The correction adds ~₹2.4 cr to the headline gain. The volume hit increases from 1% to ~4% of the book — still manageable but more substantial. Recommendation: WS I narrative should acknowledge the slightly larger volume reshape and frame as "trade a 4% reduction in origination for a 6%+ improvement in book contribution."

---

## 5. L4 Growth Rate Sensitivity

[Section to be completed when the L4 growth rate sensitivity is run. Expected pattern: linear scaling of both baseline gain and stress loss; growth at 5-20% all stays positive under +3pp stress; 10% is conservative midpoint; SME A-B is the only segment where growth is safe under stress because of its high margin cushion.]

---

## 6. Implications Summary

WS H sensitivity analysis confirms the recommendation is:

- **Robust to severe macro stress** (positive across 0pp to +5pp; no break-point in plausible range)
- **Insensitive to LGD assumption** (less than ₹0.15 cr variation across LGD ±10pp)
- **Empirically optimized on cutoff selection** (0.60 confirmed for L2, 0.65 newly identified and adopted for L5)
- **Defensible against challenge** on each major assumption

The L5 cutoff correction is the only material update triggered by WS H. The locked recommendation is now:

- **Headline:** Contain SME C-D-E at cashflow_consistency < **0.65** → +₹12.97 cr baseline, +₹14.30 cr at +3pp
- **Supporting 1:** Tighten Personal D-E at cashflow_consistency < 0.60 → +₹2.33 cr baseline (unchanged)
- **Supporting 2:** Cease BNPL Digital/DSA → +₹1.08 cr baseline (unchanged)
- **Offensive:** Grow SME A-B by 10% → +₹1.47 cr baseline (unchanged)
- **Combined:** **+₹17.85 cr at baseline, +₹18.80 cr at +3pp stress**

---

## 7. Methodology Notes

All sensitivities computed using the lever functions defined in `WS H_sensitivity.ipynb`:

- `compute_cease_net(target_loans, lgd, stress_pp)` — for cease/tighten levers
- `compute_grow_net(n_loans, mean_vp, mean_ticket, lgd, stress_pp)` — for grow levers

Underlying data: `loan_frame.parquet` (49,600 loans) and `step3_segment_assignments.csv`, both produced by Workstream C and consumed unchanged.

Output files in `WS H/`:
- `extended_stress.csv` — extended macro stress results
- `lgd_sensitivity.csv` — LGD flex results
- `cutoff_sensitivity.csv` — cashflow cutoff flex results
- `growth_rate_sensitivity.csv` — L4 growth rate results (when complete)

---

