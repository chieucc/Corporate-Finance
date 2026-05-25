# Stage 5 — Instructor Review

**Student:** Chu Chieu
**Company:** FPT Corporation (FPT, HoSE)
**Reviewed:** 2026-05-25

---

## Artifact checklist

| Artifact | Status | Location |
|----------|--------|----------|
| Final analysis (evaluated) | Present | `deliverables/2026-05-24-chu-fpt-final-analysis.md` |
| LLM raw output | Present | `deliverables/2026-05-24-chu-fpt-llm-raw.md` |
| Manual verification table | Present | `analysis/validation/2026-05-24-chu-fpt-stage5-verification.md` |
| Spec retrospective | Present | `deliverables/2026-05-24-chu-fpt-spec-retrospective.md` |
| Prompt log | Present | `deliverables/prompt-log.md` |
| Stage 2 feedback response | Not found | — |

Five of six Stage 5 artifacts present. Stage 2 feedback response is not explicitly documented.

---

## Final analysis structure

The final analysis (4,202 words) demonstrates exceptional editorial voice and Vietnamese market expertise:

1. **Company & Data Summary:** VAS accounting standard notes (VAS vs IFRS consolidation, revenue recognition flexibility, D&A sourcing from CF Code 02). Convention disclosure: start-of-year denominators, with instruction to readers on benchmarking implications.
2. **Performance Ratios:** MVA 119,789 B VND, EVA 8,612 B VND (positive — 23.8% spread over WACC), M/B 3.74x (comparable to Indian IT services peers). EVA rounding note (0.101 B VND = 0.001% — immaterial).
3. **Profitability Ratios:** ROA dual-reported (16.49% spec vs 14.03% textbook), ROC 32.77% ("the ratio I trust most for FPT"), ROE 31.44%/28.27% (start/avg gap from 22.5% equity growth). Margin gap (OPM 16.93% vs NPM 16.02% = 91 bp) identified as "most reassuring data point" — virtually frictionless path from operating income to shareholder return.
4. **Efficiency Ratios:** Asset turnover 0.974x. Receivables: "the real story" — ACP 75 days (year-end) vs 59.3 (spec) = "the number I would present to management." 27% receivables growth vs 17% revenue growth flagged as operational red flag. Vietnamese IT service context (government payment delays, milestone contract recognition).
5. **Leverage Ratios:** "The two-number leverage problem" — LT D/E 0.044x vs Total D/E 0.48x. Short-term debt in Vietnamese market context (rolling state-bank facilities). Explicit D/E computation (21,073 B VND total interest-bearing / equity = 0.48x) that the LLM omitted. Maturity mismatch flagged despite Vietnamese market norms.
6. **Liquidity Ratios:** Current 1.40x ("adequate, not comfortable" — 10% receivables shortfall → 1.24x → potential covenant breach). Cash ratio 0.967x = "the number that surprised me most" — 40,153 B VND in deposits while running 33% ST debt growth. Vietnamese corporate deposit practice contextualized.
7. **Du Pont:** 4-factor (2.015 × 0.974 × 16.93% × 0.9461 = 31.43%, gap 0.01 pp). Margin identified as primary driver. Non-independence of components explained: leverage cleanup reduces ROE ~2.3 pp — "that trade-off is worth making, but the LLM presented the two recommendations as independent when they are in tension."
8. **Strategic Recommendations:** 3 retained from LLM (2 generic ones replaced): receivables → 45 days, refinance 10,000 B VND to 5-year bonds, capital allocation policy for 40,153 B VND cash.

---

## Manual verification assessment

The verification table takes an analytically sophisticated approach: rather than verifying that LLM values match the spec's formulas (they do), it verifies them against **textbook-standard formulas** and documents the convention gaps:

| Ratio | Spec value | Textbook value | Gap | Root cause |
|-------|-----------|---------------|-----|-----------|
| ROA | 16.49% | 14.03% | 246 bp | ATOI + start-year vs net income + average |
| Current Ratio | 1.40x | 1.40x | — | No convention difference |
| DSO | 59.3 days | 75.0 days | 15.7 days | Start-year vs year-end receivables |
| Inventory Turnover | 23.82x | 21.84x | 1.98x | Start-year vs average inventory |
| D/E | 0.044x | 1.015x | 23× | LT debt only vs total liabilities |

This is MORE valuable than "all match" — it surfaces how spec design choices affect benchmarking. The D/E gap (0.044x vs 1.015x) is particularly important: it shows that the LLM correctly followed the spec but produced a number (0.044x) that gives a misleading picture of FPT's actual leverage.

---

## Spec retrospective assessment

- Section-by-section verdict: 11 sections, 4 Vague + 7 Clear
- 3 gaps traced to a single root cause: formulas that deviate from textbook convention without disclosure
- 3/5 self-rating — honest, well-calibrated (most students rate 4)
- Structural revision proposal: "Convention deviation? Y/N" column in spec template
- Key insight: "the gaps were not evenly distributed — they concentrated almost entirely in Part A.6"
- Process feedback: pattern recognition that would be "invisible in narrative reflection"

---

## Kindly-worded notes

- **The convention-difference analysis in the verification table is the most analytically sophisticated verification in the cohort.** You chose the harder path: computing textbook-standard values independently and quantifying the gaps, rather than confirming the LLM followed the spec (which it did). The 246 bp ROA gap, 15.7-day DSO gap, and 23× D/E gap are real analytical insights that surface the benchmarking implications of spec design choices. A senior analyst would recognize this as a QA methodology choice.
- **The editorial voice is the strongest in the cohort.** "The number that surprised me most," "In my experience watching Vietnamese IT service companies," "I've kept the three most grounded recommendations and replaced two," "I would present to management" — these signal genuine intellectual ownership. The analysis reads as something a managing director would trust, not just review.
- **The explicit ROE cost acknowledgment (Recommendation 2) is rare.** "ROE declines approximately 1.5 pp — this is the intentional trade-off for structural resilience" demonstrates understanding that balance-sheet cleanup and return maximization are in tension. Most analysts present recommendations as costless; you present the trade-off honestly. This is more credible and more useful to a decision-maker.
- **The Du Pont non-independence observation is the most sophisticated analytical point in the cohort.** "The four components are not independent... cleaning up the balance sheet means accepting a lower Du Pont ROE" — this connects Recommendation 2 back to the decomposition and shows that you understand the model, not just the arithmetic.
- **The 3/5 self-rating is well-calibrated.** The retrospective identifies that 4/5 verification values diverge from textbook convention and correctly attributes this to spec design gaps rather than LLM errors. A student who rates themselves 5 despite evidence of gaps earns less than one who rates 3 with honest supporting evidence.
- **The one gap is Stage 2 feedback incorporation.** A short response memo (`docs/decisions/2026-05-24-chu-stage2-feedback-response.md`) tracing which Stage 2 suggestions were addressed and where they surface in later stages would close this. Even a 200-word bullet list would suffice: "Feedback point → action taken → where it appears in Stage 5."
- **The prompt log (2,850 words) is the most detailed in the cohort.** This level of documentation creates a reproducible analytical record — valuable both for grading and as a portfolio artifact that demonstrates your prompting methodology across the full project lifecycle.
