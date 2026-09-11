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
