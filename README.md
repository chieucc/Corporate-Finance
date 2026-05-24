# Corporate-Finance — BUS-629 Portfolio

**Student:** Chieu Chu · ChieuCC@fpt.com  
**Course:** BUS-629 International Corporate Finance, Vietnam EMBA, Shidler College of Business  
**Company analysed:** FPT Corporation (FPT · HoSE)

## About me

I am passionate about building technology that creates meaningful impact in healthcare and people's lives. With nearly 20 years of experience in software engineering and global delivery management, I currently serve as Global Healthcare Center Director at FPT Software, where I lead international healthcare and med-tech initiatives across the U.S., Japan, and Asia-Pacific markets.

My work focuses on AI-native software development, digital healthcare transformation, and scaling high-performing global engineering teams. I am especially inspired by the potential of AI and emerging technologies to improve healthcare accessibility, efficiency, and patient outcomes worldwide.

I earned my degree in Software Engineering from Hanoi University of Science and Technology and hold PMP and miniMBA certifications. Throughout my career, I have led multinational teams, delivered large-scale healthcare technology solutions, and helped expand FPT's global healthcare business.

Looking ahead, I aim to further strengthen my global leadership and business expertise through an MBA program while continuing to drive innovation at the intersection of healthcare and technology. My long-term goal is to help shape the future of AI-driven healthcare and build transformative ventures that create lasting impact across the Asia-Pacific region.

---

## What you'll find here

This repository is the complete deliverable for the BUS-629 five-stage corporate finance project. It documents selecting FPT Corporation as the subject company, sourcing and modelling its FY2025 financials from the Vietnamese Accounting Standards Annual Report, drafting a machine-readable technical specification, executing that specification with an LLM, and evaluating the output with human judgment. Every directory has a README explaining what it contains, every file follows the `YYYY-MM-DD-{lastname}-{company-slug}-{kind}` naming convention, and the prompt log in `deliverables/` records every significant AI interaction from Stage 3 through Stage 5.

## Project status

| Stage | Description | Key deliverable | Status |
|---|---|---|---|
| Stage 1 | Performance ratios template | `models/templates/performance-ratios-template.xlsx` | ✅ Complete |
| Stage 2 | Company selection memo — FPT Corporation | `docs/decisions/2026-05-24-chu-fpt-selection.md` | ✅ Complete |
| Stage 3 | Populate FY2025 financials workbook | `models/builds/2026-05-22-chu-fpt-financials.xlsx` | ✅ Complete |
| Stage 4 | Technical specification v2.0 (with HIL review) | `docs/specs/2026-05-24-chu-fpt-spec.md` | ✅ Complete |
| Stage 5 | LLM analysis, verification, retrospective, final analysis | `deliverables/` | ✅ Complete |

## Repository structure

```
Corporate-Finance/
├── README.md                    # This file
├── RESUME.md                    # Professional resume
├── BIO.md                       # Extended biography
├── LICENSE                      # MIT License
├── .gitignore
├── docs/
│   ├── decisions/               # Stage 2 company selection memo
│   └── specs/                   # Stage 4 technical specification
├── models/
│   ├── templates/               # Stage 1 blank ratios template
│   └── builds/                  # Stage 3 populated FPT financials workbook
├── analysis/
│   └── validation/              # Stage 5 manual ratio verification table
└── deliverables/
    ├── prompt-log.md            # All AI sessions logged (Stages 3–5)
    ├── *-llm-raw.md             # Stage 5 unedited LLM output
    ├── *-final-analysis.md      # Stage 5 human-reviewed final analysis
    └── *-spec-retrospective.md  # Stage 5 spec retrospective
```
