# Palmetto Stay Analyst Case Brief

## Assignment

You are a junior FP&A analyst supporting the property finance manager for Palmetto Stay. Prepare for the June 2026 close and first-half operating review, then support a revised July–December outlook and a concise two-page management review in later project phases.

The information cutoff for this assignment is **July 8, 2026**. Do not use information dated after that cutoff when developing the outlook.

## Business description

Palmetto Stay is a fictional, independently operated, leased limited-service hotel with 100 available rooms. The property models room revenue only. Restaurants, events, bars, spas, and other ancillary revenue streams are outside the assignment.

## Available source files

| File | Information supplied |
| --- | --- |
| `data/approved_budget_assumptions.csv` | Approved monthly operating and cost assumptions for January–December 2026. |
| `data/operating_actuals.csv` | Recorded occupied room nights and room revenue by customer segment for January 2025–June 2026. |
| `data/labor_actuals.csv` | Recorded housekeeping hours and payroll plus aggregate fixed-staff FTE and payroll for January 2025–June 2026. |
| `data/financial_actuals.csv` | Recorded monthly financial lines for January 2025–June 2026. |
| `data/case_updates.csv` | Dated management and operating observations available through the information cutoff. |

All source files belong to frozen case version `v1.0`. Monthly periods use the first day of the month as the period key.

## Customer segments

- **Retail/Leisure:** transient guests purchasing for leisure or other non-negotiated stays.
- **Negotiated Corporate:** transient guests using an agreed corporate rate.

These are customer segments, not booking channels. Negotiated corporate demand must not be treated as guaranteed room blocks.

## Financial lines

| Account | Definition |
| --- | --- |
| Room Revenue | Recognized room revenue after discounts reflected in realized ADR and before separately presented distribution/payment expense. |
| Housekeeping Payroll | Loaded payroll cost for housekeeping labor. |
| Guest Services | Activity-linked guest-service operating expense. |
| Distribution and Payment | A fixed 4% of recognized room revenue. |
| Fixed Staff Payroll | Aggregate loaded payroll for fixed property staffing. |
| Rent | Property lease expense. |
| Property Overhead | Modeled fixed and scheduled property operating costs outside the separately listed lines. |
| Marketing | Marketing services delivered in the period. |

**Property operating contribution** is room revenue less the modeled property operating costs above, including rent, before depreciation, financing, income taxes, and corporate overhead. It is not GAAP operating income, EBITDA, cash flow, or standardized hotel GOP.

Revenue and expense amounts are positive source values. Later cost-change schedules use actual cost minus budget cost, so positive cost changes are unfavorable. Contribution impacts reverse cost changes; revenue effects do not reverse.

## Budget and actuals

The fictional 2026 assumption pack was fixed on December 15, 2025, before any 2026 actual results were available. Complete 2025 historical actuals are separately supplied to the analyst for the later review; completed December 2025 actuals were not available when the pack was fixed. The pack supplies driver assumptions for the future budget calculation; it is not a precomputed budget.

Actuals are recorded source facts. Segment ADR, housekeeping hours per occupied room, effective housekeeping wage, and guest-service cost per occupied room must be derived from recorded nights, revenue, hours, payroll, and expense. Do not reconstruct actuals from budget assumptions.

## Case updates

The dated update file records the following information available by the cutoff:

- Property records show weaker retail/leisure occupied room nights during part of the spring.
- Negotiated corporate transient activity supplied additional room nights during the spring; no guaranteed room blocks exist.
- A loaded housekeeping wage change became effective April 1.
- Property logs record higher housekeeping hours during April and May, and management has provided an estimate about normalization after June.
- A marketing activity scheduled for June was not delivered and was rescheduled for September.
- A modest May property-overhead item remains under vendor-detail review without a confirmed cause.
- Management has documented a current view of partial second-half retail/leisure recovery, subject to summer pickup.

Evidence status means:

- **Confirmed:** supported by recorded activity, an executed decision, or other dated evidence.
- **Management Estimate:** a documented forward-looking management assumption rather than a recorded fact.
- **Unconfirmed:** available information does not establish a definitive cause or treatment.

The updates provide evidence and timing. They do not replace independent analysis or pre-determine a forecast conclusion.

## Questions management wants answered

1. How did June and year-to-date room revenue, operating costs, and property operating contribution compare with the approved budget?
2. How much of the revenue difference relates to occupied-room volume, customer mix, and segment rates?
3. How much of the housekeeping payroll difference relates to volume, labor efficiency, and wage rate?
4. Which cost differences remain after flexing activity-linked expenses for actual occupied room nights?
5. Which observed differences appear timing-related, which may continue, and which require more evidence?
6. What July–December outlook is supported by dated evidence or an explicit management assumption?
7. What risks, opportunities, and follow-up actions should management consider?

## Synthetic-data disclosure

Palmetto Stay is a fictional hotel created for an independent FP&A portfolio project. All company-specific historical results, budgets, actuals, operating records, staffing information, and management updates are synthetic. Public sources may inform selected industry definitions and modeling practices; they are not the source of Palmetto Stay's internal data. The project does not represent employment, client work, or access to confidential company information.

## Known limitations

- Source data are monthly and cover one property and two customer segments.
- No daily booking, booking-channel, customer-level, or employee-level data are supplied.
- No balance sheet, cash-flow statement, debt, valuation, tax, depreciation, or corporate-overhead data are supplied.
- The source package contains 18 months of actual facts and one approved 2026 assumption pack; it does not contain a frozen forecast vintage or subsequent unseen actuals.
- One property-overhead observation remains unconfirmed. Request supporting detail rather than assigning a cause.
- The final workbook, variance analysis, reforecast, scenarios, and management review have not yet been built.
