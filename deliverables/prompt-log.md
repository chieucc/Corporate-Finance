# Prompt Log — BUS-629 Project (All Stages)

**Student:** Chieu Chu · ChieuCC@fpt.com
**Company:** FPT Corporation (FPT · HoSE)
**Course:** BUS-629 International Corporate Finance, Vietnam EMBA, Shidler College of Business
**Date range:** 2026-05-22 – 2026-05-24
**Tool:** Claude (Cowork / claude-sonnet-4-6)

---

## Stage 1 — Performance Ratios Template

**Date:** Pre-session (template provided)
**AI involvement:** None — template artifact supplied by course instructor

### What was done

The BUS-629 course provided a blank Excel performance-ratios template (`performance-ratios-template.xlsx`) with:
- Pre-labeled ratio rows across six categories: Valuation, Performance, Profitability, Efficiency, Leverage, and Liquidity
- YAML-annotated named-range convention (`BAL_*`, `INC_*`, `CASH_*`, `RATIO_*`)
- Color-coding standard (blue = hardcoded inputs, black = formulas, green = cross-sheet links)
- Empty columns for FY2025 (current year) and FY2024 (prior year)

### Output

`performance-ratios-template.xlsx` — used as the structural foundation for Stage 3 workbook population and Stage 4 spec authoring.

### Notes

No LLM prompting in Stage 1. The template established naming conventions that carried through all subsequent stages unchanged.

---

## Stage 2 — Company Selection Memo

**Date:** Pre-session
**AI involvement:** Minimal — drafting assistance

### What was done

Selected FPT Corporation (ticker: FPT, exchange: HoSE) as the subject company. Produced a company selection memo with:
- Rationale: Vietnam's largest diversified technology conglomerate; publicly listed; annual report available in both Vietnamese and English; three distinct business segments (Technology, Telecom, Education) producing multi-line financials suitable for ratio analysis
- Data availability check: FPT Annual Report 2025 confirmed available on FPT Investor Relations and the Ho Chi Minh Stock Exchange disclosure portal
- Instructor approval: obtained prior to Stage 3

### Output

Company selection memo submitted. FPT confirmed as subject company for Stages 3–5.

### Notes

The company memo established the reporting standard (Vietnamese Accounting Standards, VAS), currency (Vietnamese Dong, reported in B VND = billions), and fiscal year (FY2025 vs. FY2024 comparative) that governed all downstream stages.

---

## Stage 3 — Populate Financials Workbook

**Date:** 2026-05-22
**Tool:** Claude (Cowork / claude-sonnet-4-6)
**Stage:** Stage 3 — Data extraction and workbook population

### Inputs provided

- FPT Annual Report 2025 (PDF, uploaded)
- Blank performance-ratios template: `performance-ratios-template.xlsx`

### Prompt used

```
Using the FPT Annual Report 2025, populate the financials workbook.
Extract the Income Statement, Balance Sheet, and Cash Flow Statement
figures for FY2025 and FY2024 and fill them into the template's named
ranges. Use Vietnamese Accounting Standard line items and map them to
the template structure.
```

### Key mapping decisions (VAS → template)

| VAS source | Template named range | Note |
|---|---|---|
| Code 110 + 120 (cash + equivalents) | `BAL_cash_curr / _prior` | Combined short-term cash items |
| Code 131 (trade receivables) | `BAL_receivables_curr / _prior` | Gross trade receivables |
| Code 211–214 (inventory net) | `BAL_inventory_curr / _prior` | Net of provisions |
| Code 211 (PP&E net) | `BAL_ppe_curr / _prior` | Net after accumulated depreciation |
| Code 25+26 (SGA expenses) | `INC_sga` | Selling + general & administrative combined |
| CF Code 02 (depreciation) | `INC_depreciation` | D&A sourced from CF, not IS (VAS norm) |
| PBT − EBIT + interest | `INC_other_income` | Residual; aggregates financial income, disposal gains, associates' profit under VAS |
| Code 411 / par value 10,000 | `shares_outstanding` | = 17,035,071,210,000 ÷ 10,000 = 1,703,507,121 shares |
| CF dividends paid | `CASH_dividends_paid` | Cash paid per CF statement, not declared |

### What the LLM did well

All VAS-to-template mappings were correctly inferred. Financial statement cross-checks passed:
- Balance sheet equation: Assets = Liabilities + Equity ✓ (both years)
- Cash flow reconciliation: Opening + net CF = closing cash ✓

### Errors and fixes

- **PermissionError on output file:** The initial output path `/sessions/.../2026-05-22-chu-fpt-financials.xlsx` was locked from a prior session. Fix: saved as `2026-05-22-chu-fpt-financials-v2.xlsx` instead. All downstream references use the v2 filename.

### Output

`2026-05-22-chu-fpt-financials-v2.xlsx` — fully populated workbook with:
- Income Statement, Balance Sheet, Cash Flow tabs
- Named ranges defined for all 40+ inputs
- Ratios sheet (ratio formulas added at end of Stage 3 / start of Stage 4 session)

---

## Stage 3 (continued) — Fill Ratios Sheet

**Date:** 2026-05-24
**Prompt used:**

```
Fill Data for sheet Ratios with the remaining blanks ratio like Return on
assets (ROA), Return on equity (ROE) in 2026-05-22-chu-fpt-financials-v2
```

### What was done

Added openpyxl formula entries to every blank ratio row in the Ratios sheet (column C). Key formulas:

| Ratio | Cell | Formula written |
|---|---|---|
| ROA | C47 | `=currentYear_after_tax_operating_income/startYear_total_assets` |
| ROE | C49 | `=INC_net/startYear_equity` |
| Asset Turnover | C54 | `=INC_sales/startYear_total_assets` |
| MVA | C43 | `=market_capitalization-currentYear_equity` |
| Du Pont ROA | C75 | `=RATIO_asset_turnover*RATIO_operating_profit_margin` |
| Du Pont ROE | C76 | `=RATIO_leverage*RATIO_asset_turnover*RATIO_operating_profit_margin*RATIO_debt_burden` |
| Du Pont match checks | F75, F76 | `=IF(ABS(C75-C47)<0.0001,"✓ ROA match","✗ MISMATCH")` |

All 89 formulas recalculated via `scripts/recalc.py` with 0 errors.

**Key confirmed values:**

| Ratio | Value |
|---|---|
| MVA | 119,788.643 B VND |
| ROA (ATOI + start assets) | 16.49% |
| ROE (net income + start equity) | 31.44% |
| Current Ratio | 1.40x |
| Du Pont ROE | 31.43% (0.01 pp gap — time-mismatch, within tolerance) |

---

## Stage 4 — Technical Specification (Round 1)

**Date:** 2026-05-24
**Stage:** Stage 4 — LLM-Drafted Technical Specification

### Inputs provided

- Stage 4 brief (URL): `https://raw.githubusercontent.com/adamwstauffer/shidler/main/courses/BUS-629-VEMBA-International-Corporate-Finance/stage4-technical-specification.md`
- Spec template (uploaded): `2026-05-24-chu-fpt-spec-e6d411ba.md`
- Stage 3 populated workbook (uploaded): `2026-05-22-chu-fpt-financials-51ce2048.xlsx`
- Performance ratios template (uploaded): `performance-ratios-template-e596e5ff.xlsx`

### Prompt used

```
Read the Stage 4 brief and spec template at the URLs above. Then, using the
spec template's structure, draft a technical specification for [FPT]
accounting ratios analysis.

Requirements:
- Populate every section (Part A items 1–7, Part B items 8–11)
- Use named-range notation (BAL_*, INC_*, CASH_*, RATIO_*) throughout
- Where data values appear in my uploaded Stage 3 workbook, include them
  numerically in the Data Inputs table
- Keep the YAML frontmatter from the template intact

Before drafting, list the three or four assumptions you'll need from me
(e.g., reporting standard, fiscal year, intended audience for the analysis).
```

### Assumptions confirmed (pre-draft)

| Assumption | Value confirmed |
|------------|----------------|
| Reporting standard | Vietnamese Accounting Standards (VAS) |
| Intended audience | BUS-629 VEMBA course graders |
| Cost of capital | 9% (class working WACC) |
| Tax rate | 21% (Vietnam statutory CIT) |

### Round-1 output

Draft spec produced: `2026-05-24-chu-fpt-spec.md` (Version 1.0)

---

## Stage 4 — HIL Review Pass

**Date:** 2026-05-24
**Stage:** Stage 4 — Human-in-the-Loop iteration

### Gap 1 identified: Dividends source — wrong figure, wrong allocation

Reviewing the round-1 spec against the Stage 3 workbook, I found that the LLM's first draft reported dividends of **3,185 B VND** and addition to retained earnings of **8,047 B VND**. These figures passed the internal check (3,185 + 8,047 = 11,232 = net income ✓) but were incorrect.

**Root cause:** The v1.0 spec did not specify *which source* to use for dividends — it did not state whether to take dividends from a declared/per-share calculation or from the cash flow statement. The LLM pulled a rounded declared-dividend estimate, not the cash actually paid in FY2025. The Cash Flow Statement in the Stage 3 workbook clearly shows dividends paid as **4,573.754 B VND** (line item `CASH_dividends_paid`), which is the correct figure for the income statement's allocation section.

**Why this matters for Stage 5:** A Stage 5 LLM given the v1.0 spec would write that "FPT retained 8,047 B VND of its 11,232 B VND net income," overstating retention by ~1,389 B VND and understating dividend outflow by 44%. This would distort any Stage 5 discussion of FPT's capital return policy and payout ratio.

**What I changed:** I re-prompted with the specific discrepancy — asking which figure to use — confirmed the CF statement as the authoritative source, then revised the spec to (a) update dividends to 4,573.754 B VND, (b) update retained earnings to 6,658.585 B VND, and (c) add a source annotation in the Data Inputs table explicitly stating *"from Cash Flow Statement"* to prevent the same ambiguity at Stage 5.

### Gap 2 identified: Shares outstanding — precision

The v1.0 spec rounded shares to 1,700,000,000. The workbook derives shares as owners' capital (Code 411: 17,035,071,210,000 VND) ÷ par value 10,000 VND = **1,703,507,121** shares. The 3.5 million share gap produces a market-cap understatement of ~336 B VND. I added the derivation method explicitly to the Named-Range Assumptions table so a Stage 5 LLM can verify the figure independently.

### Revised output

Spec updated to Version 2.0: `2026-05-24-chu-fpt-spec.md`

Key changes: dividends 3,185 → 4,573.754 B VND; retained earnings 8,047 → 6,658.585 B VND; shares 1,700,000,000 → 1,703,507,121; market cap 163,200 → 163,536.684 B VND; MVA 119,452 → 119,788.643 B VND; three CF financing line items corrected; source annotation added for dividends.

---

## Stage 5 — LLM-Executed Ratio Analysis

**Date:** 2026-05-24
**Stage:** Stage 5 — LLM Analysis Execution

### Inputs provided

- Spec: `2026-05-24-chu-fpt-spec-295e0ffb.md` (Version 2.0, uploaded)
- No other files, workbook, or annual report provided — spec was the sole input, per the Stage 5 design intent

### Prompt used

```
Use it as input for Stage 5 — produce the full ratio analysis document
from this spec alone.
```

### Output

`deliverables/2026-05-24-chu-fpt-analysis.md` — full ratio analysis, 10 sections, ~2,000 words

### What the LLM did well

All 25+ ratios reproduced correctly against spec formulas. All ten output sections present in correct order (Executive Summary → Performance → Profitability → Efficiency → Leverage → Liquidity → Du Pont → Recommendations → Ratio Summary Table). All six validation rules addressed explicitly. Du Pont decomposition arithmetically correct (2.015 × 0.974 × 16.93% × 0.9461 = 31.43%), time-mismatch disclosed. Five strategic recommendations produced, spanning four ratio categories, each with specific ratio values cited.

### What I noticed reviewing the raw output

The LLM followed the spec's formulas precisely — which also meant it reproduced the spec's convention choices without flagging them. ROA appeared as 16.49% (spec: ATOI + start-of-year assets), DSO as 59.3 days (spec: prior-year receivables), and Debt-to-Equity as 0.044x (spec: long-term debt only). None of these figures were accompanied by a disclosure that they differ from textbook convention. A reader benchmarking FPT's 16.49% ROA against Bloomberg peer data would be making a 246 bp apples-to-oranges comparison. These are spec gaps, not LLM errors — but the LLM had enough data available in the spec (it listed both ROA start-assets and ROA average-assets) to have surfaced the parallel convention question for DSO and D/E. It did not.

Recommendation 5 (receivables securitisation) was also technically outside BUS-629 course scope and Vietnam's regulatory environment for ABS — the spec placed no constraint on recommendation sophistication, so the LLM reached for a sophisticated treasury technique that is unlikely to be actionable within 12–24 months.

---

## Stage 5 — Verification Table

**Date:** 2026-05-24
**Stage:** Stage 5 — Human verification of LLM ratio values

### Prompt used

```
Create analysis/validation/YYYY-MM-DD-{lastname}-{company-slug}-stage5-verification.md
with five rows. Pick 5 ratios as below (ROA, Current Ratio, Days Sales Outstanding,
Inventory Turnover, Debt-to-Equity). The table will be structured as below:
Ratio | Formula (named-range notation) | Manual value (show arithmetic) | LLM's value | Match? | One-line note.

In which:
ROA = INC_net / ((BAL_assets_total_2025 + BAL_assets_total_2024) / 2)
Current Ratio = BAL_current_assets_2025 / BAL_current_liabilities_2025
Days Sales Outstanding = (BAL_receivables_2025 / INC_revenue_2025) × 365
Inventory Turnover = INC_cogs_2025 / ((BAL_inventory_2025 + BAL_inventory_2024) / 2)
Debt-to-Equity = BAL_debt_total_2025 / BAL_equity_total_2025
```

### Inputs provided

Spec component values carried forward from prior prompt — no re-upload needed. User specified all five formulas explicitly using standard textbook conventions.

### Output

`analysis/validation/2026-05-24-chu-fpt-stage5-verification.md`

### Gap confirmed — 4 of 5 ratios showed discrepancies

| Ratio | LLM (spec convention) | Manual (textbook) | Gap |
|---|---|---|---|
| ROA | 16.49% | 14.03% | 246 bp — LLM used ATOI + start-of-year assets; textbook uses net income + average assets |
| Current Ratio | 1.40x | 1.40x | ✓ identical |
| DSO | 59.3 days | 75.0 days | 15.7 days — LLM used prior-year receivables; textbook uses year-end |
| Inventory Turnover | 23.82x | 21.84x | 1.98x — LLM used start-of-year inventory; textbook uses two-year average |
| Debt-to-Equity | 0.044x | 1.015x | 23× — LLM used LT debt only; textbook uses total liabilities |

### What I changed as a result

These four discrepancies confirmed the spec retrospective finding (Gap 1, 2, 3): the spec never disclosed its convention deviations, so the LLM had no instruction to flag them. This table was the evidence that justified the "3" effectiveness rating in the retrospective.

---

## Stage 5 — Spec Retrospective

**Date:** 2026-05-24
**Stage:** Stage 5 — Structured self-evaluation of Stage 4 spec

### Inputs provided

- Stage 5 LLM output: `2026-05-24-chu-fpt-analysis.md`
- Verification file: `analysis/validation/2026-05-24-chu-fpt-stage5-verification.md`
- Retrospective template: `2026-05-24-spec-retrospective.md` (uploaded)

### Prompt used

```
Generate 2026-05-24-spec-retrospective.md as the requirement below:
1. Section-by-section verdict on your Stage 4 spec (Clear / Vague / Missing)
   with the symptom in your Stage 5 output that justifies each verdict.
2. Top three gaps with evidence — each gap tied to where it surfaced in the
   LLM output, what your spec caused, and the exact spec language you would add.
3. Three revisions you would make if you re-ran, each tied to a numbered gap.
4. Effectiveness rating (1–5) with anchored justification.
5. Forward link — one sentence on what changes in how you approach the next spec.
6. Retrospective process feedback (≤150 words).
```

### Output

`deliverables/2026-05-24-chu-fpt-spec-retrospective.md`

### Summary of findings

- 7 of 11 spec sections rated Clear; 3 Vague (A.3 Data Inputs, A.4 Named Ranges, A.6 Ratio Definitions); 1 Vague on B.10 Recommendation scope.
- All three Vague verdicts shared the same root: Part A.6 formulas deviated from textbook convention without disclosing the alternative — a pattern invisible in narrative review but surfaced immediately in the section-by-section table.
- **Effectiveness rating: 3 / 5** — workable, correct per spec, but convention gaps materially affected benchmarkability of four ratios.

### What the retrospective template surfaced that free-form reflection would not

The section-by-section structure forced the finding that gaps were clustered in A.6, not scattered across all sections. In a free-form write-up the entry would have said "the spec had some convention issues" without identifying the specific structural cause.

---

## Stage 5 — Final Analysis (Human Review and Rewrite)

**Date:** 2026-05-24
**Stage:** Stage 5 — Human-reviewed final deliverable

### Inputs provided

- LLM raw output: `2026-05-24-chu-fpt-final-analysis.md` (uploaded)
- All prior session context (spec, verification table, retrospective)

### Prompt used

```
Update the final analysis with more my style and more realistic and satisfied below.
Required sections in the evaluated final analysis:
1. Company & Data Summary
2. Ratio Results & Interpretation (all six categories with corrections)
3. Du Pont Analysis with commentary on LLM interpretation
4. Strategic Recommendations (3–5, with LLM assessment)
5. LLM Evaluation & Annotations
6. Executive Justification — final investment thesis in your own voice
```

### Output

`deliverables/2026-05-24-chu-fpt-final-analysis.md` (human-reviewed version)

### What I changed and why

1. **Added VAS accounting standard notes** (Section 1) — the "other income" residual of 5,779.027 B VND is a model artefact derived as PBT − EBIT + interest, not a reported VAS line item. The LLM reported it without flagging this. A grader reading the analysis needs to know this figure aggregates financial income, disposal gains, and share of associates' profit under VAS.

2. **Added dual-convention ratio table** (Section 2b) — presented ROA at 16.49% (spec), 14.83% (ATOI avg), and 14.03% (net income avg) in a single table. The LLM reported only the spec figure. For benchmarking against peers, 14.03% is the correct number.

3. **Corrected DSO headline** (Section 2c) — changed the headline DSO from 59.3 days to 75.0 days (standard convention) and explained why 75 days is the number management discussions should use. Added Vietnam IT government receivables context (budget release cycles cause structural 60–90 day payment delays).

4. **Added total D/E** (Section 2d) — added total interest-bearing D/E of 0.48x alongside the spec's LT D/E of 0.044x. Reframed the short-term debt risk in the context of Vietnamese state-owned bank credit market norms.

5. **Identified ROE / leverage tension in Du Pont** (Section 3) — the LLM presented "refinance short-term debt" and "sustain ROE" as independent goals. They are not: refinancing reduces leverage, which mechanically reduces Du Pont ROE by ~1.5 pp. The final analysis states this trade-off explicitly.

6. **Replaced Recommendations 4–5** (Section 4) — Recommendation 5 (receivables securitisation) removed; replaced with a formal capital allocation policy for the 40,000 B VND cash position. Securitisation removed because: (a) outside BUS-629 scope, (b) Vietnam's ABS regulatory framework not yet mature, (c) the spec retrospective flagged this as a B.10 spec gap.

7. **Added Executive Justification in first person** (Section 6) — FPT Software's Japan exposure as the structural moat behind the 16.93% margin; government IT receivables as the structural cause of 75-day DSO; the 40,000 B VND cash as likely FPT Telecom operating cash parked in affiliated bank deposits; price target of 110,000–120,000 VND conditioned on FY2026 Q1 DSO data.
