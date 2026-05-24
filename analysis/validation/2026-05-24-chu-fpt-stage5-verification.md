# Stage 5 Verification — FPT Corporation FY2025

**File:** `analysis/validation/2026-05-24-chu-fpt-stage5-verification.md`
**Author:** Chieu Chu · Date: 2026-05-24
**Purpose:** Manual recomputation of five ratios using standard textbook formulas to verify the Stage 5 LLM analysis. Where formulas differ from the spec's named-range convention, discrepancies are flagged and their cause identified.

---

| Ratio | Formula (named-range notation) | Manual value (show arithmetic) | LLM's value | Match? | One-line note |
|-------|-------------------------------|-------------------------------|-------------|--------|---------------|
| **ROA** | `INC_net / ((BAL_assets_total_2025 + BAL_assets_total_2024) / 2)` | 11,232.339 / ((88,141.990 + 71,999.996) / 2) = 11,232.339 / **80,070.993** = **14.03%** | 16.49% | ✗ | LLM used after-tax operating income (11,872.049) and start-of-year assets (71,999.996) per spec convention; textbook ROA uses net income and average assets, producing 14.03% — a 246 bp difference. |
| **Current Ratio** | `BAL_assets_current_2025 / BAL_liabilities_current_2025` | 58,137.438 / 41,524.928 = **1.40x** | 1.40x | ✓ | Point-in-time year-end balances; no averaging or convention ambiguity. |
| **Days Sales Outstanding** | `(BAL_receivables_2025 / INC_sales_2025) × 365` | (14,402.017 / 70,112.825) × 365 = 0.20541 × 365 = **75.0 days** | 59.3 days | ✗ | LLM used prior-year (start-of-year) receivables (11,381.524) per spec's named range `startYear_receivables`; standard DSO uses year-end receivables (14,402.017), giving 75.0 days — a 15.7-day gap that matters when benchmarking against industry peers. |
| **Inventory Turnover** | `INC_cogs_2025 / ((BAL_inventory_2025 + BAL_inventory_2024) / 2)` | 44,224.296 / ((2,193.770 + 1,856.757) / 2) = 44,224.296 / **2,025.264** = **21.84x** | 23.82x | ✗ | LLM used start-of-year inventory only (1,856.757) per spec's `startYear_inventory`; the two-year average denominator (2,025.264) gives 21.84× — a 1.98× understatement of how efficiently FPT cycles its inventory. |
| **Debt-to-Equity** | `BAL_liabilities_total_2025 / BAL_equity_shareholders_2025` | 44,393.950 / 43,748.041 = **1.015x** | 0.044x | ✗ | LLM used long-term debt only (1,903.790) per spec's narrow `BAL_debt_long_term_curr` definition; total liabilities (44,393.950) gives 1.015x — a 23× difference driven by 19,169.697 B VND in short-term debt that the spec excludes from its leverage ratio. |
