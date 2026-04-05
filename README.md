# SA Retail Credit Scorecard — Excel Model

A rules-based retail credit scorecard built to reflect the decisioning 
logic used by South African banks under the National Credit Act. 
Scores 30 applicants across six weighted risk factors and produces 
automated lending decisions with reason flags and portfolio analytics.

---

## Why this project exists

Credit risk is the core function of retail banking. Every personal loan, 
home loan, and vehicle finance application in South Africa passes through 
a scorecard before a decision is made. This project models that process 
from first principles: income verification, bureau data, affordability 
assessment, and hard-decline policy rules — all within a single, 
audit-transparent Excel workbook.

---

## Business problem

A retail bank receives loan applications from borrowers across different 
income levels, employment types, and credit profiles. The bank must:

- Assess each applicant's ability to repay without becoming over-indebted
- Apply consistent, defensible lending criteria that comply with the NCA
- Flag high-risk applications for manual review before a final decision
- Produce portfolio-level analytics for the credit risk committee

This model addresses all four requirements.

---

## Approach

**Six scoring factors, one decision engine**

| Factor | Weight | Rationale |
|---|---|---|
| ITC Bureau Score | 25 pts | TransUnion/Experian SA range 330–850 |
| Debt-to-Income Ratio | 20 pts | NCR guideline: max 35–40% for unsecured |
| Affordability Surplus | 20 pts | Post-obligation net surplus per NCA S81 |
| Employment Status | 15 pts | Income certainty; payslip or 2-yr financials |
| Missed Payments (12 mths) | 10 pts | Bureau payment profile |
| Tenure in Current Role | 10 pts | Income continuity proxy |
| **Total** | **100 pts** | |

**Decision thresholds**

- Score ≥ 68: Approve
- Score 42–67: Review (refer to underwriter)
- Score < 42: Decline
- Policy override: Hard decline regardless of score for any of — unemployed, 3+ missed payments, or negative affordability surplus

**Assumptions sheet as single source of truth**

All rate assumptions (SARB prime 11.75% + bank margin 2.00% = 13.75% p.a.), 
policy thresholds, and score cut-offs live in one tab. Change a variable 
once and the model updates everywhere — the same principle used in 
production credit models.

---

## Key features

- Automated scoring and decision output for 30 applicants
- Policy override logic that mirrors real bank hard-decline rules
- Risk driver flags identifying the primary cause of each adverse decision
- Cross-sheet formula architecture with full audit trail
- Dashboard Data tab pre-structured for Power BI or chart integration
- In-workbook documentation covering NCA regulatory context
- Monthly PMT calculation using SARB prime + margin (correct as at Nov 2024)

---

## Example decision logic

**Applicant SA-2025-007**

- Unemployed: Employment Score = 0/15
- Credit Score 538: CS Score = 0/25
- Affordability Surplus: –R6,667 (negative): Surplus Score = 0/20
- 4 missed payments: Missed Payment Score = 0/10
- Total Score: 21/100
- Risk Band: High Risk
- Policy Check: POLICY DECLINE (unemployed + negative surplus + 3+ missed payments)
- Final Decision: **Decline**

All three policy override triggers are breached simultaneously. 
The hard-decline fires before the score band is even consulted.

---

## Tools used

- Microsoft Excel (formula logic, cross-sheet referencing, conditional formatting)
- TransUnion / Experian SA bureau score range (330–850)
- SARB MPC rate (Nov 2024 basis)
- National Credit Act 34 of 2005 (NCA) regulatory framework
- NCR Affordability Guidelines

---

## Why this matters in banking and credit risk

South African retail credit decisions are governed by the NCA. 
Reckless lending is a legal liability — banks must demonstrate that 
affordability was assessed, that the borrower was not over-indebted, 
and that bureau data was considered. This model embeds those legal 
requirements into a working decision engine, not just a slide deck.

The architecture — centralised assumptions, formula-driven outputs, 
reason flags, policy overrides — mirrors the structure of production 
scorecards used at banks like FirstRand, Standard Bank, and Absa.

---

## Limitations and next steps

This is a rules-based, judgemental scorecard. Production scorecards 
derive weights from logistic regression on historical default data. 
Planned improvements:

- Scenario stress-testing (rate shock: +200bps, +300bps)
- Power BI dashboard connecting to the Dashboard Data tab
- Behavioural scoring layer (payment history trends, not just 12-month count)
- Product segmentation (unsecured personal loan vs home loan vs vehicle finance)
- Python rebuild with sklearn LogisticRegression to derive statistical weights

---

## Author

Siphesihle Gwebu | Junior Management Accountant | Johannesburg, South Africa  
BCom Accounting, University of the Free State  
CIMA (in progress) | CFA Level 1 (planned)

[LinkedIn](https://www.linkedin.com/in/yourprofile) | 
[GitHub](https://github.com/yourusername)
