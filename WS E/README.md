# Workstream E — Segmentation: Final Package (clean)

This package is internally consistent: **there is exactly one canonical segmentation**, and its Gate-3 validation was run on *those* segments. All earlier intermediate versions have been removed to prevent confusion.

## Read this first — the one canonical answer lives in `FINAL/`

The deliverable is the **6-segment, product × risk-grade scheme** in `FINAL/`:

| # | Segment | % book | Default (seasoned) | Mean value | Posture |
|---|---|---|---|---|---|
| 1 | BNPL (grade A–C) | 25.9% | 5.7% | −₹661 | Maintain (fix economics) |
| 2 | Personal Prime (A–B) | 20.1% | 4.3% | +₹4,578 | Maintain |
| 3 | Personal Non-prime (C–E) | 24.9% | 10.6% | +₹5,923 | Contain |
| 4 | SME Prime (A–B) | 9.2% | 3.1% | +₹32,204 | Grow |
| 5 | SME Non-prime (C–E) | 11.0% | 8.1% | +₹40,955 | Grow (guardrails) |
| 6 | Subprime BNPL (D–E) | 8.9% | 44.1% | −₹1,642 | Exit |

All 49,600 loans covered once; value reconciles to ₹473.6M. **Gate 3 = PASS (13/13), validated on these exact segments.**

## Folder guide

| Folder / file | What it is | Use it for |
|---|---|---|
| `FINAL/` | **The canonical deliverable** — assignments, metrics (with hooks), risk×value matrix, policy hooks (DRAFT), and the Gate-3 results computed on these segments | This is the answer |
| `frames/` | The analytical tables built in Step 2 (loan / customer / product-cell) | Inputs for F, G, I |
| `inputs/` | Source data from Workstream C (4 tables + value components + dictionary) | Reproduce from scratch |
| `validation_only/` | `_true_latent_risk` — the generator's hidden field. **Never a feature** (A-019); creditworthiness-oriented (higher = safer). Included only so the 4 z-based Gate-3 checks reproduce | Audit / verification |
| `process_trail/` | **How we got here, NOT the final answer** — the heuristic baseline (Step 3), the tree and clustering methods, the head-to-head comparison memo, the build/validation scripts, and the backtest-review response | Methodology audit |
| `WS_E_closeout.md` | E's final state and what changed | Status |
| `WS_F_handoff_memo.md` | Kickoff brief for the Early Warning System | Workstream F |

## What was removed (and why)

Three generations of the segmentation existed during the build; only the last is correct. The two superseded versions — the 7-segment version and the APR-threshold 6-segment version (both naming segment 6 "High-APR Danger") — **have been removed**, because the interest-rate threshold was just a relabel of product × grade and it produced contradictory value numbers. Segment 6 is now defined cleanly as **Subprime BNPL (grade D–E)**. The method-comparison memo in `process_trail/` still discusses the earlier hybrid framing — that is intentional, as a record of how the decision was reached.

## Open before sign-off (governance, not analysis)

1. Risk Consultant + EM **ratify the policy hooks** (`FINAL/E_final_policy_hooks.md`, currently DRAFT).
2. **Joint Gate-3 signature**, then freeze `FINAL/E_final_segment_assignments.csv` and hand to F, G, I.
