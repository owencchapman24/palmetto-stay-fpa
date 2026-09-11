# Palmetto Stay FP&A Decision Log

This log records project-level decisions that control later implementation. It does not contain findings, results, or conclusions.

## 2026-09-11 — Blueprint v1.2 locked

**Status:** Locked

### Decisions

- Selected one fictional, independently operated, leased limited-service hotel with 100 available rooms as the business concept.
- Selected a fictional business with synthetic internal data so the portfolio case is reproducible and does not imply access to confidential company information.
- Selected Excel as the primary artifact, supported by frozen CSV source tables, concise documentation, and a two-page exported PDF.
- Set an eight-tab maximum and locked the workbook to exactly these eight tabs: Start, Data, Assumptions, Budget, Forecast, Variance, Review, and Checks.
- Set the actual-data scope to 18 months: January–December 2025 historical actuals and January–June 2026 recorded actuals. The January–December 2026 budget remains a calculated output.
- Locked the actuals-independence rule: recorded actuals are source facts; actual ADR and operating unit costs are derived from those facts; actuals must not be reconstructed from budget assumptions.
- Locked revenue variance analysis to the volume, customer-mix, and rate framework, in that order, with exact reconciliation to actual revenue less budget revenue.
- Locked housekeeping variance analysis to the volume, efficiency, and wage-rate framework, in that order, with guest-service expense analyzed through volume and unit-cost effects.
- Locked cost-change schedules to `Cost change = Actual cost - Budget cost`, where positive is unfavorable, and contribution-impact schedules to `Contribution impact = -(Actual cost - Budget cost)`, where positive is favorable. Revenue effects enter the contribution bridge without reversal.
- Fixed distribution/payment expense at 4% of recognized room revenue across budget, actuals, forecast, and scenarios, with no independent fee-rate scenario.
- Selected three vertically stacked twelve-month scenario blocks—Base, Upside, and Downside—with identical linked January–June actuals and operational-driver changes limited to July–December.
- Required the private Case Builder to use deterministic, nonvolatile Excel formulas, remain outside the public repository, and never remain linked to the public analysis workbook.
- Set an overall build ceiling of 21–30 hours and required scope reduction rather than expansion if that ceiling is threatened.
- Excluded multiple properties; restaurants, events, bars, and spas; daily booking and booking-channel analysis; employee-level planning; integrated balance-sheet and cash-flow statements; debt and valuation; machine learning; Monte Carlo simulation; SQL and databases; Tableau; custom applications; enterprise planning architecture; automated narrative generation; dozens of scenarios; and a large codebase.

### Rationale

The project should resemble excellent Analyst I work: accurate source handling, transparent driver logic, exact reconciliations, controlled forecasting, practical management communication, and disciplined scope. It should not resemble an enterprise planning system.

These decisions are locked unless a later validation failure or documented project requirement justifies a change. Any justified change must be dated and recorded in this log before implementation proceeds under the revised decision.

## 2026-09-11 — Phase 1 case version v1.0 frozen

**Status:** Locked

### Decisions

- Created and froze synthetic case version `v1.0` on 2026-09-11 using a July 8, 2026 forecast information cutoff.
- Retained a deterministic private Case Builder outside the public repository with four worksheets: Controls, Budget Pack, Actuals Generator, and Checks. The workbook contains no volatile random formulas, macros, circular references, hidden sheets, or external workbook links.
- Froze the public source interface as five static UTF-8 CSV files: a 12-row approved 2026 assumption pack, 36 segment-level operating-actual rows, 18 labor-actual rows, 144 financial-actual rows, and seven dated case updates.
- Added `data/approved_budget_assumptions.csv` as a necessary input-completeness correction. The analyst is supposed to receive an approved budget assumption pack, while the budget itself must be calculated in Phase 2. This correction adds an independent source input and does not expand analytical scope.
- Preserved the actuals-independence rule. Public actual files store recorded nights, revenue, hours, payroll, and expenses; actual ADR, productivity, wage, and guest-service unit cost remain derived.
- Applied the fixed 4% distribution/payment fee to recognized room revenue at stored source precision, with no fee-rate scenario or balancing item.
- Used monthly seasonality, fixed month-specific variation, customer mix, segment ADR, labor productivity, wage schedules, fixed commitments, and dated event effects to construct the case without plugs.
- Represented four case events: spring retail/leisure demand weakness, negotiated corporate transient support, a housekeeping wage and temporary productivity disruption, and a June marketing activity deferred to September.
- Included ordinary month-to-month variation, several immaterial differences, and one modest property-overhead item whose cause remains unconfirmed and requires later follow-up.

### Limitations and unresolved items

- The case is synthetic and monthly. It does not include daily bookings, booking-channel detail, employee-level records, ancillary revenue streams, or non-property financial statements.
- The evidence package is limited to information available through July 8, 2026.
- The May property-overhead item remains under vendor-detail review. No cause has been assigned in the frozen source data.
- Phase 1 does not contain a forecast vintage, variance conclusions, scenarios, or management recommendations.

Any source-data correction must be made through the private Case Builder, frozen as a new case version, independently revalidated, and recorded in this log.

## 2026-09-11 — Phase 2 workbook architecture and approved budget completed

**Status:** Locked

### Decisions

- Created `model/Palmetto_Stay_FP&A_Model.xlsx` with exactly eight visible worksheets in the locked order: Start, Data, Assumptions, Budget, Forecast, Variance, Review, and Checks.
- Imported the four recorded-fact and case-update CSVs as static typed values on `Data` and the approved 2026 assumption pack as static typed values on `Assumptions`. The workbook contains no external CSV or private-authoring link.
- Established `Assumptions` as the single authoritative source for the approved budget. `Budget` uses monthly date matching, internal calendar calculations, and transparent quantity-times-rate formulas; it does not depend on historical actuals, case updates, or later-phase tabs.
- Calculated FY2026 additive measures by summing monthly results and calculated occupancy, corporate share, ADR, RevPAR, productivity, effective rates, unit costs, and contribution margin from annual numerators and denominators rather than averaging monthly ratios.
- Kept expenses as positive values and subtracted total operating costs when calculating property operating contribution.
- Implemented `Checks` as a terminal control sheet covering source integrity, monthly operating logic, cost reconciliation, annual aggregation, and workbook integrity. Its master Phase 2 status exists only on `Checks`.
- Replaced the proposed formula link from `Start` to the master check result with a static instruction directing the reviewer to inspect `Checks`. This narrow control-design correction prevents check outputs from driving another worksheet while retaining a clear review step.
- Reserved `Forecast`, `Variance`, and `Review` for later phases and added intentional status notices without forecast values, variance calculations, scenarios, charts, or management conclusions.

### Validation boundary

- Phase 2 validation requires a clean formula-error scan, an independent monthly and annual budget comparison, source-value comparison, package-integrity review, visual inspection of every worksheet, and restored perturbation tests.
- Phase 2 does not authorize changes to frozen case version `v1.0`, the private Case Builder, or any Phase 3–6 analysis.

## 2026-09-11 — Phase 3 actual performance and variance attribution completed

**Status:** Locked

### Decisions

- Implemented January–June 2026 actual performance against the matched approved budget and January–June 2025 recorded actuals on `Variance`, using the July 8, 2026 information cutoff.
- Kept recorded actuals independent: source nights, revenue, labor, payroll, and expenses link from `Data`; operating ratios, rates, unit costs, contribution, and margin are derived from recorded facts.
- Implemented the locked sequential attribution methods for revenue, housekeeping, guest service, and fixed-staff payroll, with monthly effects summed to YTD and explicit interaction-order disclosure.
- Kept distribution/payment expense mechanically linked to the fixed 4% policy, presented rent, property overhead, and marketing as direct cost changes, and reconciled all effects through the property operating contribution bridge.
- Added an evidence-controlled commentary register that separates observed results from causal interpretation, preserves dated source wording and confidence, and limits Phase 4 implications to qualitative considerations rather than forecast assumptions.
- Retained all 41 Phase 2 controls and added 47 Phase 3 controls. The combined master status remains terminal on `Checks`; no model or displayed status depends on a check result.
- Kept `Forecast` and `Review` status-only. Phase 3 contains no reforecast, scenarios, management recommendations, charts, PDF, or portfolio images.

### Validation boundary

- Phase 3 validation requires exact frozen-source reconciliation, independent actual/budget/prior-year and bridge recomputation, a clean formula-error scan, all 88 controls passing, package and formula-architecture audits, rendered visual review, and disposable perturbation tests proving that source-reconciliation and key-integrity failures are detected while housekeeping driver changes do not rebuild recorded payroll.
- Phase 3 does not authorize changes to frozen case version `v1.0`, any public CSV, `docs/case_brief.md`, the private Case Builder, or any Phase 4–6 output.
