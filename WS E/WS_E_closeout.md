# Workstream E — Closeout Memo

**Status:** complete. Gate 3 (statistical) PASS (13/13). Crucial review fixes applied. Awaiting only the policy-hook ratification + joint Gate-3 signature.

---

## Final segmentation (canonical — supersedes all earlier versions)

Pure **product × risk-grade** scheme, 6 segments. Default on the seasoned basis (MOB ≥ 3); value on all loans. All 49,600 loans covered once; total value reconciles to ₹473.6M.

| # | Segment | % book | Default (seasoned) | Mean value | Quadrant | Posture (hook — DRAFT) |
|---|---|---|---|---|---|---|
| 1 | BNPL (grade A–C) | 25.9% | 5.7% | −₹661 | Maintain | Fix economics — value-negative at scale |
| 2 | Personal Prime (A–B) | 20.1% | 4.3% | +₹4,578 | Maintain | Nurture & deepen |
| 3 | Personal Non-prime (C–E) | 24.9% | 10.6% | +₹5,923 | Contain | Price for risk, cap exposure, monitor via F |
| 4 | SME Prime (A–B) | 9.2% | 3.1% | +₹32,204 | Grow | Expand aggressively |
| 5 | SME Non-prime (C–E) | 11.0% | 8.1% | +₹40,955 | Grow (guardrails) | Grow selectively |
| 6 | Subprime BNPL (D–E) | 8.9% | **44.1%** | −₹1,642 | Exit | Halt & re-underwrite |

Canonical files: `E_final_segment_assignments.csv`, `E_final_segment_metrics.csv`, `E_final_risk_value_matrix.png`.

---

## Crucial fixes applied (from the backtest review)

1. **Segment 6 redefined and renamed.** The old "High-APR Danger (>32.4%)" was conceded to be a relabel of product×grade (APR is fixed by product×grade ±0.5). It is now defined cleanly as **Subprime BNPL (grade D–E)** — no APR threshold, no arbitrary jitter-split. Its true default rate is 44.1% (the previous APR cut diluted it to ~42%).
2. **One canonical file set.** The duplicate 6-vs-7-segment / seasoned-vs-all-loans-value files are superseded by the single `E_final_*` set above. Default = seasoned; value = all loans.
3. **Verification data shipped.** `_true_latent_risk_VALIDATION_ONLY.parquet` is included so the four `z`-based Gate-3 checks can be reproduced. **This field is validation-only and was never a feature (A-019).** Note its orientation: it is **creditworthiness** (higher = safer), which is why the z-checks read as a strong *inverse* alignment with risk.

## Deferred (non-blocking, optional)

- Relabel clustering as "WS F early-warning input" in the comparison memo (cosmetic).
- Fold the reviewer's out-of-time test into the validation record (nice-to-have; it passed).
- Retire `step6_hybrid.py` (broken path) — superseded by the canonical build.

## Open before sign-off (governance, not analysis)

- Risk Consultant + EM **ratify the policy hooks** (currently DRAFT).
- **Joint Gate-3 signature**, then freeze the assignment table and hand to F, G, I.

The segmentation is analytically complete and validated; what remains is signatures and labelling.
