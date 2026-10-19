# Marketing Management — operational UI proposal

Status: client-review prototype, not a production implementation. Approved screen/layout scope: eight screens; user approval “ok go head with UI updated”, 2026-10-19.

Open `index.html` in a browser. It is a standalone, self-contained proposal suitable for sending as a file; it is not publicly hosted. No real card processing, payroll, ADP export, accounting journal, or employee bank payment occurs.

## Walkthrough

1. OP → Marketing Management: available and reserved credits, funding history, no funding Status column.
2. Add Funding by Credit Card: enter an amount, select **Use test details**, then Pay. Cancel/decline do not add credits. No card, CVC, payer, or postal-code input is persisted.
3. Prepare Payroll → Marketing (after Commission): review leads/conversions and configured unit rates; enter final amounts and optional notes. One shared available-credit balance limits the combined amount.
4. Submit Payroll: freeze a snapshot and reserve the combined Marketing total. Other existing payroll validation remains a handoff, not implemented or bypassed.
5. BC → Review & approve: read-only submitted Marketing amounts; approval retains the reservation.
6. HO → Payroll Summary: COMPANY TOTAL first; Total Labour, Total Job Training, Total Commission; BC/OP details below. Each OP has Labour, Commission, then Marketing. Posting is unavailable before BC approval. Posting consumes reserved credits once, without reducing available credits a second time.
7. OP → Marketing Management Log: combined work/results table and separate Payment Log; employee and role filters.
8. Marketer / Caller → own earnings: work/results and separate own Payment Log. Results-based calculated earnings can differ from OP's final pay.

Use **Preview screen** to move between roles. This is a demo navigator, not a proposed cross-role product permission. **Proposal notes & client confirmations → Reset demo data** restarts the walkthrough.

## Source and design evidence

- Latest user-confirmed rules in this conversation: marketer = leads × rate per lead; caller = conversions × rate per conversion; shared credit limit; reserve on submission, deduct on HO posting.
- HO screenshot: `Screenshot 2026-10-19 at 10.58.10.png`, supplied in this conversation. Its company-total-first hierarchy and header actions are retained.
- Previously approved SIMON mockups: `marketing-funding-stage.html`, `payroll-marketing.html`, `ho-marketing-payroll.html`, `marketing-earnings-log.html` in the thread visualization directory. Visual shell, tab, checkout and tracking relationships are reused; obsolete hourly-pay/direct-card-salary logic is replaced.
- No exact Figma UI frames or local `.agents/figma-design` foundations/components were supplied for this approved proposal. This is a screenshot-based review mockup, not a pixel-verified Figma implementation. No new icon assets were invented.
- Inline editable source: `/Users/macbook/.codex/visualizations/2026/10/05/01a10a35-0996-7bb1-b6f0-f074897a5a94/marketing-management-proposal.html`.

## Traceability

| Requirement | Screen / implementation evidence | Verification |
|---|---|---|
| Funding separate from payroll; reusable credits | Management + credit-card funding | Browser: success adds $500 once; cancel/decline unchanged |
| Results-based suggestions; final manual pay | Payroll Marketing table | Browser: 18 × $20 = $360; 8 × $25 = $200; editable amounts/notes |
| Shared balance limit | Combined total validation | Browser: $650 against $600 blocks submission |
| Reserve on submission | Submitted snapshot / available and reserved credits | Browser: $1,100 balance → $540 available + $560 reserved |
| BC/HO cannot edit | Read-only snapshot tables | Browser: submitted amounts and escaped notes retained |
| BC approval required for demo posting | HO Post Payroll Batch | Browser: disabled before approval; BC retains reservation |
| Deduct only on HO posting | Post transition | Browser: $560 consumed, $540 available, $0 reserved; duplicate post disabled |
| Tracking separate from work records | Three tracking views | Browser: period-level rows only; Paid by is OP, not HO |
| Accounting handoff, no fabricated journals | Proposal notes / posted feedback | Implemented; accounting out of scope |

## Open questions retained for client discussion

1. **Louis:** Confirm employee Payment Log updates on HO posting. Demo uses this trigger; “Total paid” means posted payroll amount, not confirmed bank receipt.
2. **Louis:** Confirm payment tracking only per employee/payroll period, without allocations to individual sessions/dates. Demo separates work-date filters from payment-period filters.
3. **Nat / Maria:** Credit GL/liability, funding and expense journals, reconciliation, burden, ADP mapping and actual payment workflow remain undefined. HO posting hands off to that future process.
4. **Louis:** Final lead/conversion attribution, cutoffs, rate-change and correction rules remain open. Sample data does not define these rules.
5. **Team:** Rejection/withdrawal/correction credit-release rules are not defined and are not simulated.

## Recommended presentation/accessibility choices

The existing SIMON desktop shell is retained, with its established narrow-screen stacking/table scrolling. All product actions use native controls with labels; errors are announced; notes are escaped; work and payment tables scroll horizontally when required. The client-confirmation notes sit outside the employee product screens in a collapsed review area. Sample data and demo-only actions are explicitly labeled.

No formal User Story IDs were supplied. The traceability table maps approved conversational requirements instead of inventing PRD/AC identifiers. Existing full-payroll eligibility, integrations, authentication and server-side permissions are not implemented.

## Verification — 2026-10-19

| Check | Result | Evidence |
|---|---|---|
| Connected funding → submission → BC → HO → tracking | Passed | Exercised through browser controls in inline wrapper and exported standalone version |
| Empty/over-budget pay validation | Passed | Empty amount blocked; $650 combined against $600 blocked |
| Manual final amount differs from suggestion | Passed | $340 submitted for Alice while suggestion stays $360; HO and period Payment Log retained $340 |
| Credit math and duplicate post prevention | Passed | $600 − $540 posted = $60 available / $0 reserved; post action disabled afterward |
| Cancelled/declined/invalid funding | Passed | Credits unchanged; appropriate validation/decline feedback shown |
| Funding with changed amount / persistence echo | Passed | Editing the amount retains transient test fields; successful $10 and $20 funding updated balance; card fields cleared on completion |
| Work-date vs payroll-period filtering | Passed | Work filtered to $120 calculated earnings while full period payment remained $340 |
| Employee view scope | Passed | Caller view showed Michael's records even when OP role filter was Marketer; marketer showed Alice only |
| Narrow layout | Passed | All eight screens at 320px: root scrollWidth equaled clientWidth; wide tables scroll locally; 375px and 1024px also inspected |
| JavaScript syntax | Passed | Extracted fragment script piped to `node --check`, exit 0 |
| Browser errors/warnings | Passed | Browser log check returned an empty list |
| Live Stripe / full payroll / accounting / ADP integration | Not implemented | Explicitly outside this client-review proposal |

These are prototype-level checks, not a production security, accessibility, or integration certification.
