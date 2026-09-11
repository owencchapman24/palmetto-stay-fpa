# Palmetto Stay — Operating Performance Review & Reforecast

Excel-based FP&A case study for a fictional limited-service hotel, featuring annual budgeting, actual-vs-plan variance analysis, driver-based reforecasting, scenarios, and management reporting. The project is designed as a focused Analyst I portfolio case with a governed, auditable path from source facts to a two-page management review.

> **Current status: Phase 1 complete; synthetic case v1.0 is frozen; financial implementation has not started.**

> **Synthetic-case disclosure:** Palmetto Stay is a fictional hotel created for an independent FP&A portfolio project. All company-specific historical results, budgets, actuals, operating records, staffing information, and management updates are synthetic. Public sources may inform selected industry definitions and modeling practices; they are not the source of Palmetto Stay’s internal data. The project does not represent employment, client work, or access to confidential company information.

## Business and analyst assignment

Palmetto Stay is one fictional, independently operated, leased limited-service hotel with 100 available rooms. The analyst role is a junior FP&A analyst supporting a property finance manager through the June 2026 close, first-half performance review, and revised July–December outlook, culminating in a two-page management-facing output.

## Locked scope

- Build a frozen 2026 annual budget from operating drivers.
- Load synthetic actual facts for January–December 2025 and January–June 2026.
- Analyze June and year-to-date actual performance against budget, including revenue volume/mix/rate and cost-driver variances.
- Reforecast July–December 2026 while preserving actuals, seasonality, and known timing.
- Compare Base, Upside, and Downside scenarios through operational-driver changes.
- Report room revenue, modeled property operating costs, hotel KPIs, and property operating contribution.
- Keep the work to one property, exactly eight workbook tabs, a two-page management output, and a 21–30-hour total build ceiling.

The approved exclusions include multi-property operations, ancillary restaurants/events/bars/spas, daily booking or booking-channel analysis, employee-level planning, integrated balance-sheet or cash-flow statements, debt, valuation, machine learning, Monte Carlo simulation, databases, Tableau, custom applications, enterprise planning architecture, automated narratives, excessive scenarios, and a large codebase.

## Planned final deliverables

- `model/Palmetto_Stay_FP&A_Model.xlsx` — an eight-tab Excel model.
- Five frozen source-data CSV files in `data/`.
- `outputs/Palmetto_Stay_Management_Review.pdf` — the two-page management review.
- Two selected review images in `images/`.
- Supporting case brief and methodology documentation in `docs/`.

The Phase 1 source files and documentation now exist. The final FP&A workbook, budget build, variance analysis, reforecast, scenarios, management output, PDF, and portfolio images have not been built. Results and conclusions will be added only after the model has been built and validated.

## Available Phase 1 source files

- `data/approved_budget_assumptions.csv` — the approved 2026 driver assumption pack for the future Budget tab.
- `data/operating_actuals.csv` — occupied room nights and recorded room revenue by customer segment.
- `data/labor_actuals.csv` — recorded housekeeping hours, housekeeping payroll, fixed-staff FTE, and fixed-staff payroll.
- `data/financial_actuals.csv` — recorded monthly financial lines.
- `data/case_updates.csv` — dated management and operating observations through July 8, 2026.

Case version `v1.0` contains January–December 2025 historical actuals, January–June 2026 recorded actuals, and the January–December 2026 approved assumption pack. The private deterministic Case Builder is retained outside this public repository.

## Implementation phases

1. **Phase 0 — Repository foundation and project governance (complete):** defined and locked the project before implementation.
2. **Phase 1 — Synthetic case construction, validation, and freeze (complete):** produced deterministic source facts privately and published validated frozen inputs.
3. **Phase 2 — Workbook architecture and frozen annual budget:** build the eight-tab workbook and driver-based budget.
4. **Phase 3 — Actuals, KPIs, and variance analysis:** load recorded facts and build reconciled performance analysis.
5. **Phase 4 — Reforecast and scenarios:** create the July–December outlook and three operational scenarios.
6. **Phase 5 — Management output and repository packaging:** complete the two-page review and recruiter-ready repository.
7. **Phase 6 — Independent audit, remediation, and final release:** validate, correct, and release the finished case.

If the 21–30-hour ceiling is threatened, scope will be reduced rather than expanded.

## Planned final repository structure

```text
palmetto-stay-fpa/
├── README.md
├── model/
│   └── Palmetto_Stay_FP&A_Model.xlsx
├── data/
│   ├── approved_budget_assumptions.csv
│   ├── financial_actuals.csv
│   ├── operating_actuals.csv
│   ├── labor_actuals.csv
│   └── case_updates.csv
├── docs/
│   ├── PROJECT_SPEC.md
│   ├── DECISION_LOG.md
│   ├── case_brief.md
│   └── methodology_and_sources.md
├── outputs/
│   └── Palmetto_Stay_Management_Review.pdf
└── images/
    ├── management_review.png
    └── variance_bridge.png
```

The Phase 0 governance files and Phase 1 source-data and documentation files now exist. Empty model, output, and image directories have not been created.

## Intended recruiter review experience

A reviewer will be able to understand the assignment and governance from the repository landing page, open the finished workbook to trace assumptions through budget, actuals, variances, forecast, scenarios, and checks, and then review the same management conclusions in a concise two-page PDF. The completed case is intended to demonstrate disciplined entry-level FP&A judgment, transparent formulas, exact reconciliations, and concise communication—not enterprise-system complexity.
