# EquiReward: Bonus Fairness Guardrail (MVP)

## Background

Managers often find it difficult to fully exclude systemic and non-systemic bias when allocating bonuses, and they are frequently unaware of their own bias. EquiReward is a prototype that adds a fairness guardrail to the bonus proposal process.

## What it does

1. **Calculates a fair incentive range** for each employee based on their level and performance rating.
2. **Validates each proposal:**
   - Within the band: the proposal passes.
   - Up to 10% outside the band: a written reason is required.
   - More than 10% outside the band: the proposal is escalated, and an email notice is sent to HR to create a traceable record.
3. **Produces an audit dashboard** in Power BI that summarises bonus totals and averages by team, level and performance rating.

## Components

| Component | Platform | Purpose |
|---|---|---|
| Proposal form and validation | Power Apps (canvas app) | Captures proposals and applies band checks |
| Data storage | SharePoint Lists | Employees (`equireward`), pay bands (`BandTable`), proposals (`BonusProposal`) |
| Escalation notice | Power Automate | Sends an email when a proposal is escalated |
| Audit dashboard | Power BI | Semantic model, bar charts, matrix, and a bonus-to-annual-salary consistency check |

## Data

All data in this project is **synthetic**. The employee dataset (1,470 rows) is based on the public IBM HR Analytics Employee Attrition dataset, extended with team, level, performance and bonus fields. Band values are placeholders pending HR confirmation, particularly for level L5. No real employee data is included.

## Files

- `EquiReward_solution.zip`: Power Platform solution containing the canvas app and the cloud flow.
- `equireward_hr_augmented_full.csv`: Employee dataset (synthetic, 1,470 rows).
- `equireward_band_table_v2.csv`: Pay band table (placeholder values).
- `equireward_bonus_history_mock.csv`: Mock bonus history (43 rows).

## How to import

1. In Power Apps, go to **Solutions** → **Import solution**, and select `EquiReward_solution.zip`.
2. Create the SharePoint lists `equireward`, `BandTable` and `BonusProposal`, then import the CSV files into them.
3. Update the connections in the imported app and flow to point to your own SharePoint site and Outlook account.
4. Open the app and test a proposal.

## Limitations

- Band values are placeholders and need HR confirmation.
- The escalation step currently sends an email and saves the proposal. It does not block or require approval.
- Gender analysis is not included. Any such analysis requires field-level permissions and legal or compliance review first.
- Power Apps and Power Automate authentication is not configured for public access.

## Next steps

- Confirm pay bands with HR using real salary data (with authorisation).
- Add an approval workflow and role-based access control.
- Automate the bonus-to-salary consistency check.
