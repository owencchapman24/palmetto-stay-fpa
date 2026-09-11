# Palmetto Stay FP&A Project Specification — Blueprint v1.2

- **Status:** Locked
- **Date:** 2026-09-11
- **Implementation status:** Not started

This document is the authoritative specification for the Palmetto Stay FP&A portfolio project. The decisions below are locked and must be implemented without redesign unless a later validation failure or documented project requirement justifies a controlled change.

## 1. Business and role

- The business is one fictional, independently operated, leased limited-service hotel.
- The property has 100 available rooms.
- The role is a junior FP&A analyst supporting a property finance manager.
- The assignment begins with the June close and first-half performance review.
- The analyst will prepare a revised July–December outlook.
- The final management-facing output will be two pages.

## 2. Periods and source scope

- January–December 2025: synthetic historical actuals.
- January–December 2026: frozen budget.
- January–June 2026: synthetic recorded actuals.
- July–December 2026: reforecast.
- The full-year latest estimate equals six months of actuals plus six months of forecast.
- The forecast is not a rolling twelve-month forecast.
- The source case contains 18 months of actual facts; the budget is a calculated output.

## 3. Customer segments

- Retail/leisure transient.
- Negotiated corporate transient.
- Customer segments must not be confused with booking channels.
- Corporate demand must not automatically be treated as guaranteed room blocks.

## 4. Primary operating drivers

- Occupied room nights.
- Customer mix.
- Retail/leisure ADR.
- Negotiated corporate ADR.
- Housekeeping hours per occupied room.
- Loaded housekeeping wage.
- Guest-service cost per occupied room.
- Fixed staffing.
- Fixed and scheduled property costs.

Available room nights and occupancy are derived calculations. Occupancy and occupied room nights must not both be independent inputs.

## 5. Financial scope

The model will include:

- Room revenue.
- Housekeeping payroll.
- Guest-service expense.
- Distribution/payment expense.
- Fixed staffing payroll.
- Rent.
- Property overhead.
- Marketing.
- Property operating contribution.

**Property operating contribution** is room revenue less modeled property operating costs, including rent, before depreciation, financing, income taxes, and corporate overhead.

This measure must not be labeled GAAP operating income, EBITDA, cash flow, or standardized hotel GOP.

## 6. Actuals-independence rule

Actuals must be treated as recorded source facts.

Recorded actual inputs must include:

- Occupied room nights by segment.
- Room revenue by segment.
- Housekeeping hours.
- Housekeeping payroll.
- Guest-service expense.
- Distribution/payment expense.
- Fixed payroll and property costs.

Actual ADR, effective wage, and guest-service unit cost are derived from recorded actual facts. The Budget and Forecast tabs will use forward driver formulas. The Data tab must not reconstruct actuals from budget assumptions.

## 7. Distribution-fee rule

- Room revenue is recognized after discounts reflected in realized ADR but before separately presented distribution/payment expense.
- Distribution/payment expense equals 4% of recognized room revenue.
- The rate is fixed across budget, actuals, forecast, and scenarios.
- There is no independent fee-rate scenario.
- Fee cost variance equals 4% of revenue variance.
- Fee contribution impact equals negative 4% of revenue variance.
- The fee effect may appear as one mechanically linked contribution-bridge bar and does not require separate causal commentary.

## 8. Required variance analysis

### 8.1 Revenue: volume, customer mix, and rate

Revenue must be decomposed in this documented order:

1. Volume.
2. Customer mix.
3. Rate.

```text
Volume effect =
(Actual total occupied nights - Budget total occupied nights)
× Budget weighted-average ADR

Mix effect =
Actual total occupied nights
× Σ[(Actual segment share - Budget segment share)
× Budget segment ADR]

Rate effect =
Actual total occupied nights
× Σ[Actual segment share
× (Actual segment ADR - Budget segment ADR)]
```

These components must reconcile exactly to actual revenue less budget revenue.

### 8.2 Housekeeping: volume, efficiency, and wage rate

Housekeeping must be decomposed in this documented order:

1. Volume.
2. Efficiency.
3. Wage rate.

```text
Volume effect =
(Actual occupied nights - Budget occupied nights)
× Budget hours per occupied night
× Budget wage

Efficiency effect =
(Actual housekeeping hours
- Actual occupied nights × Budget hours per occupied night)
× Budget wage

Wage-rate effect =
Actual housekeeping hours
× (Actual effective wage - Budget wage)
```

### 8.3 Guest service and flexed cost

Guest-service expense must be decomposed into volume and unit-cost effects.

The project must include a flexed-cost comparison so that lower costs caused by serving fewer guests are not described as operating savings.

## 9. Sign conventions

Underlying cost-change schedules use:

```text
Cost change = Actual cost - Budget cost
```

Positive means higher expense and therefore unfavorable.

The contribution bridge uses:

```text
Contribution impact = -(Actual cost - Budget cost)
```

Positive means favorable to contribution. Revenue effects enter the contribution bridge without reversal. Every relevant table must state its sign convention explicitly.

## 10. Forecast framework

- The approved budget remains frozen.
- January–June actuals remain immutable.
- Actuals are identical in all scenarios.
- Only July–December assumptions may change.
- Forecast updates require dated evidence or a documented management assumption.
- The reforecast must retain seasonality and known timing.
- June must not simply be multiplied across the remaining months.
- The project must not claim improved forecast accuracy without a frozen forecast vintage and subsequent unseen actuals.

## 11. Scenarios

The workbook will use three vertically stacked twelve-month blocks:

1. **Base:** partial demand recovery.
2. **Upside:** stronger corporate pickup and earlier productivity normalization.
3. **Downside:** persistent demand weakness and slower productivity normalization.

January–June must link to identical actuals in every block. Upside and Downside should be collapsible using row grouping. Scenarios must change operational drivers rather than apply blanket percentage shocks. Probabilities must not be assigned.

## 12. Workbook architecture

The final workbook will contain exactly eight tabs, in this order:

1. Start
2. Data
3. Assumptions
4. Budget
5. Forecast
6. Variance
7. Review
8. Checks

The workbook must not contain hidden calculation tabs, macros, circular references, or external workbook links.

## 13. Management output

The final Review tab and exported PDF will contain two pages.

### Page 1

- June and YTD performance.
- Revenue and contribution versus budget.
- Occupancy, ADR, and RevPAR.
- Contribution bridge.
- Three material explanations.
- Timing-versus-ongoing classification.

### Page 2

- Full-year budget versus latest estimate.
- Base/Upside/Downside comparison.
- Monthly actual-versus-forecast trend.
- Two risks.
- Two opportunities.
- Three recommended follow-ups.

The management output is limited to a maximum of three charts and approximately 350–500 words. It must not become a decorative dashboard, and no separate slide deck will be created.

## 14. Synthetic case construction

The future private Case Builder must:

- Use deterministic, nonvolatile Excel formulas.
- Avoid `RAND()` and `RANDBETWEEN()`.
- Use capacity, seasonality, customer mix, segment ADR, fixed monthly variation, operating events, labor productivity, and wage schedules.
- Produce values that are later pasted into public source tables.
- Remain outside the public repository.
- Be retained privately so the case can be regenerated.
- Never remain linked to the public analysis workbook.

The case must contain ordinary variation, immaterial variances, at least one inconclusive variance, events affecting multiple lines, and effects that normalize over time.

The four planned case events are:

1. Spring retail/leisure demand weakness.
2. A shift toward negotiated corporate volume.
3. A housekeeping wage increase with temporary productivity disruption.
4. A June marketing activity deferred to September.

## 15. Frozen-data version control

- The initial frozen case version is `v1.0`.
- Actuals must not be hand-patched to make analysis reconcile.
- Source-data errors must be corrected through the private Case Builder.
- Source changes require a new case version, revalidation, and documentation.
- Workbook-formula corrections do not require changing valid frozen source data.

## 16. Planned final repository structure

This is the planned final structure. Directories and deliverables that are not needed in Phase 0 must not be created early.

```text
palmetto-stay-fpa/
├── README.md
├── model/
│   └── Palmetto_Stay_FP&A_Model.xlsx
├── data/
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

The private `Palmetto_Stay_Case_Builder_AUTHORING.xlsx` is intentionally excluded from this public structure.

## 17. Phase plan and effort control

- **Phase 0 — Repository foundation and project governance.**
- **Phase 1 — Synthetic case construction, validation, and freeze.**
- **Phase 2 — Workbook architecture and frozen annual budget.**
- **Phase 3 — Actuals, KPIs, and variance analysis.**
- **Phase 4 — Reforecast and scenarios.**
- **Phase 5 — Management output and repository packaging.**
- **Phase 6 — Independent audit, remediation, and final release.**

The overall build ceiling is 21–30 hours. If that ceiling is threatened, scope must be reduced rather than expanded.

## 18. Explicit exclusions

The project will not include:

- Multiple properties.
- Restaurants, events, bars, or spas.
- Daily booking data.
- Booking-channel analysis.
- Employee-level planning.
- An integrated balance sheet or cash-flow statement.
- Debt or valuation.
- Machine learning.
- Monte Carlo simulation.
- SQL or a database.
- Tableau.
- A custom application.
- Enterprise planning architecture.
- Automated narrative generation.
- Dozens of scenarios.
- A large codebase.
