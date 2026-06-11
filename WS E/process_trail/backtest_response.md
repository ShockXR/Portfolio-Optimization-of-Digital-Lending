# Workstream E — Response to the Backtesting Review (DRAFT)

*Our point-by-point reply to "Backtesting Review — Universal WS E." **No files have been changed yet** — this is the proposed position and mitigation list, to be actioned only on your go-ahead.*

---

## 1. Overall stance

This is a fair, rigorous review and we accept the bulk of it. Its out-of-time test is a genuinely valuable addition we didn't run ourselves, and its three substantive criticisms are largely correct. Two of them we had already flagged in our own memos; one (the tree relabel) we concede fully and can even sharpen. The rest are housekeeping fixes. Nothing in the review overturns the core result — the 6-segment scheme stands.

---

## 2. Points we accept with no argument

- **Numbers reproduce exactly** — agreed; that was the intent of the self-checking scripts.
- **Out-of-time test passed** (value ranking preserved, risk rank ρ≈0.94, High-APR 42.8%→41.4%) — a welcome, stronger test than our in-sample bootstrap. We'd like to fold it into the validation record.
- **Grade staircase 2→4→8→18→30%** — matches our R1 check exactly.
- **Value ≠ creditworthiness** — agreed and already flagged by us (Step 9 found value uncorrelated with the latent-risk field, r≈0.00). "Grow" is a product/economics call, not a low-risk call.
- **We correctly refused to use clustering as the answer** — agreed; that boundary was deliberate.

---

## 3. Responses to the substantive findings

### Finding 1 — "The decision tree's discovery is an illusion" → **CONCEDE (fully), with one fair nuance**

The review is correct, and our own data confirms it: APR is a near-deterministic function of product×grade (each cell fixed to within ±0.5). The "High-APR Danger" segment is 92% BNPL D/E + 8% Personal E, entirely grade D/E. The 32.4% threshold carries **no information beyond product×grade** — and is actually *worse* than a clean cell rule, because the pricing jitter means it arbitrarily splits the BNPL-D cell (only 88% of BNPL-D lands above the line).

*Fair nuance (not a rebuttal):* relative to the **delivered baseline**, which lumped **all** BNPL into a single bucket regardless of grade, carving out the worst-grade BNPL *was* a real, actionable refinement — the baseline as-built hid it. So the distinction is genuine; the **label and the APR-threshold definition** are what mislead.

**Mitigation:** redefine and rename the segment by its true cell — **"Subprime BNPL (grade D–E) + Personal E"** — instead of an APR cut. This removes the misleading "high-APR discovery" framing *and* the arbitrary jitter-split, and slightly cleans up membership. *Files: assignments, metrics, matrix, comparison memo.*

### Finding 2 — "Clustering's C4 is leakage; unusable as a segmentation" → **CONCEDE (framing)**

Agreed. C4 is defined by in-progress-distress signals (bounces, shocks, utilisation) knowable only *after* a loan starts failing. Important to state clearly: **no behaviour entered the final hybrid** (it uses only product/grade/APR), so this leakage never touched the deliverable. The clustering was a benchmark candidate, correctly rejected, and C4 routed to Workstream F.

**Mitigation:** relabel clustering explicitly in the memo as a **"behavioural early-warning input (WS F), not a segmentation,"** and state the leakage plainly rather than leaving it implied. *Files: comparison memo wording.*

### Finding 3 — "Clustering is really 3 groups, not 4" → **AGREE (already stated)**

We said this ourselves (C1/C2 are statistical twins; "≈3 meaningful groups"). No new change beyond Finding 2's relabel. *Files: none.*

### Finding 4 — "Short-window backtest is misleading (survivorship); seasoned basis is right" → **AGREE**

The review validates our seasoned-basis choice and correctly warns the next analyst about the survivorship illusion. 

**Mitigation:** add an explicit methodology note: *do not use fixed-early-window default — fast write-offs vanish early and make risky buckets look safe; use the seasoned (MOB≥3) basis.* *Files: validation/methodology note.*

---

## 4. Housekeeping (all conceded — fixable)

### H1 — Two files disagree (6-bucket vs 7-bucket; −₹681 vs −₹782) → **CONCEDE**

Cause: the corrected **6-segment, all-loans-value** file supersedes the original **7-segment, seasoned-value** file, but the old one is still in the package. **Mitigation:** delete the superseded 7-segment / seasoned-value files; canonical = 6 segments, value on all loans, default on seasoned. *Files: remove `step6_hybrid_assignments.csv`, `step6_hybrid_metrics.csv`, `slide7_*` (7-seg).*

### H2 — `step6_hybrid.py` won't run (wrong data path) → **CONCEDE**

It points at `out/data/parquet/...`; the frame lives in `out/frames/`. **Mitigation:** fix the path (or retire it in favour of the working `step6_apply_fixes.py`). *Files: `step6_hybrid.py`.*

### H3 — Four Gate-3 checks can't be re-verified (z not shipped) → **CONCEDE, with rationale**

This is the right catch. The `true_latent_risk` (z) field is **deliberately excluded from the delivered analytical dataset** (A-019 — it must never be a feature). But for a *sign-off* package the z-based checks should be reproducible. **Mitigation:** include `_true_latent_risk.parquet` in the Gate-3 verification bundle as a clearly-marked **validation-only** file (not part of the analytical data). *Files: add z to the gate pack + a README note.*

---

## 5. One thing to add to the record (helps the verifier)

Our Step 9 found that `true_latent_risk` is oriented as **creditworthiness (higher = safer)**, not risk — which is why the z-checks read as a strong *inverse* alignment (ρ = −0.89). When we ship z (H3), we should document this orientation so the reviewer's 4 currently-trusted checks reproduce cleanly rather than appearing to "fail" on a sign convention.

---

## 6. Proposed change-list (pending your go-ahead — nothing done yet)

| # | Change | Trigger finding | Files affected |
|---|---|---|---|
| 1 | Rename + redefine "High-APR Danger" → "Subprime BNPL (D–E) + Personal E" by cell, not APR | F1 | assignments, metrics, matrix, memo |
| 2 | Relabel clustering as "WS F early-warning input, not segmentation"; state leakage plainly | F2 | comparison memo |
| 3 | Add survivorship/seasoning methodology warning | F4 | validation note |
| 4 | Delete superseded 7-segment / seasoned-value files; declare the 6-seg/all-loans file canonical | H1 | remove old files |
| 5 | Fix the data path in `step6_hybrid.py` (or retire it) | H2 | `step6_hybrid.py` |
| 6 | Ship `_true_latent_risk.parquet` (validation-only) + note its creditworthiness orientation | H3, §5 | gate pack + README |
| 7 | (Optional) Fold the reviewer's out-of-time test into the validation record | §2 | validation note |

**Net effect:** the segmentation itself doesn't change in substance — segment 6 is re-defined slightly cleaner and renamed; everything else is labelling, file hygiene, and verification packaging. Say the word and I'll apply whichever rows you approve.
