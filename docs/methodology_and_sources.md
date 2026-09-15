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

The fictional 2026 approved assumption pack was fixed before 2026 actual results were available, using planning assumptions and the historical information available at that time. Complete 2025 actuals are separately supplied for the later analyst review; completed December 2025 actuals were not available when the pack was fixed. Limited authoring calculations confirmed that the driver pack produced a coherent, positive property operating contribution; the public budget was subsequently calculated in Phase 2 from the frozen assumptions.

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

## Phase 4 reforecast and scenario methodology

`2026 RF1` uses case version `v1.0` and the July 8, 2026 information cutoff. January–June is an immutable actual period sourced from `Data`; July–December is a forecast period driven by a separate visible RF1 layer on `Assumptions`. The approved-budget assumption table remains frozen and continues to drive only `Budget`.

The Base case is the official working reforecast. It preserves approved monthly seasonality while reflecting first-half retail/leisure weakness, a supportable partial recovery, and continued but limited negotiated-corporate support documented in the dated case updates. Retail and Corporate ADR are forecast independently. Inputs without better evidence remain tied to the approved Budget; analyst judgment is explicitly labeled and is not calibrated backward to a contribution target.

The April housekeeping wage increase is treated as structural, with a loaded wage of $23.25 per hour throughout July–December. Base housekeeping hours per occupied room normalize gradually to the approved path by October; Upside normalizes faster and Downside more slowly. Guest-service unit cost, the 4% distribution fee, fixed staffing, rent, property overhead, and marketing treatment are held constant across scenarios.

The documented June marketing deferral is treated as timing: $18,000 is included in September and is not double counted. Full-year marketing is $167,600 because the other recorded first-half months are $600 above their approved total. The unconfirmed May property-overhead item is not treated as recurring; July–December retains the approved baseline while the uncertainty remains documented for later review.

Upside and Downside change only five H2 drivers: occupied room nights, corporate share, Retail ADR, Corporate ADR, and housekeeping hours per occupied room. They use the same January–June actuals as Base and do not apply blanket income-statement shocks. They are unweighted decision-support sensitivities, not separately approved plans or confidence intervals.

For each case, forecast segment nights equal total occupied room nights allocated by corporate share; segment revenue equals segment nights times segment ADR; variable costs follow the relevant volume and rate drivers; and fixed costs reference visible monthly assumptions. FY2026 equals January–June recorded actual plus July–December forecast. Annual occupancy, mix, ADR, RevPAR, productivity, effective rates, unit costs, and margin use aggregate annual numerators and denominators.

The full-year summary compares approved Budget, Base, Upside, and Downside, while the detailed blocks retain explicit `A` and `F` period labels. Base is expanded and Upside/Downside detail is grouped for collapse. `Checks` retains all 88 prior controls and adds 58 Phase 4 controls; its 146-control master status remains terminal. `Variance` is preserved unchanged and `Review` remains status-only pending Phase 5.

RF1 forecast accuracy cannot be evaluated until later actual results exist. Phase 3 actual-versus-budget analysis is the available evidence about approved-plan performance; no artificial future actuals were created. Phase 4 validation covers independent scenario reconstruction, formula and package integrity, visual inspection, and restored disposable sensitivity tests, but excludes management conclusions, recommendations, charts, PDF/image exports, and final packaging.

## Phase 5 management-review and output methodology

Phase 5 converts the validated analysis into a two-page management decision document without creating new business logic. Key values on `Review` link directly to the existing H1 scorecard and contribution bridge on `Variance`, the approved FY2026 results on `Budget`, and the scenario summary and monthly Base path on `Forecast`. Chart helper ranges sit outside the print area and remain formula-linked and visible for inspection. No `Review` formula references `Checks`, and no output feeds a model calculation.

Page 1 reports H1 occupancy, room revenue, property operating contribution, and contribution margin against the approved budget. It presents the existing contribution impacts using the model’s established convention: positive impact is favorable, revenue effects enter unchanged, and expense effects are reversed. The supporting driver table keeps demand, customer mix, ADR, housekeeping productivity, wage, and guest-service unit cost visible beside the management interpretation.

Page 2 reports the FY2026 Budget, Base, Upside, and Downside cases and marks the June actual / July forecast boundary explicitly in the monthly occupancy view. Management implications distinguish observed first-half results, dated case evidence, and forecast judgment. The marketing deferral remains timing rather than a structural saving; the unconfirmed overhead item remains a follow-up rather than an annualized assumption. The page includes four follow-ups with an owner, timing, and expected evidence.

The three charts are intentionally limited to decision-useful comparisons: H1 contribution impact by driver, monthly occupancy, and full-year contribution by case. A standard impact bar is used instead of a native waterfall because it survives the controlled Excel export reliably; the adjacent formula-linked table supplies the exact bridge start, end, direction, and reconciliation.

The PDF is exported directly from `Review` using a fixed `B1:N96` print area, landscape letter orientation, one page wide, two pages tall, and a manual break before the RF1 outlook page. The two public PNG files are rasterized from the final PDF pages, so the workbook, PDF, and preview images present the same management content.

`Checks` remains terminal and expands from 146 to 179 passing controls. Phase 5 controls cover displayed KPI ties, bridge reconciliation, scenario and chart-source links, the actual/forecast boundary, management-language constraints, page setup, artifact count, and package integrity.

## Phase 6 independent audit and release validation

Phase 6 independently reconstructed the material model results outside Excel using only the frozen CSVs and the documented methodology. The work covered all 12 approved-budget months and FY2026, H1 2026 actuals and matched budget, H1 2025 comparison, every monthly and YTD revenue and cost attribution, the full contribution bridge, and each monthly Base, Upside, and Downside RF1 case. The maximum differences against workbook results were `$0.0000000005` for money, `0.0000000000003333` for ratios, and `0.000000000003` for nights and hours. These are within tolerances of `$0.01`, `1e-7`, and `1e-6`.

The workbook was also opened, fully recalculated, saved, closed, and reopened in native Excel. All eight sheets remained visible in the locked order, `Start` remained the opening sheet, the three charts and `Review` print area remained intact, and `Checks` returned exactly `179 / 179 PASS` with master status `PASS`. Upside and Downside detail on `Forecast` is grouped and collapsed by default.

Package review found and removed one absolute local-path record and replaced an internal authoring-theme label with `Palmetto Stay`. Workbook author and last-modified metadata are `Owen Chapman`. The final package has no macros, external links, hidden sheets, circular iteration, volatile formulas, connections, Power Query, pivots, data model, broken relationships, or unintended media. No formula outside `Checks` references `Checks`.

`outputs/Palmetto_Stay_Management_Review.pdf` remains the workbook’s direct two-page landscape `Review` export. Fresh 200-DPI rendering reproduced `outputs/management_review_page_1.png` and `outputs/management_review_page_2.png` exactly; both PNGs are 2200 × 1700. Phase 6 required no change to financial logic, frozen sources, assumptions, `Review`, the PDF, or the PNGs.

This validation is limited to the project’s stated scope. It is an independent portfolio-model reconstruction and adversarial review, not third-party assurance or an accounting audit opinion.

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
- Base, Upside, and Downside are judgment-based decision cases, not probabilities or confidence intervals.
- No forecast-accuracy claim because no frozen forecast vintage and subsequent unseen actuals exist.
- The project does not represent employment by or advice to a real company.

## References for definitions and modeling practice

- CoStar/STR, “Hotel Industry Terms to Know”: https://www.costar.com/products/str-benchmark/resources/glossary
- ICAEW, “Twenty principles for good spreadsheet practice,” 2024 edition: https://www.icaew.com/technical/technology/excel-community/20-principles-for-good-spreadsheet-practice-2024-edition
- FAST Standard Organisation, FAST Standard: https://fast-standard.org/

These references support selected terminology and modeling discipline. They do not supply Palmetto Stay's synthetic numerical assumptions.
