---
template: spec-retrospective
purpose: "Structured self-evaluation of a Stage 4 technical specification after seeing how an LLM executed it at Stage 5 — surfaces spec gaps with evidence, not impressions"
audience: student
fields_required: [date, author, company, spec_file, stage5_output, section_verdicts, top_gaps, revisions, effectiveness_rating, forward_link, process_feedback]
naming_convention: "YYYY-MM-DD-{lastname}-{company-slug}-spec-retrospective.md (lives in deliverables/)"
courses: [BUS-629, FIN-321, BUS-314]
---

# Stage 4 Spec — Retrospective

**Author:** Chieu Chu
**Date:** 2026-05-24
**Company:** FPT Corporation · FPT · HoSE
**Spec being evaluated:** `docs/specs/2026-05-24-chu-fpt-spec.md` (Version 2.0)
**Stage 5 LLM output:** `deliverables/2026-05-24-chu-fpt-analysis.md`
**Verification file:** `analysis/validation/2026-05-24-chu-fpt-stage5-verification.md`

---

## 1. Section-by-section verdict

| Spec section | Verdict | Symptom in Stage 5 output |
|---|---|---|
| **Part A.1 — Scope & Objective** | Clear | Stage 5 opened with the correct company (FPT Corporation), fiscal period (FY2025 vs. FY2024), reporting standard (VAS), currency (B VND), and audience (BUS-629 graders) — verbatim from the spec. No guessing required. |
| **Part A.2 — Model Architecture** | Clear | Stage 5 correctly referenced the six-tab workbook, color-coding convention, and left-to-right data-flow rule. No tab was omitted or mis-described. |
| **Part A.3 — Data Inputs** | Vague | Several Cash Flow named ranges (e.g., `CASH_operating`) were defined with cell references (`=C7+C8+C15`) rather than named-range notation. A Stage 5 LLM has no workbook to resolve `C7`; it can only reproduce the stated formula value, not verify the formula independently. The spec also listed `INC_dividends` = 4,573.754 B VND as a data input but placed it inside the Income Statement table — dividends are sourced from the Cash Flow Statement and the spec's annotation ("from Cash Flow Statement") was added only in the HIL revision, leaving an ambiguous source for any executor who reads v1.0. |
| **Part A.4 — Named Range Conventions** | Vague | The prefix table defined `BAL_[item]_curr / _prior` as a convention but never listed a `BAL_debt_total` range combining short-term and long-term debt. The verification table showed that when the Stage 5 verification used `BAL_debt_total_2025 / BAL_equity_total_2025`, there was no named range to resolve it — forcing a choice between `BAL_liabilities_total_curr` (1.015x) and `BAL_debt_short_term_curr + BAL_debt_long_term_curr` (0.48x), both materially different from the spec's reported Debt-to-Equity of 0.044x. The spec never defined which debt concept maps to each leverage ratio. |
| **Part A.5 — Derived Inputs** | Clear | Every derived input was given with its named-range formula and a computed value. The Stage 5 analysis correctly reproduced ATOI (11,872.049 B VND), market cap (163,536.684 B VND), and all start-of-year and average figures without error. |
| **Part A.6 — Ratio Definitions & Formulas** | Vague | The spec stated all formulas correctly per its own convention, but three formulas deviated silently from textbook standards without disclosure: (1) ROA used ATOI + start-of-year assets instead of net income + average assets, producing 16.49% vs. 14.03%; (2) DSO used `startYear_receivables` instead of year-end receivables, giving 59.3 days vs. 75.0 days; (3) Inventory Turnover used `startYear_inventory` instead of the two-year average, giving 23.82× vs. 21.84×. The Stage 5 analysis reported all three spec-consistent values without flagging any deviation from standard convention, because the spec never instructed it to. |
| **Part A.7 — Validation Rules** | Clear | All six validation checks were addressed explicitly in the Stage 5 analysis: both balance-sheet equations cited, Du Pont ROA confirmed at 16.49%, Du Pont ROE vs. direct ROE gap (0.01 pp) explained with the time-mismatch note, net income allocation confirmed (4,573.754 + 6,658.585 = 11,232.339), and EVA sign confirmed positive. |
| **Part B.8 — Analysis Requirements** | Clear | The per-category guidance (benchmarks, cross-category connections, specific figures to cite) was followed precisely. The Efficiency section flagged receivables growth (+27%) against revenue growth; the Leverage section distinguished short-term from long-term debt with the 33% YoY figure; the Liquidity section connected collection period to the quick ratio — all per spec instruction. |
| **Part B.9 — Du Pont Decomposition** | Clear | The four-component breakdown was correct (2.015 × 0.974 × 16.93% × 0.9461 = 31.43%), the primary driver (margin) was correctly identified, the sustainability assessment addressed the short-term debt risk, and the time-mismatch note was included as required. |
| **Part B.10 — Strategic Recommendation Requirements** | Vague | The spec required 3–5 recommendations spanning ≥3 ratio categories, with each citing at least one ratio value and one financial statement data point. The Stage 5 analysis produced five recommendations and met all stated criteria. However, one recommendation (Rec 5: accounts receivable securitisation) applied a structured-finance technique not covered in BUS-629 course materials. The spec placed no boundary on recommendation sophistication or instrument type, so the LLM reached beyond expected course scope without a guardrail. |
| **Part B.11 — Output Format** | Clear | All ten sections appeared in the correct order. Word counts were within the target ranges: Executive Summary (~160 words vs. ~150 target), Du Pont (~380 words vs. ~300 target, appropriately long given the time-mismatch note). The ratio summary table covered all 25+ ratios. Tone was professional and third-person throughout. |

---

## 2. Top three gaps with evidence

### Gap 1: ROA formula convention undisclosed — ATOI vs. net income, start-of-year vs. average assets

- **Where it surfaced:** Stage 5 Profitability section reported ROA (start assets) = 16.49% as the primary figure and labelled it consistent with spec convention. The verification table (`stage5-verification.md`, Row 1) showed the standard textbook formula — net income / average assets — produces 14.03%, a 246 bp understatement. The analysis cited 16.49% when discussing FPT against "Southeast Asian tech-telecom benchmarks" without noting that those benchmarks almost certainly use net income / average assets.
- **Spec cause:** Section 5 (Profitability table) listed the formula as `currentYear_after_tax_operating_income / startYear_total_assets` but contained no note explaining (a) why ATOI rather than net income, or (b) why start-of-year rather than average. Any analyst benchmarking FPT's 16.49% ROA against a Bloomberg or FactSet peer median is making an apples-to-oranges comparison.
- **Fix (exact language):** Add a footnote row beneath the ROA formula cell in Section 5: *"Convention note: this model uses after-tax operating income (ATOI) in the numerator to isolate operating performance from capital structure. Net income / average assets = 11,232.339 / 80,070.993 = 14.03%. When benchmarking against peers, use 14.03% to ensure comparability with databases that default to net income and average assets."*

---

### Gap 2: DSO uses start-of-year receivables without flagging the deviation from standard convention

- **Where it surfaced:** The Stage 5 Efficiency section reported Average Collection Period = 59.3 days, sourced from `startYear_receivables / currentYear_daily_sales_average`. The Stage 5 analysis then observed that "receivables grew 27% YoY" as a risk flag, yet the 59.3-day DSO figure conceals the severity of that risk: computed on year-end receivables (the standard DSO convention), the figure is 75.0 days — a 15.7-day gap the analysis never disclosed. A BUS-629 grader comparing 59.3 days to a peer benchmark of 45 days sees a 14-day gap; the actual gap is 30 days.
- **Spec cause:** Section 5 (Efficiency table) listed the formula as `startYear_receivables / currentYear_daily_sales_average` but included no note flagging the deviation from the standard `(BAL_receivables_curr / INC_sales) × 365` convention. Section 7 (Analysis Requirements) instructed the LLM to "flag YoY receivables growth" but did not instruct it to present the year-end DSO alongside the spec-convention DSO.
- **Fix (exact language):** Add to the Average Collection Period row in Section 5: *"Convention note: this model uses prior-year (start-of-year) receivables to match the denominator convention used in asset turnover and inventory turnover. Standard DSO using year-end receivables = (14,402.017 / 70,112.825) × 365 = 75.0 days. Report both figures in the Efficiency section and note the 15.7-day gap when benchmarking."*

---

### Gap 3: Debt-to-Equity definition too narrow — long-term debt only, short-term debt unaddressed

- **Where it surfaced:** The Stage 5 Leverage section reported Long-term Debt-to-Equity = 0.044x and described FPT as having "virtually no long-term financial leverage." The verification table (Row 5) showed that total liabilities / equity = 1.015x, a 23× difference. The analysis separately discussed the 33% YoY increase in short-term debt as a risk but never connected it to a headline leverage ratio — leaving the reader with two disconnected observations rather than a coherent leverage picture.
- **Spec cause:** Section 5 (Leverage table) defined `RATIO_leverage` as `currentYear_assets_total / currentYear_equity` = 2.015x (a leverage multiplier) and separately defined "Long-term Debt-to-Equity" as `currentYear_debt_long_term / currentYear_equity` = 0.044x. Neither the leverage multiplier (2.015x) nor the LT D/E (0.044x) captures total interest-bearing debt (short + long = 21,073.487 B VND), giving a total D/E of 0.48x. The spec never defined or required a total-debt D/E ratio, so the LLM never computed one.
- **Fix (exact language):** Add a row to the Leverage table in Section 5: *"`Total Debt-to-Equity` | `(BAL_debt_short_term_curr + BAL_debt_long_term_curr) / BAL_equity_shareholders_curr` | (19,169.697 + 1,903.790) / 43,748.041 = **0.48x** | x | Total interest-bearing leverage; required alongside Long-term D/E (0.044x) to give a complete picture of FPT's debt structure."* And add to Section 7 (Leverage analysis requirements): *"Report both Long-term D/E (0.044x) and Total D/E (0.48x) and explain why the gap is large — FPT's leverage is short-term in character."*

---

## 3. Revisions

1. **Add a "Convention note" column to every ratio row in Section 5 that deviates from the textbook standard, stating the textbook alternative formula and its computed value for FPT FY2025.** — addresses Gap 1 (ROA) and Gap 2 (DSO), and would have caught the inventory turnover deviation (spec: 23.82×; textbook average: 21.84×) before Stage 5 ran.

2. **Add `Total Debt-to-Equity` as an explicit named range and ratio row in Section 5, defined as `(BAL_debt_short_term_curr + BAL_debt_long_term_curr) / BAL_equity_shareholders_curr` = 0.48×, and require the Stage 5 analysis to report it alongside Long-term D/E and explain the structural gap.** — addresses Gap 3.

3. **Add a scope constraint to Section 9 (Strategic Recommendation Requirements): "Recommendations must not involve derivative instruments, structured-finance products, or off-balance-sheet techniques unless explicitly covered in BUS-629 course materials. Acceptable tools include: capital allocation decisions, working capital policy, refinancing into conventional debt instruments, and dividend/buyback policy."** — addresses the Part B.10 gap (Rec 5 securitisation fell outside expected BUS-629 scope).

---

## 4. Effectiveness rating

| Rating | Anchor |
|:---:|---|
| **5** | I would hand this spec to a junior analyst and trust their output without re-checking. |
| **4** | Solid overall; one section needs sharpening before I'd ship it. |
| **3** | Workable with revisions; spec has gaps the LLM had to guess around. |
| **2** | Substantial rework needed; LLM output diverged in meaningful ways traceable to the spec. |
| **1** | Spec is not yet usable as a standalone artifact. |

**My rating: 3**

**Justification:**

The spec was precise enough that the Stage 5 LLM produced zero formula errors, hit all ten required output sections, followed all cross-category connections, and correctly executed the Du Pont decomposition including the time-mismatch disclosure — evidence of a structurally sound Part A and a well-specified Part B. The six validation rules were all addressed explicitly. These are rating-4 outcomes.

However, the verification table documented that 4 of 5 ratios produced values materially different from standard textbook conventions, and none of those deviations were disclosed in the Stage 5 analysis. The 59.3-day DSO (vs. 75.0 days on year-end receivables) and the 0.044x D/E (vs. 0.48x on total debt) are not minor rounding differences — they would lead a BUS-629 grader or an external reader to a substantially different conclusion about FPT's collection efficiency and leverage profile. A spec rated 4 would have caught these in a convention-note column; this spec did not. One recommendation (receivables securitisation) also exceeded expected course scope without a guardrail in the spec. Three sections needing revision (A.6, A.4, B.10) puts this firmly at a 3.

---

## 5. Forward link

In the next spec, every ratio formula that deviates from the textbook convention will carry an inline "convention note" giving the textbook alternative, its computed value for the company being analysed, and an instruction to the Stage 5 LLM to report both figures and explain the gap — so that a benchmarking reader gets two anchors rather than one potentially misleading number.

---

## 6. Retrospective process feedback (≤150 words)

The section-by-section verdict table (Section 1) forced a finding I would not have reached in a free-form write-up: the gaps were not evenly distributed — they concentrated almost entirely in Part A.6 (Ratio Definitions), not across all eleven sections. Seven sections earned "Clear" with no hesitation; the three "Vague" verdicts all traced back to the same root cause — formulas that deviated from textbook convention without disclosure. That pattern is invisible in narrative reflection.

**Structural suggestion:** Add a dedicated "Convention deviation?" column (Y/N) to Section 5 of the spec template itself — not the retrospective — so the spec writer is forced to check, at writing time, whether each formula matches the textbook standard. The retrospective template could then ask: "For each Y in that column, did the Stage 5 LLM disclose the deviation?" This would shift the convention-gap check from post-mortem to pre-execution, which is where it has the most leverage.

---

## Notes for graders

This retrospective is part of the Stage 5 deliverable rubric. Strong submissions are:

- **Evidence-tied.** Every verdict, gap, and rating points at a specific symptom in the Stage 5 LLM output.
- **Specific in revisions.** "Add more detail" earns less than "Add a Derived Inputs row defining `avgAssets_2025 = (BAL_assets_total_2025 + BAL_assets_total_2024) / 2`."
- **Honest in rating.** A self-rated **5** with weak Stage 5 output and no specific evidence is a flag, not a flex.
- **Thoughtful in Section 6.** Cohort-level patterns in Section 6 inform next semester's template — this section is read with that in mind.
