# Stage 4 — Instructor Review

**Student:** Chieu Chu
**Company:** FPT Corporation (FPT:HOSE)
**Spec:** `docs/specs/2026-05-24-chu-fpt-spec.md`
**Reviewed:** 2026-05-24

---

## Observations

### Part A — Model Specification

- **Scope & Objective (Section 1):** Well-defined — correctly identifies VAS reporting standard, VND billions, FY2025/FY2024 comparative periods, and analytical objective. Audience framing is appropriate.
- **Model Architecture (Section 2):** Six-tab workbook documented with tab descriptions, color coding convention, and named-range convention. Data flows correctly described (left-to-right, top-to-bottom).
- **Data Inputs (Section 3):** Comprehensive — Balance Sheet has 20+ named ranges with FY2025/FY2024 values, Income Statement has 12 items, Cash Flow has 10+ items. Formulas are documented inline showing how derived totals are calculated. The VAS-specific treatment of `INC_depreciation` (sourced from CF Code 02 D&A add-back) is analytically correct.
- **Derived Inputs (Section 4):** 21 intermediate calculations with explicit named-range formulas and computed values. Includes averages, daily rates, and working capital — all the building blocks the Ratios tab needs.
- **Ratio Definitions (Section 5):** 29 ratio rows across all six categories (Performance, Profitability, Efficiency, Leverage, Liquidity, Du Pont). All in named-range notation with computed values shown.

### Part A — Ratios & Validation

- **Validation Rules (Section 6):** 6 rules — BS balance both years, Du Pont ROA vs. direct ROA, Du Pont ROE time-mismatch caveat, net income allocation, EVA sign check. The time-mismatch explanation (structural feature, not error) is the exact caveat that prevents Stage 5 false-positives.

### Part B — Analysis Specification

- **Analysis Requirements (Section 7):** Per-category requirements with interpretation guidance, benchmark ranges (e.g., "tech/telecom conglomerate in Southeast Asia typically targets ROE of 15–25%"), and cross-category connections. Well-scoped.
- **Du Pont Decomposition (Section 8):** Full 4-factor decomposition with primary driver analysis (OPM as the main contributor), sustainability assessment (flagging 33% YoY short-term debt growth), and the required time-mismatch note.
- **Strategic Recommendations (Section 9):** Framework specifies 3–5 recommendations with evidence standard and cross-category scope requirement.
- **Output Format (Section 10):** Section-by-section layout with word-count targets and professional tone guidance.

### Prompt Log & HIL Iteration

- **Prompt log:** Documented in a separate iteration file. Round 1 prompt is specific (lists 4 inputs, names all sections, requests named-range notation). Assumptions confirmed pre-draft.
- **HIL iteration:** Exceptional — caught two material errors in the v1.0 draft:
  1. **Dividends:** LLM used 3,185 B VND (a rounded declared estimate) instead of 4,573.754 B VND (the cash actually paid per CF statement). Root cause correctly identified: spec didn't specify which source to use. Impact: 44% understatement of dividend outflow, 1,389 B VND overstatement of retained earnings.
  2. **Shares outstanding:** LLM rounded to 1.7B instead of 1,703,507,121. Impact: 336 B VND market-cap understatement.
- Both corrections were made in v2.0 with source annotations added to prevent recurrence at Stage 5.

---

## Kindly-worded suggestions for improvement

- **VAS depreciation sourcing is well-handled.** Pulling `INC_depreciation` from the CF statement's D&A add-back (Code 02) is the correct approach for VAS companies where the income statement bundles depreciation in COGS/SGA. Document this treatment explicitly in your Stage 5 analysis notes so reviewers understand the methodology.
- **Minor: iteration log date typo** — the file is named `2025-05-24-chu-fpt-stage4-iteration.md` (2025 instead of 2026). A quick rename for consistency: `git mv deliverables/2025-05-24-chu-fpt-stage4-iteration.md deliverables/2026-05-24-chu-fpt-stage4-iteration.md`.
- **The dividend HIL catch is exemplary.** The root-cause analysis ("the LLM pulled a rounded declared-dividend estimate, not the cash actually paid") and the impact quantification ("44% understatement") are exactly the kind of critical human review the rubric rewards. Carry this analytical discipline into Stage 5's manual verification pass.

**Looking ahead to Stage 5:** Run your Stage 4 spec through the LLM of your choice, then verify at least five of its ratio outputs against the workbook by hand. Your spec is detailed enough that the LLM output should be high-quality; the key Stage 5 task is the manual verification and the retrospective on what the LLM got right and wrong.
