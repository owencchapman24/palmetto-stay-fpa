# Palmetto Stay Synthetic Case Methodology and Sources

## Purpose and classification

Phase 1 creates a controlled synthetic source package for a fictional 100-room limited-service hotel. The package is designed to support later budgeting, variance analysis, driver-based reforecasting, scenarios, and management reporting without implying access to confidential company information.

All Palmetto Stay numerical data, operating records, staffing information, and management updates are synthetic. The external references at the end of this document inform selected definitions and spreadsheet-modeling practices only. They are not sources for the numerical assumptions.

## Deterministic construction method

The private Case Builder uses fixed, nonvolatile Excel inputs and ordinary formulas. It does not use `RAND()`, `RANDBETWEEN()`, macros, circular references, hidden sheets, external workbook links, Solver, optimization, or machine learning.

The construction sequence is:

1. Set room capacity, monthly seasonality, baseline demand, and fixed month-specific variation.
2. Apply dated retail/leisure demand and negotiated corporate support effects.
3. Calculate total occupied room nights and split them between the two customer segments.
4. Apply segment-specific ADR inputs and fixed monthly rate variation to generate recorded segment revenue.
5. Apply independent actual housekeeping productivity and wage schedules to generate recorded hours and payroll.
6. Apply guest-service unit construction rates, aggregate fixed staffing, rent, property overhead, and marketing service timing.
7. Calculate distribution/payment expense as exactly 4% of recognized room revenue.
8. Export the resulting recorded facts as static public CSV values.

The 2026 approved assumption pack was constructed from completed 2025 history and documented planning assumptions and is dated before 2026 actual results. Limited authoring calculations confirm that the driver pack produces a coherent, positive property operating contribution, but the public budget itself will be calculated only in Phase 2.

## Actuals-independence rule

Public actuals store source facts rather than reconstructed driver results:

- Operating actuals store occupied room nights and room revenue by segment.
- Labor actuals store housekeeping hours, housekeeping payroll, fixed-staff FTE, and fixed-staff payroll.
- Financial actuals store the required revenue and expense lines.

Actual ADR, housekeeping hours per occupied room, effective housekeeping wage, and guest-service cost per occupied room are not source fields. Later work must derive them from the recorded numerators and denominators. Public source files contain no formulas and do not link to the private Case Builder.

## Phase 2 public workbook implementation

Phase 2 created `model/Palmetto_Stay_FP&A_Model.xlsx` with the final eight-tab public architecture. `Data` stores static typed copies of the financial, operating, labor, and case-update CSVs. `Assumptions` stores the frozen approved assumption pack as the single authoritative source for the 2026 budget. The source tables use real Excel dates and retain every public field and row without external CSV links.

The `Budget` sheet matches each monthly header to `Assumptions` and applies the documented operating relationships. Available room nights equal rooms multiplied by calendar days; occupied nights split into retail/leisure and negotiated corporate nights using the approved mix; segment nights and ADR produce room revenue; and approved productivity, wage, unit-cost, staffing, rent, overhead, marketing, and distribution-fee assumptions produce operating costs. Property operating contribution equals total room revenue less total operating costs.

The FY2026 column sums additive measures. It calculates occupancy, corporate share, blended ADR, RevPAR, housekeeping hours per occupied room, effective housekeeping wage, guest-service unit cost, effective distribution fee rate, and contribution margin from annual numerators and denominators. Monthly operating levels use an appropriate annual average or weighted calculation.

`Checks` remains terminal. It reads source and Budget results but does not feed model calculations or displayed statuses elsewhere. `Start` contains only a static instruction to inspect `Checks`; it has no formula dependency on the check result. `Forecast` and `Review` remain status-only sheets until their authorized phases.

## Phase 3 actual-performance and variance methodology

Phase 3 uses January–June 2026 recorded actuals, the matching six months of the approved 2026 Budget, and January–June 2025 recorded actuals. The analysis cutoff is July 8, 2026. `Variance` retrieves recorded amounts from `Data` and approved-budget amounts from `Budget`; it does not copy or independently hardcode budget outputs.

Actual segment ADR equals recorded segment revenue divided by recorded segment nights. Blended ADR, RevPAR, corporate share, housekeeping hours per occupied room, effective housekeeping wage, guest-service cost per occupied room, fixed-staff cost per FTE-month, distribution rate, and contribution margin are derived from recorded numerators and denominators. YTD ratios use aggregate YTD numerators and denominators rather than averages of monthly ratios.

The revenue bridge applies volume, then customer mix, then rate. The housekeeping bridge applies volume, then efficiency, then wage rate. These are sequential attribution conventions: interaction effects follow the documented order, which is consistent and fully reconciling but is not asserted to be the only possible causal allocation. Guest-service expense separates occupied-room volume from unit cost, and fixed-staff payroll separates FTE from cost per FTE. Each driver bridge is calculated monthly, summed to YTD, and compared with the recorded actual-minus-budget variance.

Underlying expense schedules use actual cost minus budget cost, where positive is unfavorable. The contribution bridge reverses those expense effects so positive contribution impact is favorable; revenue effects enter unchanged. Distribution/payment expense remains fixed at 4% of recognized room revenue, so its cost change is mechanically tied to the revenue variance and has no independent rate explanation. Rent, property overhead, and marketing are presented as direct cost changes.

The commentary register is evidence-controlled. It records the period, observed result, calculated financial impact, operating driver, dated case-update reference, confidence, classification, qualitative Phase 4 implication, and required follow-up. A materiality flag or management observation is not treated as proof of causation, and no forecast assumption is created in Phase 3.

`Checks` retains the 41 Phase 2 controls and appends 47 Phase 3 controls for source-period and key completeness, actual reconstruction, budget linkage, YTD aggregation, bridge residuals, contribution signs, and workbook architecture. All checks are terminal: no other worksheet references `Checks`. `Start` provides a static inspection instruction, while `Forecast` and `Review` remain status-only and contain no Phase 4 output.

## Public source files and fields

### `approved_budget_assumptions.csv`

| Field | Definition |
| --- | --- |
| `case_version` | Frozen source version. |
| `period` | First day of the budget month. |
| `rooms_available` | Physical room capacity. |
| `total_occupied_room_nights` | Approved occupied-room-night assumption. |
| `corporate_share` | Negotiated Corporate share of occupied room nights. |
| `retail_adr` | Approved Retail/Leisure ADR. |
| `corporate_adr` | Approved Negotiated Corporate ADR. |
| `housekeeping_hours_per_occupied_room` | Approved housekeeping productivity assumption. |
| `housekeeping_loaded_wage_per_hour` | Approved loaded housekeeping wage. |
| `guest_service_cost_per_occupied_room` | Approved activity-linked guest-service unit cost. |
| `distribution_fee_rate` | Fixed distribution/payment rate of 0.04. |
| `fixed_staff_fte` | Approved aggregate fixed-staff FTE. |
| `fixed_staff_loaded_cost_per_fte` | Approved monthly loaded cost per fixed-staff FTE. |
| `rent` | Monthly rent assumption in USD. |
| `property_overhead` | Monthly property-overhead assumption in USD. |
| `marketing` | Monthly marketing service assumption in USD. |

### `operating_actuals.csv`

| Field | Definition |
| --- | --- |
| `case_version` | Frozen source version. |
| `period` | First day of the recorded month. |
| `segment` | Retail/Leisure or Negotiated Corporate customer segment. |
| `occupied_room_nights` | Recorded occupied room nights for the segment. |
| `room_revenue` | Recorded recognized room revenue for the segment in USD. |

### `labor_actuals.csv`

| Field | Definition |
| --- | --- |
| `case_version` | Frozen source version. |
| `period` | First day of the recorded month. |
| `housekeeping_hours` | Recorded housekeeping labor hours. |
| `housekeeping_payroll` | Recorded loaded housekeeping payroll in USD. |
| `fixed_staff_fte` | Recorded aggregate fixed-staff FTE. |
| `fixed_staff_payroll` | Recorded aggregate fixed-staff payroll in USD. |

### `financial_actuals.csv`

| Field | Definition |
| --- | --- |
| `case_version` | Frozen source version. |
| `period` | First day of the recorded month. |
| `account_code` | Stable four-digit account identifier. |
| `account_name` | Required financial-line name. |
| `amount_usd` | Positive recorded revenue or expense amount in USD. |

The file contains Room Revenue, Housekeeping Payroll, Guest Services, Distribution and Payment, Fixed Staff Payroll, Rent, Property Overhead, and Marketing once for every actual month. Property operating contribution is derived and is not a source line.

### `case_updates.csv`

| Field | Definition |
| --- | --- |
| `update_id` | Stable unique update identifier. |
| `as_of_date` | Date the observation was available. |
| `effective_start` | Start of the affected period. |
| `effective_end` | End of the affected period. |
| `category` | Demand, mix, labor, marketing, overhead, or outlook classification. |
| `observation` | Available fact or management observation. |
| `evidence_status` | Confirmed, Management Estimate, or Unconfirmed. |
| `forecast_relevance` | How the evidence should be considered in later forecast assumptions. |

## Sign, date, and unit conventions

- CSV files are UTF-8 and comma-delimited with one header row and no blank rows.
- Monthly periods use ISO `YYYY-MM-DD` dates and the first day of each month.
- Room nights and FTE are quantities. ADR and unit costs are USD per stated unit.
- Revenue, payroll, and expense source amounts are positive USD values without currency symbols or thousands separators.
- Percentages are stored as decimals, such as `0.04` for 4%.
- Customer share is between 0 and 1.
- Actual cost change is later defined as actual cost minus budget cost; positive is unfavorable.
- Contribution impact from a cost is the negative of actual cost minus budget cost; positive is favorable.
- Revenue effects enter the contribution bridge without reversal.

## Case version and freeze

- Case version: `v1.0`
- Freeze date: 2026-09-11
- Forecast information cutoff: 2026-07-08
- Actual coverage: 2025-01-01 through 2026-06-01
- Approved assumption coverage: 2026-01-01 through 2026-12-01

The private Case Builder is retained outside the public repository so the case can be regenerated. The public CSVs are frozen static values and have no workbook links.

## Validation and regeneration protocol

The Case Builder contains terminal checks for capacity, segment totals, revenue reconciliation, labor/payroll reconciliation, fixed-payroll reconciliation, the 4% distribution-fee policy, required periods, unique keys, missing values, nonnegative values, case-event timing, and output row counts. Those checks do not feed generated business values.

Public CSVs must also be parsed and reconciled independently of the Case Builder before a version is frozen. A valid freeze requires:

- Exactly 12 budget-assumption rows, 36 operating rows, 18 labor rows, and 144 financial rows.
- Complete monthly coverage and unique required keys.
- Exact segment-to-financial revenue, labor-to-financial payroll, and fixed-payroll reconciliations.
- Distribution/payment expense equal to exactly 4% of recorded room revenue at stored precision.
- No capacity breach, impossible share, negative source amount, blank required value, or formula.

Do not hand-patch public actuals to force a reconciliation. If a source-data defect is found, correct the deterministic private Case Builder, regenerate every affected public table, repeat workbook and independent validations, assign a new case version, and document the change in the decision log. A correction to a later workbook formula does not require changing valid frozen source data.

## Known simplifications

- One independently operated, leased property with 100 rooms.
- Two customer segments and no booking-channel analysis.
- Monthly rather than daily source data.
- Room revenue only; no restaurants, events, bars, spas, or other ancillary operations.
- Aggregate fixed staffing rather than employee-level planning.
- No integrated balance sheet, cash-flow statement, debt, valuation, depreciation, tax, or corporate overhead.
- A fixed 4% distribution/payment rate with no fee-rate scenario.
- No forecast-accuracy claim because no frozen forecast vintage and subsequent unseen actuals exist.

## References for definitions and modeling practice

- CoStar/STR, “Hotel Industry Terms to Know”: https://www.costar.com/products/str-benchmark/resources/glossary
- ICAEW, “Twenty principles for good spreadsheet practice,” 2024 edition: https://www.icaew.com/technical/technology/excel-community/20-principles-for-good-spreadsheet-practice-2024-edition
- FAST Standard Organisation, FAST Standard: https://fast-standard.org/

These references support selected terminology and modeling discipline. They do not supply Palmetto Stay's synthetic numerical assumptions.
