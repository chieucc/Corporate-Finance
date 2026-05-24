# Prompt Log — BUS-629 Project

**Student:** Chieu Chu · ChieuCC@fpt.com
**Company:** FPT Corporation (FPT · HoSE)
**Course:** BUS-629 International Corporate Finance, Vietnam EMBA, Shidler College of Business

---

## Entry 1 — Stage 4: Technical Specification (Round 1)

**Date:** 2026-05-24
**Tool:** Claude (Cowork / claude-sonnet-4-6)
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

## Entry 2 — Stage 4: HIL Review Pass

**Date:** 2026-05-24
**Stage:** Stage 4 — Human-in-the-Loop iteration

### Gap identified: Dividends source — wrong figure, wrong allocation

Reviewing the round-1 spec against the Stage 3 workbook, I found that the LLM's first draft reported dividends of **3,185 B VND** and addition to retained earnings of **8,047 B VND**. These figures passed the internal check (3,185 + 8,047 = 11,232 = net income ✓) but were incorrect.

**Root cause:** The v1.0 spec did not specify *which source* to use for dividends — it did not state whether to take dividends from a declared/per-share calculation or from the cash flow statement. The LLM pulled a rounded declared-dividend estimate, not the cash actually paid in FY2025. The Cash Flow Statement in the Stage 3 workbook clearly shows dividends paid as **4,573.754 B VND** (line item `CASH_dividends_paid`), which is the correct figure for the income statement's allocation section.

**Why this matters for Stage 5:** A Stage 5 LLM given the v1.0 spec would write that "FPT retained 8,047 B VND of its 11,232 B VND net income," overstating retention by ~1,389 B VND and understating dividend outflow by 44%. This would distort any Stage 5 discussion of FPT's capital return policy and payout ratio.

**What I changed:** I re-prompted with the specific discrepancy — asking which figure to use — confirmed the CF statement as the authoritative source, then revised the spec to (a) update dividends to 4,573.754 B VND, (b) update retained earnings to 6,658.585 B VND, and (c) add a source annotation in the Data Inputs table explicitly stating *"from Cash Flow Statement"* to prevent the same ambiguity at Stage 5.

### Secondary gap identified: Shares outstanding — precision

The v1.0 spec rounded shares to 1,700,000,000. The workbook derives shares as owners' capital (Code 411: 17,035,071,210,000 VND) ÷ par value 10,000 VND = **1,703,507,121** shares. The 3.5 million share gap produces a market-cap understatement of ~336 B VND. I added the derivation method explicitly to the Named-Range Assumptions table so a Stage 5 LLM can verify the figure independently.

### Revised output

Spec updated to Version 2.0: `2026-05-24-chu-fpt-spec.md`

Key changes: dividends 3,185 → 4,573.754 B VND; retained earnings 8,047 → 6,658.585 B VND; shares 1,700,000,000 → 1,703,507,121; market cap 163,200 → 163,536.684 B VND; MVA 119,452 → 119,788.643 B VND; three CF financing line items corrected; source annotation added for dividends.
