---
template: spec
purpose: "Technical specification for model-driven projects — defines scope, inputs, formulas, validation, and analysis requirements precisely enough that any competent executor (human or LLM) can produce correct output"
audience: student
fields_required: [title, author, date, version, company, scope, model_architecture, data_inputs, derived_inputs, formulas, validation, analysis_requirements, output_format, references]
naming_convention: "YYYY-MM-DD-{slug}.md"
courses: [BUS-314, BUS-629, FIN-321]
notes: "Originally authored for BUS-629 ratios analysis. Section 5 (Ratio Definitions) can be replaced with project-specific formulas (e.g., FX hedging payoffs, valuation models) for non-ratios projects."
---

# FPT Corporation — Accounting & Performance Ratios Analysis Specification

**Author:** Chieu Chu
**Date:** 2026-05-24
**Version:** 2.0
**Company:** FPT Corporation · FPT · HoSE (Ho Chi Minh Stock Exchange)

---

## 1. Scope & Objective

This specification defines the model architecture, data inputs, ratio formulas, and written-analysis requirements for a comprehensive accounting and performance ratios analysis of **FPT Corporation (FPT)**, Vietnam's largest technology, telecommunications, and education conglomerate, for **fiscal year 2025** (year ended 31 December 2025) with **FY2024 as the prior-year comparative period**.

**Reporting standard:** Vietnamese Accounting Standards (VAS).
**Reporting currency:** Vietnamese Dong (VND). All financial statement figures are denominated in **billions VND (B VND)** unless otherwise noted.
**Analytical objective:** Assess FPT's financial health across five dimensions — Performance, Profitability, Efficiency, Leverage, and Liquidity — and synthesise findings into evidence-backed strategic recommendations. The Du Pont decomposition is required to identify the primary drivers of FPT's return on equity and to evaluate the sustainability of that return.
**Intended audience:** BUS-629 International Corporate Finance course graders (professor and TAs), Vietnam EMBA programme, University of Hawaiʻi at Mānoa — Shidler College of Business.

---

## Part A — Model Specification

### 2. Model Architecture

The workbook (`2026-05-22-chu-fpt-financials.xlsx`) has six tabs in the following order:

| Tab | Contents | Role |
|-----|----------|------|
| Cover | Instructions, color key, named-range convention | Reference only |
| Balance Sheet | FY2025 and FY2024 balance-sheet line items | Data input |
| Income Statement | FY2025 income statement with % of sales column | Data input |
| Cash Flow Statement | FY2025 operating / investing / financing cash flows | Data input |
| Ratios | Analyst assumptions, derived inputs, all ratio outputs | Calculation + output |
| Notes | Company metadata, AI usage log, self-checks | Documentation |

**Color coding convention:**

| Style | Meaning |
|-------|---------|
| Yellow background | DATA INPUTS — numbers pulled from FPT annual report. Do not compute; overwrite from source. |
| Light-blue background, blue text | ANALYST ASSUMPTIONS — share price, shares outstanding, WACC, tax rate. |
| Green text | FORMULAS — cross-sheet references and derived calculations. Do not overwrite. |
| Gray background | RATIO OUTPUTS — computed values in the Ratios tab. Do not overwrite. |

**Named-range convention:**

| Prefix | Scope |
|--------|-------|
| `BAL_[item]_curr` | Current-year (FY2025) balance-sheet values |
| `BAL_[item]_prior` | Prior-year (FY2024) balance-sheet values |
| `INC_[item]` | Income-statement items (single year) |
| `CASH_[item]` | Cash-flow items (single year) |
| `startYear_[item]` | Alias for prior-year balance (used in ratio formulas) |
| `currentYear_[item]` | Current-year derived quantities |
| `avg_[item]` | Two-year averages |
| `RATIO_[item]` | Named ratio outputs referenced in Du Pont formulas |
| `share_price`, `shares_outstanding`, `cost_capital`, `tax_rate` | Analyst assumptions (no prefix) |

Data flows strictly left to right and top to bottom: raw inputs on the three financial-statement tabs are referenced via named ranges on the Ratios tab; no manual re-entry of any figure on more than one tab.

---

### 3. Data Inputs

All values are sourced from the **FPT Consolidated Annual Report 2025 (Báo cáo Thường niên 2025)**. Figures in billions VND (full-precision values from Stage 3 workbook; rounded for display).

#### Balance Sheet

| Named Range | Description | FY2025 (curr) | FY2024 (prior) | Unit |
|-------------|-------------|--------------|----------------|------|
| `BAL_cash_marketable_securities_curr` / `_prior` | Cash and marketable securities (Code 110 + Code 120) | 40,153.092 | 31,100.654 | B VND |
| `BAL_receivables_curr` / `_prior` | Receivables (Code 130) | 14,402.017 | 11,381.524 | B VND |
| `BAL_inventories_curr` / `_prior` | Inventories (Code 140) | 2,193.770 | 1,856.757 | B VND |
| `BAL_other_current_assets_curr` / `_prior` | Other current assets (Code 150) | 1,388.559 | 1,197.008 | B VND |
| `BAL_assets_current_curr` / `_prior` | **Total current assets** | `=SUM(C7:C10)` = 58,137.438 | `=SUM(D7:D10)` = 45,535.943 | B VND |
| `BAL_ppe_gross_curr` / `_prior` | Property, plant & equipment — gross (Code 222) | 29,122.042 | 24,457.734 | B VND |
| `BAL_accumulated_depreciation_curr` / `_prior` | Less: accumulated depreciation (Code 223) | 13,762.874 | 11,683.166 | B VND |
| `BAL_fixed_assets_net_curr` / `_prior` | **Net tangible fixed assets** | `=C14−C15` = 15,359.168 | `=D14−D15` = 12,774.568 | B VND |
| `BAL_intangibles_curr` / `_prior` | Intangible assets + goodwill (Code 227 net + Code 269) | 2,943.826 | 3,136.979 | B VND |
| `BAL_other_assets_curr` / `_prior` | Other assets (residual to balance) | 11,701.558 | 10,552.506 | B VND |
| `BAL_assets_total_curr` / `_prior` | **Total assets** | `=C11+C16+C19+C20` = 88,141.990 | `=D11+D16+D19+D20` = 71,999.996 | B VND |
| `BAL_debt_short_term_curr` / `_prior` | Short-term debt (Code 320) | 19,169.697 | 14,445.809 | B VND |
| `BAL_accounts_payable_curr` / `_prior` | Accounts payable (Code 311) | 3,836.801 | 4,423.633 | B VND |
| `BAL_other_current_liabilities_curr` / `_prior` | Other current liabilities (residual) | 18,518.430 | 15,966.394 | B VND |
| `BAL_liabilities_current_curr` / `_prior` | **Total current liabilities** | `=SUM(G7:G9)` = 41,524.928 | `=SUM(H7:H9)` = 34,835.836 | B VND |
| `BAL_debt_long_term_curr` / `_prior` | Long-term debt (Code 338) | 1,903.790 | 501.116 | B VND |
| `BAL_other_long_term_liabilities_curr` / `_prior` | Other long-term liabilities | 965.232 | 934.724 | B VND |
| `BAL_liabilities_total_curr` / `_prior` | **Total liabilities** | `=G10+G12+G13` = 44,393.950 | `=H10+H12+H13` = 36,271.676 | B VND |
| `BAL_common_stock_curr` / `_prior` | Common stock and paid-in capital | 29,446.001 | 24,699.460 | B VND |
| `BAL_retained_earnings_curr` / `_prior` | Retained earnings (Code 421) | 14,302.040 | 11,028.320 | B VND |
| `BAL_equity_shareholders_curr` / `_prior` | **Total shareholders' equity** | `=G18+G19` = 43,748.041 | `=H18+H19` = 35,727.780 | B VND |

#### Income Statement

| Named Range | Description | FY2025 | Unit |
|-------------|-------------|--------|------|
| `INC_sales` | Net sales (Code 10) | 70,112.825 | B VND |
| `INC_cost_goods_sold` | Cost of goods sold (Code 11) | 44,224.296 | B VND |
| `INC_sga` | Selling + G&A expenses (Code 25 + Code 26) | 14,899.986 | B VND |
| `INC_depreciation` | Depreciation (CF Code 02 — D&A add-back) | 2,914.178 | B VND |
| `INC_ebit` | **EBIT** | `=C6−C7−C8−C9` = 8,074.365 | B VND |
| `INC_other_income` | Plus: other income (derived: PBT − EBIT + Interest) | 5,779.027 | B VND |
| `INC_interest_expense` | Less: interest expense (Code 23) | 809.760 | B VND |
| `INC_taxable_income` | **Taxable income** | `=C10+C11−C12` = 13,043.632 | B VND |
| `INC_taxes` | Less: taxes (Code 51 + Code 52) | 1,811.293 | B VND |
| `INC_net` | **Net income** | `=C13−C14` = 11,232.339 | B VND |
| `INC_dividends` | Dividends paid (from Cash Flow Statement) | 4,573.754 | B VND |
| `INC_addition_retained_earnings` | Addition to retained earnings | `=C15−C18` = 6,658.585 | B VND |

#### Cash Flow Statement

| Named Range | Description | FY2025 | Unit |
|-------------|-------------|--------|------|
| — | Net income (linked from Income Statement) | 11,232.339 | B VND |
| — | Plus depreciation (linked from Income Statement) | 2,914.178 | B VND |
| — | Decrease (increase) in accounts receivable | −2,874.822 | B VND |
| — | Decrease (increase) in inventories | −335.072 | B VND |
| — | Decrease (increase) in other current assets | −595.604 | B VND |
| — | Increase (decrease) in accounts payable | −586.832 | B VND |
| — | Increase (decrease) in other current liabilities | 381.856 | B VND |
| `CASH_operating` | **Cash provided by operations** | `=C7+C8+C15` = 10,136.043 | B VND |
| — | Capital expenditures (Code 221 + 222 net change) | −5,097.919 | B VND |
| — | Sales (acquisitions) of long-term assets | 7.314 | B VND |
| — | Other investing activities | −6,534.138 | B VND |
| `CASH_investments` | **Cash used for investments** | `=SUM(C19:C21)` = −11,624.743 | B VND |
| — | Increase (decrease) in short-term debt | 4,723.459 | B VND |
| — | Increase (decrease) in long-term debt | 1,402.674 | B VND |
| — | Dividends paid | −4,573.754 | B VND |
| — | Issues (repurchases) of stock | 1,196.235 | B VND |
| — | Other financing | 52.708 | B VND |
| `CASH_financing` | **Cash provided by financing** | `=SUM(C25:C29)` = 2,801.322 | B VND |

#### Analyst Assumptions

| Named Range | Value | Source / Notes |
|-------------|-------|----------------|
| `share_price` | 9.6 × 10⁻⁵ B VND (= 96,000 VND) | FY2025 year-end closing price, HoSE |
| `shares_outstanding` | 1,703,507,121 shares | Owners' capital (Code 411: 17,035,071,210,000 VND) ÷ par value 10,000 VND |
| `cost_capital` | 0.09 (9%) | BUS-629 class working WACC |
| `tax_rate` | 0.21 (21%) | Vietnam statutory corporate income tax rate |

---

### 4. Derived Inputs

All derived inputs are computed on the **Ratios tab** via named-range formulas. The executor must not overwrite these cells.

| Named Range | Formula (named-range notation) | Value | Unit |
|-------------|-------------------------------|-------|------|
| `market_capitalization` | `share_price × shares_outstanding` | 163,536.684 | B VND |
| `startYear_equity` | `BAL_equity_shareholders_prior` | 35,727.780 | B VND |
| `startYear_inventory` | `BAL_inventories_prior` | 1,856.757 | B VND |
| `startYear_receivables` | `BAL_receivables_prior` | 11,381.524 | B VND |
| `startYear_total_assets` | `BAL_assets_total_prior` | 71,999.996 | B VND |
| `startYear_total_capitalization` | `BAL_debt_long_term_prior + BAL_equity_shareholders_prior` | 36,228.896 | B VND |
| `currentYear_after_tax_operating_income` | `INC_net + (1 − tax_rate) × INC_interest_expense` | 11,872.049 | B VND |
| `currentYear_daily_sales_average` | `INC_sales / 365` | 192.090 | B VND/day |
| `currentYear_equity` | `BAL_equity_shareholders_curr` | 43,748.041 | B VND |
| `currentYear_cash_marketable_securities` | `BAL_cash_marketable_securities_curr` | 40,153.092 | B VND |
| `currentYear_assets_current` | `BAL_assets_current_curr` | 58,137.438 | B VND |
| `currentYear_liabilities_current` | `BAL_liabilities_current_curr` | 41,524.928 | B VND |
| `currentYear_cost_goods_sold_daily` | `INC_cost_goods_sold / 365` | 121.162 | B VND/day |
| `currentYear_debt_long_term` | `BAL_debt_long_term_curr` | 1,903.790 | B VND |
| `currentYear_working_capital_net` | `BAL_assets_current_curr − BAL_liabilities_current_curr` | 16,612.510 | B VND |
| `currentYear_assets_total` | `BAL_assets_total_curr` | 88,141.990 | B VND |
| `currentYear_total_capitalization` | `currentYear_debt_long_term + currentYear_equity` | 45,651.831 | B VND |
| `currentYear_liabilities_total` | `BAL_liabilities_total_curr` | 44,393.950 | B VND |
| `avg_equity` | `AVERAGE(startYear_equity, currentYear_equity)` | 39,737.911 | B VND |
| `avg_total_assets` | `AVERAGE(startYear_total_assets, currentYear_assets_total)` | 80,070.993 | B VND |
| `avg_total_capitalization` | `AVERAGE(startYear_total_capitalization, currentYear_total_capitalization)` | 40,940.364 | B VND |

---

### 5. Ratio Definitions & Formulas

**Performance**

| Ratio | Formula (named-range notation) | Computed Value | Unit |
|-------|-------------------------------|----------------|------|
| Market Value Added (MVA) | `market_capitalization − currentYear_equity` | 119,788.643 | B VND |
| Market-to-Book | `market_capitalization / currentYear_equity` | 3.74 | x |
| Economic Value Added (EVA) | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | 8,611.549 | B VND |

**Profitability**

| Ratio | Formula | Computed Value | Unit |
|-------|---------|----------------|------|
| ROA (start assets) | `currentYear_after_tax_operating_income / startYear_total_assets` | 16.49% | % |
| ROA (average assets) | `currentYear_after_tax_operating_income / avg_total_assets` | 14.83% | % |
| ROC (start capital) | `currentYear_after_tax_operating_income / startYear_total_capitalization` | 32.77% | % |
| ROC (average capital) | `currentYear_after_tax_operating_income / avg_total_capitalization` | 29.00% | % |
| ROE (start equity) | `INC_net / startYear_equity` | 31.44% | % |
| ROE (average equity) | `INC_net / avg_equity` | 28.27% | % |
| Net Profit Margin | `INC_net / INC_sales` | 16.02% | % |
| Operating Profit Margin (`RATIO_operating_profit_margin`) | `currentYear_after_tax_operating_income / INC_sales` | 16.93% | % |

**Efficiency**

| Ratio | Formula | Computed Value | Unit |
|-------|---------|----------------|------|
| Asset Turnover (`RATIO_asset_turnover`) | `INC_sales / startYear_total_assets` | 0.974 | x |
| Receivables Turnover | `INC_sales / startYear_receivables` | 6.160 | x |
| Average Collection Period | `startYear_receivables / currentYear_daily_sales_average` | 59.3 | days |
| Inventory Turnover | `INC_cost_goods_sold / startYear_inventory` | 23.82 | x |
| Days in Inventory | `startYear_inventory / currentYear_cost_goods_sold_daily` | 15.3 | days |

**Leverage**

| Ratio | Formula | Computed Value | Unit |
|-------|---------|----------------|------|
| Long-term Debt Ratio | `currentYear_debt_long_term / (currentYear_debt_long_term + currentYear_equity)` | 4.17% | % |
| Long-term Debt-to-Equity | `currentYear_debt_long_term / currentYear_equity` | 0.044 | x |
| Total Debt Ratio | `currentYear_liabilities_total / currentYear_assets_total` | 50.37% | % |
| Times Interest Earned | `INC_ebit / INC_interest_expense` | 9.97 | x |
| Cash Coverage Ratio | `(INC_ebit + INC_depreciation) / INC_interest_expense` | 13.57 | x |
| Debt Burden (`RATIO_debt_burden`) | `INC_net / currentYear_after_tax_operating_income` | 0.9461 | x |
| Leverage Ratio (`RATIO_leverage`) | `currentYear_assets_total / currentYear_equity` | 2.015 | x |

**Liquidity**

| Ratio | Formula | Computed Value | Unit |
|-------|---------|----------------|------|
| NWC-to-Assets | `currentYear_working_capital_net / currentYear_assets_total` | 18.85% | % |
| Current Ratio | `currentYear_assets_current / currentYear_liabilities_current` | 1.40 | x |
| Quick Ratio | `(currentYear_cash_marketable_securities + BAL_receivables_curr) / currentYear_liabilities_current` | 1.31 | x |
| Cash Ratio | `currentYear_cash_marketable_securities / currentYear_liabilities_current` | 0.967 | x |

**Du Pont**

| Ratio | Formula | Computed Value | Unit |
|-------|---------|----------------|------|
| ROA (Du Pont) | `RATIO_asset_turnover × RATIO_operating_profit_margin` | 16.49% | % |
| ROE (Du Pont) | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | 31.43% | % |

---

### 6. Validation Rules

The executor must verify the following internal consistency checks before submitting any output:

1. **Balance sheet balance (FY2025):** `BAL_assets_total_curr = BAL_liabilities_total_curr + BAL_equity_shareholders_curr`. Expected: 88,141.990 = 44,393.950 + 43,748.041. ✓

2. **Balance sheet balance (FY2024):** `BAL_assets_total_prior = BAL_liabilities_total_prior + BAL_equity_shareholders_prior`. Expected: 71,999.996 = 36,271.676 + 35,727.780. Difference < 1 B VND due to rounding of residual "other assets" line. ✓

3. **Du Pont ROA vs. direct ROA:** `RATIO_asset_turnover × RATIO_operating_profit_margin` must equal `currentYear_after_tax_operating_income / startYear_total_assets` to within 0.01 percentage points. Both = 16.49%. The inline check in `Ratios!F75` must display ✓.

4. **Du Pont ROE time-mismatch (expected and acceptable):** `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` = 31.43% vs. direct ROE (start equity) = 31.44%. The 0.01 pp gap is a structural feature: `RATIO_leverage` uses current-year total assets while `RATIO_asset_turnover` uses prior-year assets. This does not constitute an error — the executor must note the time-mismatch in the written analysis. The inline check in `Ratios!F76` must display ✓ (within 0.01 tolerance).

5. **Net income allocation:** `INC_dividends + INC_addition_retained_earnings = INC_net`. Expected: 4,573.754 + 6,658.585 = 11,232.339. ✓

6. **EVA sign check:** Verify `currentYear_after_tax_operating_income > cost_capital × startYear_total_capitalization` → 11,872.049 > 3,260.601. Positive EVA confirms FPT earned above its cost of capital. ✓

---

## Part B — Analysis Specification

### 7. Analysis Requirements

The written analysis must address each ratio category in sequence, following the order in Section 5. For each category, the executor must: (a) state the computed value(s), (b) interpret what the ratio means for FPT, and (c) connect the findings to at least one other category where relevant.

**Performance** — Interpret MVA, Market-to-Book, and EVA together. MVA of 119,788.643 B VND and MTB of 3.74x indicate strong market confidence beyond book value. A positive EVA of 8,611.549 B VND confirms genuine economic value creation above the 9% cost of capital hurdle. Connect to Profitability (high ROC sustains positive EVA) and Leverage (low long-term debt reduces capital-charge denominator).

**Profitability** — Report ROA, ROC, and ROE using both start-of-year and average-asset bases. Benchmark: a tech/telecom conglomerate in Southeast Asia typically targets ROE of 15–25%; FPT's 31.44% ROE (start equity) substantially exceeds this. Examine the gap between net profit margin (16.02%) and operating profit margin (16.93%); the narrow spread indicates low interest burden. Connect to Efficiency (margin × turnover → ROA) and Du Pont.

**Efficiency** — Evaluate asset turnover (0.974x) against the technology-services norm of 0.8–1.2x. Note that receivables collection (59.3 days) is the primary efficiency drag; flag the YoY receivables growth (14,402 vs. 11,382 B VND, +27%) against revenue growth (+17% YoY estimated). Inventory turnover (23.82x / 15.3 days) is consistent with FPT's service-heavy mix. Connect to Leverage (high current-liability base supports the short collection cycle) and Liquidity.

**Leverage** — Distinguish short-term from long-term debt. Long-term debt ratio of 4.17% signals virtually no long-term financial leverage; however, total debt ratio of 50.37% reflects significant operational payables and current debt. Times interest earned of 9.97x and cash coverage of 13.57x confirm comfortable debt-service capacity. Note the sharp increase in short-term debt (19,170 vs. 14,446 B VND prior year, +33%). Connect to Liquidity (current ratio of 1.40x is adequate but cushion is moderate given the large current-liability base) and Performance (low interest burden improves EVA).

**Liquidity** — Current ratio of 1.40x exceeds the minimum acceptable threshold of 1.0x but is below 2.0x, typical for technology companies. Quick ratio of 1.31x and cash ratio of 0.967x indicate FPT can meet near-term obligations almost entirely from cash and receivables. Connect to Efficiency (collection period improvement would strengthen the quick ratio).

---

### 8. Du Pont Decomposition

The Du Pont system decomposes ROE into four components:

```
ROE = Leverage × Asset Turnover × Operating Profit Margin × Debt Burden
    =  2.015   ×     0.974      ×        16.93%           ×   0.9461
    = 31.43%
```

**Primary driver analysis:** Operating Profit Margin (16.93%) is the single largest contributor to FPT's ROE. FPT's diversified business mix — technology services, telecoms, and education — generates above-average margins relative to pure-play telecoms (typical EBIT margin 10–15%). Leverage contributes moderately (2.015x), consistent with the 50.37% total debt ratio.

**Debt Burden interpretation:** A Debt Burden of 0.9461 (< 1.0) indicates that net income is slightly below after-tax operating income, reflecting modest non-operating costs net of taxes. A ratio close to 1.0 signals minimal interest and tax distortion beyond the statutory rate — structurally healthy.

**Sustainability assessment:** The combination of FPT's margin strength and moderate leverage is sustainable in the near term. However, the 33% YoY increase in short-term debt (19,170 vs. 14,446 B VND) warrants monitoring: if short-term debt continues to outpace operating income growth, the Debt Burden component will compress ROE.

**Time-mismatch note (required for submission):** The Du Pont leverage ratio (`RATIO_leverage = currentYear_assets_total / currentYear_equity`) uses end-of-period balances, while asset turnover (`RATIO_asset_turnover = INC_sales / startYear_total_assets`) uses prior-period assets. This mismatch is a structural feature of the template design: because FY2025 opening assets equal FY2024 closing assets, asset turnover is correctly measured against the asset base in place at the beginning of the period. The model's Du Pont ROE (31.43%) and direct ROE (start equity, 31.44%) differ by 0.01 pp, within the template's stated 0.01 tolerance; any larger gap in future periods must be explained rather than corrected.

---

### 9. Strategic Recommendations

The analysis must produce **three to five** strategic recommendations. Each recommendation must: (a) name the specific ratio or finding that motivates it, (b) describe the recommended action concretely, and (c) explain the expected financial impact on at least one ratio.

**Minimum evidence standard:** Every recommendation must cite at least one computed ratio value and one supporting data point from the financial statements. Recommendations must be actionable within a 12–24 month horizon and appropriate for a listed company of FPT's size and sector.

**Required scope:** Recommendations must span at least three different ratio categories (e.g., efficiency + leverage + liquidity) to demonstrate cross-category analytical synthesis.

---

### 10. Output Format

The deliverable is a **single Markdown document** (`.md`) with the following structure and length targets:

| Section | Content | Target length |
|---------|---------|---------------|
| Header | Company, period, author, date, course | 5–8 lines |
| Executive Summary | 3–4 sentences: key finding per category + overall verdict | ~150 words |
| Performance | MVA, MTB, EVA with interpretation | ~200 words |
| Profitability | ROA, ROC, ROE (both bases) with interpretation | ~250 words |
| Efficiency | Asset turnover, receivables, inventory | ~200 words |
| Leverage | Short vs. long-term debt, TIE, coverage | ~200 words |
| Liquidity | Current, quick, cash ratios | ~150 words |
| Du Pont Decomposition | Formula, driver identification, sustainability, time-mismatch note | ~300 words |
| Strategic Recommendations | 3–5 numbered recommendations, each ~100 words | ~400 words |
| Ratio Summary Table | All computed ratios in one table | 1 table |

**Tone:** Professional, analytical, written in third person. Avoid hedging phrases ("it seems," "perhaps"). State findings as conclusions supported by evidence.

**Ratio presentation:** State each ratio as `[value] [unit]` (e.g., "Current Ratio: 1.40x") before interpreting it. Do not present ratios in isolation from the text.

---

## References

- FPT Corporation. *Báo cáo Thường niên 2025 (Consolidated Annual Report FY2025)*. Ho Chi Minh City: FPT Corporation, 2026. [Primary data source for all financial statement inputs; Balance Sheet pp. 165–168, Income Statement pp. 169–170, Cash Flow pp. 171–172.]
- University of Hawaiʻi at Mānoa — Shidler College of Business. *BUS-629 International Corporate Finance — Course Materials and Working WACC*, Vietnam EMBA Programme, 2026. [Source for 9% cost of capital assumption.]
- Stauffer, A. *BUS-629 Stage 4: LLM-Drafted Technical Specification*. Shidler College of Business, University of Hawaiʻi at Mānoa, 2026. `https://raw.githubusercontent.com/adamwstauffer/shidler/main/courses/BUS-629-VEMBA-International-Corporate-Finance/stage4-technical-specification.md`
- Excel model: `2026-05-22-chu-fpt-financials.xlsx` (Stage 3 workbook populated by Chieu Chu, 2026-05-22, v2).
