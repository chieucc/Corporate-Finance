# FPT Corporation — Final Ratio Analysis

**Company:** FPT Corporation (FPT · HoSE)
**Fiscal Period:** FY2025 (year ended 31 December 2025), FY2024 comparative
**Reporting Standard:** Vietnamese Accounting Standards (VAS) · Currency: Billions VND (B VND)
**Author:** Chieu Chu
**Date:** 2026-05-24
**Course:** BUS-629 International Corporate Finance, Vietnam EMBA
**Shidler College of Business — University of Hawaiʻi at Mānoa**

> **Spec retrospective:** `deliverables/2026-05-24-chu-fpt-spec-retrospective.md`
> **Verification file:** `analysis/validation/2026-05-24-chu-fpt-stage5-verification.md`

---

## 1. Company & Data Summary

FPT Corporation is Vietnam's largest integrated technology company, operating across three core segments: Technology (FPT Software — offshore IT services, domestic IT services, and system integration), Telecommunications (FPT Telecom — broadband and digital content), and Education (FPT University, FPT Polytechnic, FPT School). As of FY2025, FPT Software's export revenues — primarily from Japan, the US, and Europe — have become the highest-margin and fastest-growing segment, which is important context for reading the margin and efficiency figures below.

**Accounting standard notes.** FPT reports under Vietnamese Accounting Standards (VAS), which differs from IFRS in several ways relevant to this analysis:

- VAS does not require consolidation of variable-interest entities in the same way IFRS 10 does, which means some joint ventures and associates may be reflected at cost rather than mark-to-market, potentially understating total asset base.
- VAS allows flexibility in revenue recognition timing for multi-year IT service contracts, which may explain the large "other income" residual (5,779.027 B VND) derived as PBT − EBIT + interest. This residual is a model artefact, not a reported line item — graders should be aware that it aggregates financial income, gains on disposals, and share of associates' profit.
- Depreciation in this model is sourced from the Cash Flow Statement (Code 02 D&A add-back = 2,914.178 B VND), not a separately reported income statement line, because VAS does not require standalone D&A disclosure. This is standard practice for VAS-based models but should be disclosed.

**Assumptions confirmed:**

| Assumption | Value | Source |
|------------|-------|--------|
| Share price | 96,000 VND (9.6 × 10⁻⁵ B VND) | HoSE year-end FY2025 closing price |
| Shares outstanding | 1,703,507,121 | Code 411 owners' capital ÷ par value 10,000 VND |
| Cost of capital (WACC) | 9% | BUS-629 class working WACC |
| Tax rate | 21% | Vietnam statutory corporate income tax |

**Convention disclosure.** This model uses start-of-year (prior-year) denominators for asset turnover, receivables turnover, and inventory turnover — matching FPT's asset base at the start of the period being measured. This produces higher turnover and ROA figures than the two-year average convention. Where the gap is material, both figures are reported below. Readers benchmarking these ratios against peer databases (Bloomberg, FactSet) should use the average-denominator figures.

---

## 2. Ratio Results & Interpretation

### 2a. Performance

FPT's performance ratios are exceptional by any regional benchmark.

**Market Value Added (MVA): 119,788.643 B VND.** The equity market places a premium of nearly 120,000 B VND over FPT's reported book equity of 43,748 B VND. This isn't surprising given FPT's brand strength in Vietnam's digitisation wave and its growing offshore software reputation in Japan (where FPT is now among the top foreign IT vendors by revenue). Market-to-Book of **3.74x** reflects investor confidence in earnings durability — the multiple is comparable to mid-tier Indian IT services firms (Infosys, Wipro trade at 3–5x book), which is the right peer group for FPT Software.

**Economic Value Added (EVA): 8,611.549 B VND.** After charging 9% on start-of-year invested capital of 36,228.896 B VND (capital charge: 3,260.601 B VND), FPT still generated 8,611 B VND of economic profit. The 23.8% spread between actual return and capital cost is a strong signal. In my view, this EVA is structurally durable as long as FPT Software continues winning multi-year contracts — the near-invisible long-term debt (1,903.790 B VND) keeps the capital charge base lean, which mechanically inflates EVA. If FPT ever takes on significant long-term debt to fund acquisitions, this spread will compress even if operating income holds steady.

*Minor correction:* The EVA stated in the LLM output (8,611.549 B VND) differs from the value computed directly from the spec's stated component values (8,611.448 B VND) by 0.101 B VND. This is a rounding artefact — the spec's displayed `startYear_equity` (35,727.780 B VND) differs marginally from the workbook's full-precision cell. The difference is immaterial (0.001% of EVA) and does not affect the conclusion.

---

### 2b. Profitability

**ROA — convention disclosure required.** Two conventions are used in this model:

| Basis | Formula | Value |
|-------|---------|-------|
| Start-of-year assets (spec convention) | ATOI / prior-year total assets | **16.49%** |
| Average assets (textbook convention) | ATOI / avg total assets | **14.83%** |
| Net income / average assets (standard benchmark) | net income / avg total assets | **14.03%** |

The spec's 16.49% is correct per the model's convention but cannot be directly compared to industry peer ROA figures, which use net income and average assets. For benchmarking purposes, **14.03% is the appropriate figure**. That said, 14% ROA is still outstanding — FPT's closest public comparables in Southeast Asian IT services rarely exceed 8–10% on the same basis.

**ROC: 32.77% (start capital).** This is the ratio I trust most for FPT, because the capital base is genuinely small — FPT funds growth primarily with retained earnings and short-term debt, keeping long-term capital lean. A 32.77% ROC against a 9% cost of capital means FPT is generating economic rents at nearly 4× the hurdle rate. That's not an accounting artefact; it reflects the genuine pricing power of FPT's education and offshore software businesses.

**ROE: 31.44% (start equity), 28.27% (average equity).** The 3.17 pp gap between the two measures reflects the pace of equity growth in FY2025 (+22.5%, from 35,727.780 to 43,748.041 B VND), driven partly by retained earnings (6,658.585 B VND) and partly by new share issuance (common stock increased from 24,699.460 to 29,446.001 B VND, +4,746.541 B VND). The equity dilution from new issuance is not harmful at these return levels, but it does mean the reported ROE is flattered by the start-of-year denominator.

**Margins.** Net profit margin of **16.02%** and operating profit margin of **16.93%** are separated by only 91 basis points. This narrow gap is the most reassuring single data point in the income statement: FPT has a virtually frictionless path from operating income to shareholder return. For a company doing 70,000 B VND in revenue, 810 B VND of interest expense is effectively noise.

---

### 2c. Efficiency

**Asset turnover: 0.974x (spec convention) / 0.880x (average-assets basis).** The spec figure is within the 0.8–1.2x technology-services range. The average-assets figure of 0.880x is closer to the lower bound, reflecting FPT's heavy FY2025 investment activity (11,624.743 B VND net investing outflows). If these investments — primarily in IT infrastructure and education campuses — generate the revenue growth management has guided for, asset turnover will recover in FY2026–27. If they don't, this ratio will continue to compress.

**Receivables — the real story.** The ACP of **59.3 days** (spec convention, start-of-year receivables) understates the current problem. Using year-end receivables — the convention most peer databases and auditors apply — the figure is **75.0 days**. This is the number I would present to management, not 59.3. Receivables grew 27% YoY (11,382 → 14,402 B VND) against roughly 17% revenue growth. In my experience watching Vietnamese IT service companies, this pattern usually reflects one of two things: (1) the government IT segment, where payment delays of 60–90 days are standard and worsening, or (2) aggressive revenue recognition on milestone contracts that haven't yet been collected. Either way, the 75.0-day DSO should be the headline figure in any management discussion.

**Inventory turnover: 23.82x (spec) / 21.84x (average-inventory convention).** The gap is modest (1.98x) and both figures confirm FPT's service-dominant mix. Not a material concern.

---

### 2d. Leverage

This section requires more nuance than the LLM provided.

**The two-number leverage problem.** The Long-term Debt Ratio of **4.17%** and Long-term D/E of **0.044x** are technically correct but dangerously incomplete as a leverage summary. The Total Debt Ratio of **50.37%** — half the asset base financed by creditors — tells a very different story. And total interest-bearing debt (short-term 19,169.697 + long-term 1,903.790 = **21,073.487 B VND**) gives a total D/E of **0.48x**, which is the figure a credit analyst or potential lender would use. The LLM correctly identified the 33% YoY increase in short-term debt as a risk but never tied it to a total D/E figure — so the reader was left with 0.044x and a prose warning that didn't add up.

**Short-term debt risk in Vietnamese context.** In Vietnam's credit market, short-term bank facilities are the dominant corporate financing instrument — rolling short-term credit lines at state-owned banks (Vietcombank, BIDV) is standard practice for companies of FPT's tier. This reduces (but does not eliminate) refinancing risk compared to, say, US commercial paper markets. FPT's TIE of **9.97x** and cash coverage of **13.57x** are strong buffers. However, the 33% YoY increase in short-term debt (4,723.459 B VND net new borrowing from the CF statement) combined with net investing outflows of 11,624.743 B VND suggests FPT is using short-term credit to partially fund long-cycle investments. That maturity mismatch is worth flagging even in a Vietnamese market context.

**Debt-service capacity is genuine.** TIE of 9.97x means EBIT could fall 90% before interest coverage becomes a concern. That's not a risk that needs to be managed in the near term.

---

### 2e. Liquidity

**Current ratio: 1.40x.** Adequate, not comfortable. The 41,524.928 B VND current liability base is large enough that a 10% shortfall in receivables collection could compress this ratio to 1.24x — below the 1.25x threshold many Vietnamese banks use as a covenant trigger. That's not an imminent risk given the 10,136.043 B VND operating cash flow, but it's worth watching.

**Cash ratio: 0.967x.** This is the number that surprised me most in the entire analysis. FPT holds 40,153 B VND in cash and short-term investments — equivalent to 97% of all current liabilities — while simultaneously running a 33% short-term debt increase and a large investment programme. The cash holding is likely a combination of: (1) deposits at affiliate banks earning above-market rates (common for large Vietnamese corporates), (2) restricted cash for government project bonds, and (3) cash from FPT Telecom's strong operating cash generation that hasn't yet been deployed. The LLM flagged this as "sub-optimal" but was too gentle — for a company earning 32.77% ROC, holding 40,000 B VND in low-yield deposits is a meaningful drag on shareholder value.

---

## 3. Du Pont Analysis

```
ROE = Leverage × Asset Turnover × Operating Profit Margin × Debt Burden
    =   2.015  ×     0.974      ×        16.93%           ×   0.9461
    = 31.43%  (vs. direct ROE of 31.44% — gap of 0.01 pp, within tolerance)
```

**Is the LLM's interpretation sound?** Largely yes, with one addition. The LLM correctly identified Operating Profit Margin as the primary ROE driver and correctly explained the time-mismatch. The sustainability assessment was reasonable. What it missed is this: the four components are not independent.

FPT's Leverage (2.015x) is elevated primarily because of short-term liabilities — the same short-term debt whose 33% YoY increase was flagged in the Leverage section. If FPT addresses that maturity mismatch (Recommendation 2 below), leverage will fall toward 1.7–1.8x. That would reduce Du Pont ROE by approximately 2.3 pp, all else equal. In other words, the "liability management" recommendation has a direct ROE cost. A rigorous analysis should state this explicitly: cleaning up the balance sheet means accepting a lower Du Pont ROE in the short term in exchange for structural resilience. That trade-off is worth making, but the LLM presented the two recommendations (refinancing + ROE sustainability) as if they were independent, when they are in tension.

**Primary driver confirmation.** Margin (16.93%) is the right answer. FPT's software segment operates at gross margins materially above telecoms (my estimate: 35–40% for FPT Software vs. 55–60% gross but 15–20% EBIT for FPT Telecom after network D&A). The consolidated 16.93% operating margin is therefore a blended figure that would improve if the software segment's revenue share continues to grow relative to telecoms. That's the strategic thesis: invest in the margin-accretive segment (software + education), manage the cash-generative but margin-dilutive segment (telecoms).

**Time-mismatch note.** The 0.01 pp gap (Du Pont 31.43% vs. direct 31.44%) is within the spec's tolerance. Given FPT's 22% asset growth in FY2025, in a slower growth year the gap would narrow further.

---

## 4. Strategic Recommendations

I've kept the three most grounded recommendations from the LLM analysis and replaced two that were either outside BUS-629 scope or less actionable.

### Recommendation 1: Standardise receivables collection to 45 days for enterprise customers *(Efficiency → Liquidity)*

The 27% YoY growth in receivables (11,382 → 14,402 B VND) against 17% revenue growth is the clearest operational red flag in the FY2025 financials. Using the standard DSO formula (year-end receivables), collection has deteriorated to **75 days**, not the 59.3 days the spec reports.

**Action:** Within 12 months, renegotiate payment terms with the top-20 enterprise customers by receivables balance to standardise at net-45. Introduce a 1.5–2% early-payment discount for settlement within 30 days. For government IT contracts (where payment timing is structural), build explicit payment milestones into new contract terms rather than accepting project-completion billing.

**Expected impact:** Reducing DSO from 75 to 50 days frees approximately 4,800 B VND in working capital (25 days × 192 B VND daily sales). Quick Ratio improves from 1.31x toward 1.43x; short-term debt pressure reduces proportionally.

---

### Recommendation 2: Refinance 10,000 B VND of short-term debt into 5-year instruments *(Leverage → Liquidity)*

FPT's short-term debt of 19,170 B VND funds long-cycle assets (capex: 5,098 B VND; other investing: 6,534 B VND in FY2025 alone). This maturity mismatch is the most structural risk in the balance sheet. FPT's creditworthiness — 9.97x TIE, 31.44% ROE, investment-grade-equivalent fundamentals — should allow issuance of 5-year bonds at 7.5–8.0% in Vietnam's domestic corporate bond market (Hanoi Stock Exchange bond segment, or HNX).

**Action:** Within 18 months, issue 10,000 B VND in 5-year fixed-rate bonds. Use proceeds to retire the most expensive short-term facilities.

**Expected impact:** Current Ratio improves from 1.40x to ~1.65x. TIE declines modestly from 9.97x to ~8.7x (still well within safe coverage). ROE declines approximately 1.5 pp as leverage falls — this is the intentional trade-off for structural resilience. Note: this recommendation is in tension with the Du Pont ROE maximisation objective; the trade-off is explicitly worth making.

---

### Recommendation 3: Set a formal capital allocation policy for the 40,000 B VND cash position *(Performance → Efficiency)*

Cash and marketable securities of **40,153 B VND** represent 45.6% of total assets. This holding generates negligible return relative to FPT's 32.77% ROC. There is no strategic rationale for a technology company to hold nearly 100% of its current liabilities in cash.

**Action:** FPT's Board should adopt a Capital Allocation Policy within six months:
- **Operational reserve:** 15,000 B VND (sufficient for 1.5 months of operating costs, covering working capital and covenant headroom).
- **Strategic reserve:** 5,000 B VND earmarked for opportunistic M&A in the ASEAN software/edtech space.
- **Deployed capital:** The remaining 20,000 B VND should be: (a) 10,000 B VND into accelerated capex in FPT University campus expansion (EBIT margins ~30%+) and FPT Software offshore delivery centres; (b) 10,000 B VND returned to shareholders via a share buyback at current market price.

**Expected impact:** Deploying 10,000 B VND at the current ROC (32.77%) generates ~3,277 B VND in additional ATOI annually — expanding EVA by the same amount. The buyback reduces the equity base, mechanically raising ROE from 31.44% toward 34–35%.

---

*Recommendations 4 and 5 from the LLM output — excess-cash deployment and receivables securitisation — were partially incorporated above. Securitisation (Rec 5) was removed as it involves structured finance instruments outside BUS-629 course scope and requires regulatory approvals under Vietnam's Asset Securitisation framework that make it unlikely within a 12–24 month horizon.*

---

## 5. LLM Evaluation & Annotations

### What the LLM executed correctly

- **Formula accuracy:** All 25+ ratios were computed without error against the spec's named-range definitions. Zero formula errors in 89 Excel calculations.
- **Structural compliance:** All ten output sections appeared in the correct order. Word counts were within target ranges.
- **Du Pont decomposition:** The four-component decomposition was arithmetically correct (31.43%), the time-mismatch was disclosed, and the primary driver (margin) was correctly identified.
- **Validation rules:** All six spec validation checks were addressed explicitly, including the Du Pont ROA confirmation and the net income allocation check (4,573.754 + 6,658.585 = 11,232.339).
- **Cross-category connections:** The Efficiency → Liquidity connection (receivables → quick ratio), Leverage → Performance (low interest burden → EVA), and Du Pont component interactions were all correctly articulated.

### Where the LLM deviated or oversimplified

**1. Convention gaps not disclosed** *(spec gap, not LLM error).*
The LLM followed the spec precisely — which meant it reported ROA as 16.49%, DSO as 59.3 days, and inventory turnover as 23.82× without flagging these are spec-convention figures, not standard textbook figures. The verification table showed:

| Ratio | Spec-convention (LLM) | Standard textbook | Gap |
|-------|----------------------|-------------------|-----|
| ROA | 16.49% | 14.03% | 246 bp |
| DSO | 59.3 days | 75.0 days | 15.7 days |
| Inventory turnover | 23.82× | 21.84× | 1.98× |

This is primarily a spec gap (the spec should have required the LLM to report both figures). But the LLM also had enough information in the spec to notice the convention difference — the spec listed both ROA (start assets) and ROA (average assets), so the parallel structure was there. A more analytical LLM output would have extended that parallel to DSO.

**2. D/E ratio incomplete** *(spec gap).*
The LLM reported Long-term D/E as 0.044x without noting that total interest-bearing D/E = 0.48x. The 33% short-term debt increase was discussed in prose, but these two observations were never connected into a single, coherent leverage summary. The reader left with 0.044x as the headline leverage number — which is misleading.

**3. Receivables DSO understated** *(spec gap + LLM limitation).*
The 59.3-day ACP conceals the 75.0-day standard DSO. In the Efficiency section, the LLM correctly flagged the 27% receivables growth but then used 59.3 days as the benchmark figure, which understates the problem. A human analyst familiar with Vietnamese enterprise payment norms would have immediately noted that 75 days is closer to the structural reality for Vietnamese IT service companies.

**4. Recommendation 5 (securitisation) out of scope.**
Receivables securitisation is a legitimate tool but involves Vietnam's nascent ABS market (SBV Circular 39/2016, regulations still maturing), makes assumptions about advance rates that cannot be verified from public data, and is outside BUS-629 course scope. This was a spec gap (the spec placed no constraint on recommendation sophistication) — but the LLM should have flagged the implementation complexity rather than presenting it as a near-term 18-month action.

**5. Vietnam market context absent.**
The LLM had no knowledge of: FPT Software's Japan exposure and Japanese client payment norms (notoriously slow — 60–90 days standard), the VAS revenue recognition flexibility on multi-year contracts, the role of state-owned bank relationships in short-term credit rollover, or FPT University's position as Vietnam's largest private university. These contextual factors matter for interpreting the receivables trajectory, the short-term debt pattern, and the education segment's margin structure. This is an LLM limitation, not a spec gap — no specification document could have substituted for first-hand industry knowledge.

### Error classification summary

| Issue | Caused by spec gap | Caused by LLM limitation |
|-------|-------------------|--------------------------|
| ROA convention undisclosed | ✓ | — |
| DSO start-of-year vs. year-end | ✓ | Partially (LLM had the data) |
| D/E narrow definition | ✓ | — |
| Rec 5 scope overshoot | ✓ | — |
| No Vietnam market context | — | ✓ |

---

## 6. Executive Justification

*This section is mine, not the LLM's.*

I've worked with FPT's products and services across my career in Vietnam's technology sector. The numbers in this analysis are impressive, but what they don't show is why they're sustainable — and where the real risk is.

FPT is Vietnam's best-positioned beneficiary of two structural trends: Vietnam's domestic digital transformation (government IT, enterprise ERP, cloud migration) and the global demand for cost-competitive software development outside India. FPT Software's revenue from Japan alone — which I estimate accounts for 40–50% of technology segment revenue — is built on relationships that took 15+ years to cultivate and cannot be replicated quickly by a competitor. That's the moat behind the 16.93% operating margin and the 32.77% ROC. The numbers are high because the competitive position is genuine.

The risk the ratios understate is receivables. I noted above that standard DSO is 75 days, not 59 days. In practice, what I see is that a significant portion of FPT's receivables are government IT contracts — Ministry of Public Security, Ministry of Health, provincial government systems — where payment is structurally delayed by budget release cycles, not by client credit problems. This means the receivables are almost certainly collectible, but the cash conversion cycle is genuinely long. Management should not be blamed for 75-day DSO in this segment; they should be pushed to restructure contract terms so that more cash comes in at delivery milestones rather than at project sign-off.

The 40,000 B VND cash holding is the most puzzling feature of the balance sheet. My best interpretation: FPT Telecom generates strong, predictable operating cash flow (~6,000–7,000 B VND annually, my estimate), and that cash is sitting in deposit accounts at affiliated banks rather than being deployed. FPT University is capital-constrained (campus expansion is expensive) but is the highest-margin growth segment. The strategic decision I'd push management on is simple: invest more aggressively in education infrastructure, buy back shares, and stop hoarding cash.

**Investment thesis:** FPT is a strong hold at the current 96,000 VND / 3.74x book multiple. The fundamentals — EVA of 8,600+ B VND, ROC at 33%, margin above 16% — justify a premium to regional peers. The risks (short-term debt maturity mismatch, DSO creep, cash hoarding) are all self-inflicted and correctable with management action, not structural. If FPT executes on the three recommendations above — receivables discipline, debt maturity extension, capital deployment — the stock has a credible path to 110,000–120,000 VND within 18–24 months as cash return and ROE improvement are priced in. I would not add aggressively at current prices without seeing FY2026 Q1 receivables data; if DSO continues to widen past 80 days, that changes the thesis.

---

## Ratio Summary Table

| Category | Ratio | Spec-convention value | Textbook-convention value | Unit |
|----------|----|---|---|---|
| **Performance** | MVA | 119,788.643 | — | B VND |
| | Market-to-Book | 3.74 | — | x |
| | EVA | 8,611.5 | — | B VND |
| **Profitability** | ROA | 16.49% (ATOI, start assets) | 14.03% (net income, avg assets) | % |
| | ROA (average assets) | 14.83% (ATOI) | 14.03% (net income) | % |
| | ROC (start capital) | 32.77% | — | % |
| | ROC (average capital) | 29.00% | — | % |
| | ROE (start equity) | 31.44% | — | % |
| | ROE (average equity) | 28.27% | — | % |
| | Net Profit Margin | 16.02% | — | % |
| | Operating Profit Margin | 16.93% | — | % |
| **Efficiency** | Asset Turnover | 0.974x (start assets) | 0.880x (avg assets) | x |
| | Receivables Turnover | 6.16x (start recv) | 4.87x (year-end recv) | x |
| | Collection Period / DSO | 59.3 days (start recv) | **75.0 days** (year-end recv) | days |
| | Inventory Turnover | 23.82x (start inv) | 21.84x (avg inv) | x |
| | Days in Inventory | 15.3 days | 16.7 days (avg inv) | days |
| **Leverage** | Long-term Debt Ratio | 4.17% | — | % |
| | Long-term D/E | 0.044x | — | x |
| | **Total Interest-bearing D/E** | — | **0.48x** | x |
| | Total Debt Ratio | 50.37% | — | % |
| | Times Interest Earned | 9.97x | — | x |
| | Cash Coverage | 13.57x | — | x |
| | Debt Burden | 0.9461x | — | x |
| | Leverage (assets/equity) | 2.015x | — | x |
| **Liquidity** | NWC-to-Assets | 18.85% | — | % |
| | Current Ratio | 1.40x | — | x |
| | Quick Ratio | 1.31x | — | x |
| | Cash Ratio | 0.967x | — | x |
| **Du Pont** | ROA (Du Pont) | 16.49% | — | % |
| | ROE (Du Pont) | 31.43% | — | % |

*Bold rows = figures where textbook convention produces a materially different result. Use textbook-convention values when benchmarking against peer databases.*
*ATOI = after-tax operating income = net income + (1 − 0.21) × interest expense = 11,232.339 + 639.710 = 11,872.049 B VND*
