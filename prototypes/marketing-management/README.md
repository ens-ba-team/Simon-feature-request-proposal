# Marketing Management — operational UI proposal

Status: client-review prototype, not a production implementation. Approved screen/layout scope: eight screens on 2026-10-19, extended with Profit on 2026-10-21 and the E-Transfer funding drawer / two-tab report on 2026-10-22. Ten screens plus the funding drawer.

Open `index.html` in a browser. It is a standalone, self-contained proposal suitable for sending as a file. The earlier eight-screen version was published; these local Profit / E-Transfer updates have not been pushed or deployed. No real card processing, Interac notification import, payroll, ADP export, accounting journal, or employee bank payment occurs.

## Walkthrough

1. OP → Marketing Management: available and reserved credits, funding history, no funding Status column.
2. **Add Funding ▾ → Credit Card**: existing checkout; enter an amount, select **Use test details**, then Pay. Cancel/decline do not add credits. No card, CVC, payer, or postal-code input is persisted. **Add Funding ▾ → E-Transfer** opens the new sender-name / amount drawer, described below.
3. Prepare Payroll → Marketing (after Commission): review leads/conversions and configured unit rates; enter final amounts and optional notes. One shared available-credit balance limits the combined amount.
4. Submit Payroll: freeze a snapshot and reserve the combined Marketing total. Other existing payroll validation remains a handoff, not implemented or bypassed.
5. BC → Review & approve: read-only submitted Marketing amounts; approval retains the reservation.
6. HO → Payroll Summary: COMPANY TOTAL first; Total Labour, Total Job Training, Total Commission; BC/OP details below. Each OP has Labour, Commission, then Marketing. Posting is unavailable before BC approval. Posting consumes reserved credits once, without reducing available credits a second time.
7. OP → Marketing Management Log: combined work/results table and separate Payment Log; employee and role filters.
8. Marketer / Caller → own earnings: work/results and separate own Payment Log. Results-based calculated earnings can differ from OP's final pay.
9. OP → Profit: Income Statement retains the supplied row order. Marketing Expense is indented below Fixed Expenses as an included detail, not an additional deduction. It affects Net Profit, not Gross Profit. The preview displays $0.00 throughout, independently of funding and payroll posting; accounting recognition timing is unresolved. New sessions open Marketing Management; existing saved sessions may restore their prior screen. Use the Profit navigation button or Preview screen selector to open it.
10. Admin → E-Transfer Report: **Client Payment** retains the client-report hierarchy; **Operator Payment** shows Marketing deposits, status and the claiming OP. Both tabs have search, date/status/amount filters, filtered totals and a reference-only Download Report action. Operator Payment has no invoice column or invented claim/unclaim actions.

Use **Preview screen** to move between roles. This is a demo navigator, not a proposed cross-role product permission. **Proposal notes & client confirmations → Reset demo data** restarts the walkthrough.

## Source and design evidence

- Latest user-confirmed rules in this conversation: marketer = leads × rate per lead; caller = conversions × rate per conversion; shared credit limit; reserve on submission, deduct on HO posting.
- HO screenshot: `Screenshot 2026-10-19 at 10.58.10.png`, supplied in this conversation. Its company-total-first hierarchy and header actions are retained.
- Profit screenshot: `Screenshot 2026-10-21 at 17.07.09.png`, inspected directly. Revenue, Gross Profit and Net Profit retain shaded emphasis; Commission remains above Gross Profit. The user approved Marketing Expense as an indented Fixed Expenses detail.
- E-Transfer screenshots: `Screenshot 2026-10-22 at 15.05.52.png` (report) and `Screenshot 2026-10-22 at 15.12.08.png` (drawer), inspected directly. The approved adaptation removes invoice-specific Balance Due / Add Another Payment from funding; it adds separate Client / Operator report tabs.
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
| Marketing Expense included in Fixed Expenses | Profit / Income Statement | Browser: approved row order, indented detail, all zero-value layout samples; no posting/funding linkage |

## Open questions retained for client discussion

1. **Louis:** Confirm employee Payment Log updates on HO posting. Demo uses this trigger; “Total paid” means posted payroll amount, not confirmed bank receipt.
2. **Louis:** Confirm payment tracking only per employee/payroll period, without allocations to individual sessions/dates. Demo separates work-date filters from payment-period filters.
3. **Nat / Maria:** Credit GL/liability, funding and expense journals, reconciliation, burden, ADP mapping and actual payment workflow remain undefined. HO posting hands off to that future process.
4. **Louis:** Final lead/conversion attribution, cutoffs, rate-change and correction rules remain open. Sample data does not define these rules.
5. **Team:** Rejection/withdrawal/correction credit-release rules are not defined and are not simulated.
6. **Louis:** BC approval for E-Transfer funding still requires confirmation. The approved UI demo releases credits immediately after a unique eligible match, as requested; this is not evidence of final client approval of that policy. Bank reconciliation is not a prerequisite in this proposal.

## E-Transfer walkthrough — 2026-10-22

1. Reset demo data: available credits are $600.00. Two Marketing transfers have already been received as **Unclaimed**: Cameron Roach / $250.00 and Roach Painting / $150.00. A separate client transfer (Linh / $200.09) cannot fund Marketing.
2. In Marketing Management choose **Add Funding ▾ → E-Transfer**. Enter bank transfer sender name `Cameron Roach` and amount `250.01` to see a non-matching error. No credits or report status change.
3. Correct the amount to `250.00`, then Add Funding. Available credits become $850.00, funding history gains an E-Transfer entry, and the same report record becomes **Claimed**, linked to Cameron Roach. There is no Status column in funding history.
4. Open **Admin → E-Transfer Report → Operator Payment** to review the shared record. Unclaimed records show no Operator; claimed records show the claiming SIMON OP, not necessarily the bank sender name.
5. Retry the claimed sender/amount: no additional credits. Claim `Roach Painting` / `150.00` to demonstrate that a bank sender name can differ from the OP profile; it credits the logged-in OP, not an account inferred from the sender name.
6. **Receive sample Interac notification** in the outer demo toolbar creates Cameron Roach / $300.00 as Unclaimed. It does not add credits. **Replay sample Interac notification** ignores that same notification ID. Claim the $300.00 through the funding drawer to add credits.

Matching is restricted to Operator transfers received at `marketing@studentworks.com`, with Unclaimed status and matching sender name / integer-cent amount. The demo compares names exactly after trimming surrounding spaces; final name-normalization rules are not established. Multiple eligible matches are blocked for investigation, never selected arbitrarily. Cancel / Escape closes the drawer without adding credits or reversing any real transfer. There is no live bank integration.

## E-Transfer verification — 2026-10-22

| Requirement / AC | Implementation and browser evidence | Result |
|---|---|---|
| Payment-method selection and drawer | Funding menu opens existing checkout or new right-side drawer; no invoice balance / additional-payment controls | Passed |
| Unmatched claim makes no changes | Cameron / $250.01 error; $600.00 remains available; correcting to $250 adds credits | Passed |
| Successful match updates shared records once | $600 → $850; funding history shows E-Transfer; report MKT001 is Claimed / Cameron; persisted after reload | Passed |
| Duplicate claim blocked | Repeating Cameron / $250 is rejected; $850 balance unchanged | Passed |
| Sender may differ from profile | Roach Painting / $150 credits Cameron's account; balance $1,000 | Passed |
| Client transfers cannot fund Marketing | Linh / $200.09 rejected; balance unchanged | Passed |
| Notification import / replay | New $300 record Unclaimed; report total $700; replay total remains $700 with no credits; claim brings balance to $1,300 | Passed |
| Report tabs and filters | Client total $200.09; operator-only total $700; status, reference search, amount range and date filtering verified; invalid range shows feedback | Passed |
| Cancel / keyboard | Cancel and Escape make no credit changes; focus returns to funding trigger; Tab / Shift+Tab remain inside drawer | Passed |
| Card and payroll regression | $10 card funding → $1,310; submit reserves $560 / available $750; BC approval; HO posting leaves $750 available / $0 reserved; repeat posting disabled | Passed |
| Responsive containment | At browser widths 320 / 375 / 1024, root clientWidth = scrollWidth (288 / 343 / 992); report table scrolls locally; drawer footer stays inside shell | Passed |
| JavaScript / browser diagnostics | `node --check` exit 0; browser error / warning logs empty | Passed |
| Ambiguous-match branch | Code blocks multiple eligible name/amount matches; fixture does not contain duplicates, so browser path not exercised | Not tested |
| Live Interac, bank reconciliation, production permissions, report export | Outside approved prototype scope; report download is reference-only | Not implemented |

Screenshots were visually inspected for the drawer/error and two-tab report. This is screenshot-informed proposal QA, not a pixel-match or production certification. Old saved v1 state has a migration path; its migration has not been separately exercised in this update.

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

## Profit-screen verification — 2026-10-21

| Check | Result | Evidence |
|---|---|---|
| Approved Income Statement hierarchy | Passed | Full-page browser screenshot: original rows retained; Marketing Expense follows Fixed Expenses, before Net Profit |
| Navigation | Passed | Preview selector opens Marketing Management; Profit navigation returns to Income Statement |
| Narrow layout | Passed | At 320px browser viewport, prototype root clientWidth and scrollWidth both 288px; values and wrapped labels remain visible |
| JavaScript syntax | Passed | Extracted fragment script piped to `node --check`, exit 0 |
| Browser errors/warnings | Passed | Browser log check returned an empty list |
| Accounting calculation/integration | Not implemented | Zero-value layout only; recognition trigger and GL mapping await Nat / Maria |

No new journals, funding-as-expense rule, or automatic Profit update on HO posting were introduced. The existing eight-screen flows were not fully re-tested in this UI-only update; their prior verification remains recorded above.
