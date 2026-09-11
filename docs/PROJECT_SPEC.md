# Palmetto Stay FP&A Project Specification — Blueprint v1.3

- **Status:** Locked
- **Date:** 2026-09-11
- **Implementation status:** Phase 5 complete; Phase 6 independent audit pending

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
- January–December 2026 approved budget assumptions are supplied independently in `data/approved_budget_assumptions.csv`; the budget itself is calculated in Phase 2.
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

The frozen `data/approved_budget_assumptions.csv` file is the source input for the Budget tab. It contains approved operating and cost drivers only. The Phase 2 Budget tab calculates financial outputs from those assumptions and does not treat a precomputed budget as source data.

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

### 12.1 Phase 2 implementation

- The public workbook is `model/Palmetto_Stay_FP&A_Model.xlsx` and contains the eight required visible tabs in the locked order.
- `Data` holds static, typed imports of `financial_actuals.csv`, `operating_actuals.csv`, `labor_actuals.csv`, and `case_updates.csv`. It does not calculate actual KPIs or variances.
- `Assumptions` holds `approved_budget_assumptions.csv` as the single authoritative input for the approved 2026 budget.
- `Budget` matches each monthly header to the approved source and calculates capacity, segment room nights, segment revenue, hotel KPIs, operating costs, property operating contribution, and contribution margin through ordinary formulas.
- The distribution and payment calculation references the monthly approved fee assumption rather than hardcoding 4% in an operating formula.
- The FY2026 column sums additive measures. Occupancy, corporate share, ADR, RevPAR, housekeeping productivity, effective wage, guest-service unit cost, effective distribution fee rate, and contribution margin use annual numerators and denominators. Monthly operating levels use an appropriate average or weighted annual presentation.
- `Checks` is terminal. It reads source and Budget results, contains the master Phase 2 status, and does not feed any other worksheet.
- `Start` contains a static instruction to inspect `Checks`. It does not display or reference the master check result. This controlled correction replaces the proposed Start-to-Checks dependency and preserves the rule that checks validate the model without driving model outputs.
- `Forecast` and `Review` contain status notices only. Their calculations and management content remain reserved for later phases.

### 12.2 Phase 3 implementation

- `Variance` analyzes January–June 2026 recorded actuals against the matched January–June 2026 approved budget and January–June 2025 recorded actuals. The information cutoff is July 8, 2026.
- Actual room nights, segment revenue, housekeeping hours and payroll, guest-service expense, distribution/payment expense, fixed-staff FTE and payroll, rent, property overhead, and marketing link to the frozen `Data` facts. Actual ADR, RevPAR, mix, productivity, effective wage, unit cost, contribution, and margin are derived from recorded numerators and denominators rather than budget assumptions.
- The sheet presents a YTD scorecard and three vertically stacked monthly blocks for approved budget, recorded actual, and actual minus budget. Additive YTD measures sum monthly amounts; YTD ratios use aggregate numerators and denominators.
- Revenue is attributed in the locked sequence of volume, customer mix, and rate. Housekeeping is attributed in the locked sequence of volume, efficiency, and wage rate. Guest service separates volume and unit-cost effects; fixed-staff payroll separates FTE and rate effects. Each bridge is shown monthly and YTD and reconciles to its reported variance.
- Distribution/payment expense remains mechanically linked to 4% of recorded revenue. Rent, property overhead, and marketing are shown as direct cost changes. The property operating contribution bridge reverses expense cost changes and reconciles budget contribution to recorded actual contribution.
- The evidence-controlled commentary register includes only meaningful results and supplied case events. It identifies period, observed result, financial impact, operating driver, dated evidence, confidence, classification, qualitative Phase 4 implication, and follow-up while distinguishing observation from causal interpretation.
- `Checks` retains the 41 Phase 2 controls and adds 47 Phase 3 controls for period and key completeness, actual reconstruction, budget linkage, ratio aggregation, bridge integrity, contribution signs, and workbook architecture. The 88-control master status remains terminal on `Checks`, and no other sheet depends on it.
- `Forecast` and `Review` remain status-only. Phase 3 adds no reforecast, scenarios, management recommendations, charts, PDF, or portfolio images.

### 12.3 Phase 4 implementation

- `2026 RF1` uses case version `v1.0`, the July 8, 2026 information cutoff, January–June recorded actuals, and a July–December driver-based forecast. Base is the official working reforecast; Upside and Downside are bounded, unweighted sensitivities.
- `Assumptions` preserves the approved-budget table unchanged and adds a visibly separate RF1 layer. Base inputs show monthly operating drivers with basis, source, and rationale. Scenario changes are limited to occupied room nights, corporate share, Retail ADR, Corporate ADR, and housekeeping hours per occupied room.
- Base preserves approved seasonality while allowing partial retail/leisure recovery and continued but limited corporate support. Segment ADRs are forecast independently. The April housekeeping wage increase remains structural, temporary productivity disruption normalizes over a documented path, deferred June marketing is recognized in September, and the unconfirmed May overhead item is not annualized.
- `Forecast` contains a compact full-year summary and three vertically stacked twelve-month blocks. January–June in every case links to the authoritative Base actual section; July–December references visible scenario assumptions. FY2026 equals H1 recorded actual plus H2 forecast, and annual ratios use aggregate numerators and denominators.
- Base is expanded by default. Upside and Downside detail is grouped for collapse. Actual and forecast months have explicit `A` and `F` labels, and each scenario compares with the approved FY2026 Budget.
- `Checks` retains all 88 Phase 2–3 controls and adds 58 Phase 4 controls for forecast boundaries, actualization, assumptions, known updates, financial mechanics, scenario ordering, and architecture. The combined 146-control master status remains terminal on `Checks`; no other worksheet depends on it.
- `Variance` remains the complete Phase 3 analysis and `Review` remains status-only. Phase 4 adds no management recommendations, charts, PDF, images, or final packaging.
- RF1 accuracy cannot be evaluated until later actual results exist. The three scenarios are decision-support cases, not confidence intervals, and are not probability weighted.

### 12.4 Phase 5 implementation

- `Review` is complete as a two-page management-facing worksheet and is the direct source for the exported PDF. Page 1 summarizes H1 actual performance against the approved budget, management interpretation, supporting operating drivers, and the reconciled contribution bridge. Page 2 summarizes the FY2026 Base outlook, the Budget/Base/Upside/Downside range, risks, opportunities, and four owned follow-ups.
- Key displayed results and all three chart source ranges are formula-linked to `Variance`, `Budget`, or `Forecast`. No `Review` formula references `Checks`, and no management output drives model calculations.
- The three authorized charts are an H1 contribution-impact view, a monthly occupancy view with an explicit June actual / July forecast boundary, and a full-year contribution comparison.
- The approved Budget, Phase 3 Variance analysis, Phase 4 Forecast logic, and the frozen approved-assumption range remain unchanged.
- `Checks` retains the 146 prior controls and adds 33 Phase 5 controls covering displayed KPI ties, bridge and scenario links, chart sources, output architecture, management-language boundaries, and the PDF/image package. The combined 179-control master status remains terminal.
- The workbook opens on `Start`, contains exactly eight visible sheets, and has no macros, external workbook links, hidden sheets, circular iteration, or volatile formulas.
- The public output package contains one two-page landscape PDF exported directly from `Review` and two PNG previews rendered from the final PDF pages.

## 13. Management output

The completed `Review` tab and exported PDF contain exactly two landscape pages.

### Page 1

- H1 actual performance.
- Revenue and contribution versus budget.
- Occupancy, ADR, and RevPAR.
- Contribution bridge.
- Concise, evidence-bounded management explanations.
- Timing-versus-ongoing classification.

### Page 2

- Full-year budget versus latest estimate.
- Base/Upside/Downside comparison.
- Monthly actual-versus-forecast trend.
- Material risks and opportunities.
- Four recommended follow-ups with owners, timing, and expected evidence.

The management output is limited to three charts and approximately 350–500 words. It is a compact decision document rather than a decorative dashboard, and no separate slide deck is included.

## 14. Synthetic case construction

The private Case Builder must:

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

- The initial case version `v1.0` was frozen on 2026-09-11 with a forecast information cutoff of 2026-07-08.
- Actuals must not be hand-patched to make analysis reconcile.
- Source-data errors must be corrected through the private Case Builder.
- Source changes require a new case version, revalidation, and documentation.
- Workbook-formula corrections do not require changing valid frozen source data.

### 15.1 Frozen source interface

All public Phase 1 CSVs are UTF-8, comma-delimited static values with one header row, ISO monthly period keys represented by the first day of each month, no formulas, and no blank records.

- `approved_budget_assumptions.csv`: 12 rows for January–December 2026. Fields are `case_version`, `period`, `rooms_available`, `total_occupied_room_nights`, `corporate_share`, `retail_adr`, `corporate_adr`, `housekeeping_hours_per_occupied_room`, `housekeeping_loaded_wage_per_hour`, `guest_service_cost_per_occupied_room`, `distribution_fee_rate`, `fixed_staff_fte`, `fixed_staff_loaded_cost_per_fte`, `rent`, `property_overhead`, and `marketing`.
- `operating_actuals.csv`: 36 rows covering 18 months and two customer segments. Fields are `case_version`, `period`, `segment`, `occupied_room_nights`, and `room_revenue`.
- `labor_actuals.csv`: 18 monthly rows. Fields are `case_version`, `period`, `housekeeping_hours`, `housekeeping_payroll`, `fixed_staff_fte`, and `fixed_staff_payroll`.
- `financial_actuals.csv`: 144 rows covering eight required accounts for each actual month. Fields are `case_version`, `period`, `account_code`, `account_name`, and `amount_usd`.
- `case_updates.csv`: dated observations with fields `update_id`, `as_of_date`, `effective_start`, `effective_end`, `category`, `observation`, `evidence_status`, and `forecast_relevance`.

The four versioned source files use `case_version = v1.0`. Actual ADR, effective housekeeping wage, housekeeping hours per occupied room, and guest-service cost per occupied room must remain derived measures and must not be added to the public actual-source schemas.

## 16. Planned final repository structure

This is the planned final structure. Directories and deliverables must be created only in their authorized implementation phase; currently empty directories must not be created early.

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
└── outputs/
    ├── Palmetto_Stay_Management_Review.pdf
    ├── management_review_page_1.png
    └── management_review_page_2.png
```

The private `Palmetto_Stay_Case_Builder_AUTHORING.xlsx` is intentionally excluded from this public structure.

## 17. Phase plan and effort control

- **Phase 0 — Repository foundation and project governance.**
- **Phase 1 — Synthetic case construction, validation, and freeze.**
- **Phase 2 — Workbook architecture and frozen annual budget.**
- **Phase 3 — Actuals, KPIs, and variance analysis.**
- **Phase 4 — Reforecast and scenarios (complete).**
- **Phase 5 — Management output and repository packaging (complete).**
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
