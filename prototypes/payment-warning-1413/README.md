# Ticket 1413 — interactive payroll UI

Open `index.html` directly in a modern browser. It is a single, self-contained file with embedded styles, JavaScript, and reference imagery. Send that file to clients to let them interact with the preview without installing anything.

For a local browser preview, run `python3 -m http.server 8765 --bind 127.0.0.1` in this directory and open http://127.0.0.1:8765. That address is available only on the computer running the server.

## Approval and sources

- Source: the user's ticket 1413 discussion, supplied payroll screenshots, answers to the clarification questions, and explicit approval of the four proposed states and layouts.
- Layout approval: “ok let's go with UI”.
- Business requirements are confirmed; visual presentation and warning copy remain a design proposal. Vy owns final warning wording.
- The user reviewed and accepted the [BPMN workflow](workflow/index.html). Editable source: [payment-warning-1413.bpmn](workflow/payment-warning-1413.bpmn).
- The ticket-level [BA document](../../Features/new/epic-20-production-payroll/BA-1413-payment-name-warning.md) records the confirmed requirements, testable acceptance criteria, and data-integration handoff.
- No Figma file, production application, backend, or design-system library was supplied for this standalone preview.

## Confirmed rules and implementation

| ID | Required behavior | Implementation |
|---|---|---|
| BR-01 | Warn BC/President when a payment name matches the payroll operator's full name. | `matchesOperator` compares only the relevant payment field to `OPERATOR`. |
| BR-02 | Cheques use Name on cheque; e-transfers use Client name from the payment. | `paymentName` selects the field by method. The job's Client name is separate. |
| BR-03 | Ignore capitalization and extra spaces; otherwise require a full-name match. | `normalizeName` trims, collapses whitespace, and lowercases. No partial or fuzzy matching. |
| BR-04 | Add Payment name to Payments Summary. | Column follows Client name in the existing table hierarchy. |
| BR-05 | Trigger a non-blocking warning when Approve Payroll is selected. | A modal offers Review payments and Acknowledge and approve. |
| BR-06 | Review scrolls to the first match and highlights all matches. | Focus moves to the first matching row; amber rows also include Matches operator name text. |
| BR-07 | Reviewer may acknowledge and proceed. | Acknowledgment reaches the prototype's simulated Approved state. |

## Screen inventory and transitions

| State | Entry | Result / exit |
|---|---|---|
| S-01 Review payroll | Open or reset the preview. | Payment table and existing cash-flow regions; Approve Payroll opens S-02 if names match. |
| S-02 Warning | Approve Payroll with one or more matching payment names. | Review payments enters S-03; acknowledgment enters S-04. Close or Escape returns without approval. |
| S-03 Review matching payments | Review payments. | Modal closes; all matching rows are highlighted. Selecting Approve Payroll reopens S-02. |
| S-04 Approved | Acknowledgment, or simulated approval without name matches. | Approved badge, approver detail, disabled approval control, and success announcement. Reset returns to S-01. |

## Layout and components

- Preserve the screenshot's narrow dark sidebar, global header, breadcrumb, payroll heading and metadata, summary table, payment table, totals, and lower cash-flow region.
- Cash flow uses the reference's three desktop columns: adjustments, balances, and advance/approval panel.
- The warning is a centered native dialog with warning content above an action footer.
- Recommended presentation: amber warning colors, non-color matching indicators, brand-red approval action, thin borders, and pale-blue total rows. These are screenshot-derived approximations, not claimed design-system tokens.
- At narrower widths the financial columns stack and tables scroll horizontally. This is a preview adaptation, not an approved mobile product design.
- Unrelated navigation and advance settings are visual context, not implemented product flows.

## Accessibility and interaction

- Native buttons, select, tables with column headings, named sections, and a labeled dialog.
- Dialog focuses Review payments, traps keyboard focus natively, supports Escape, and restores focus on dismissal.
- Review focuses the first matching row. Successful approval focuses the payroll title.
- Matching rows have both color and descriptive text. Status changes are announced through live regions.
- Focus outlines are visible; reduced-motion preferences disable smooth scrolling and transitions.
- No claim of a formal accessibility audit is made.

## Preview data and boundaries

- Preview controls sit outside the payroll content. Scenarios: With name matches, No name matches, and No payments. Reset preview restores the selected scenario.
- Mock records live in `SAMPLE_PAYMENTS`, separate from name matching and UI code.
- The default scenario contains a matching cheque and a matching e-transfer. The latter demonstrates capitalization and extra-space normalization.
- Financial values and displayed totals are illustrative sample data. They do not define or validate production payroll calculations.
- Approval is simulated in memory. This file does not submit payroll, transfer money, store a decision, or contact a backend.
- Loading, network failure, offline recovery, permissions enforcement, and real approval errors require integration with the actual application. Offline viewing of this standalone file is supported.
- No name matching is performed for unscoped methods, blank names, or missing names. Production handling of missing fields is outside this preview.

## Verification

Verified in the Codex in-app browser at its normal desktop viewport:

- Matching cheque and e-transfer names trigger a warning containing the correct count.
- Review scrolls to the first matching row, moves focus there, and highlights both matching rows with text indicators.
- A second approval attempt reopens the warning.
- Escape dismisses the warning without approval and returns focus to Approve Payroll.
- Acknowledge and approve reaches Approved and disables further approval.
- No-match and empty scenarios bypass this warning and simulate approval.
- Empty state and zero payment totals render correctly; reset restores Submitted.
- No browser warning or error logs were reported. No document-level horizontal overflow at the tested viewport.
- JavaScript syntax and nine source-level matching checks passed, covering both fields, case/space normalization, rejection of partial names and suffixes, separation from job Client name, wrong-field isolation, null/blank values, and methods outside scope.
- Narrow-screen styling is present but has not been visually verified.

Visual evidence: `warning-preview.png` and `highlighted-payments.png`.
