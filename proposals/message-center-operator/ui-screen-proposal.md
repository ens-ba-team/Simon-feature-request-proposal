# UI Screen Proposal: Manual Messages and Message for Operator

Status: Interactive review draft built at the user’s request — 2026-10-18. Required creation fields remain open.

Preview: [Interactive UI](http://127.0.0.1:8766/) · [Standalone HTML](../../prototypes/operator-messages/index.html).

## Confirmed scope

- Admins can manually create messages, selecting a type and entering its required fields.
- Reuse the existing creation API and business rules for existing types.
- Add Message for Operator, assignable to an operator and visible on that operator's dashboard. This type creates a message and notification. The operator reaches assigned messages through a new Action Center summary row; saving a message does not create a separate operational action.
- Reuse existing Message Center notification settings and define the new notification content. Send through enabled channels; do not assume all channels are enabled.
- Confirmed dashboard entry: an Action Center row labeled “Messages for you” with a number. Clicking the row opens an operator Message Center page using the current HO table layout; Business shows the operator name.
- Confirmed resolution behavior: the operator can mark an assigned message as resolved on the operator Message Center page. The Action Center count includes all assigned, unresolved messages; viewing alone does not reduce it.
- The linked ticket 1413 chat is a reference for the interactive preview and client proposal format. Payroll functionality is outside this proposal.

## Reference Layout Analysis

### R-01 — Admin Message Center

Inspected artifact: Screenshot 2026-10-18 at 10.02.35.png, supplied by the user.

The 1822 × 699 screenshot shows a page title, a full-width tab strip, one horizontal filter row, and a full-width table. The table is empty. Its visible columns are ID, Date, Client, Email, Postal Code, Message, and Source. Tabs are Message for Office, Lead, Complaint, Warranty, and Employment. No creation control is visible.

```text
Message Center
┌─ Full-width tabs ──────────────────────────────────────────┐
│ Office | Lead | Complaint | Warranty | Employment         │
└───────────────────────────────────────────────────────────┘
[Search ID] [Source ▼] [Show Archived toggle]
┌─ Full-width message table ─────────────────────────────────┐
│ ID | Date | Client | Email | Postal Code | Message | Source│
│                         No data                           │
└───────────────────────────────────────────────────────────┘
```

Preserve the title → tabs → filters → table hierarchy. **Recommended:** add the primary creation control to the title row and append an operator-message tab. Preserve filters according to each type's existing behavior rather than applying Office-only controls to every type.

### R-02 — Operator Dashboard

Inspected artifact: Screenshot 2026-10-18 at 10.04.11.png, supplied by the user.

The 1895 × 964 screenshot shows a narrow left navigation rail, top account/division/year/notification controls, a full-width welcome banner, a wide Company Stats panel next to a narrower Action Center, and Company Message / Upcoming Events below. The visible main columns have an approximately 4:1 ratio in the first row. The screenshot establishes visible placement, not sticky or scrolling behavior.

```text
┌─ Nav ─┬─ Top account / division / year / notification bar ─┐
│       ├─ Full-width welcome banner ───────────────────────┤
│       ├─────────────────────────────────┬─────────────────┤
│       │ Company Stats — wide            │ Action Center   │
│       ├───────────────────────────┬─────┴─────────────────┤
│       │ Company Message           │ Upcoming Events     │
└───────┴───────────────────────────┴───────────────────────┘
```

Preserve the existing navigation and the relative ordering of the existing panels. **Required by user feedback:** add “Messages for you” with a number as a new row inside Action Center. This replaces the earlier recommendation for a separate dashboard section.

### R-03 — Current HO Message Center table

Inspected artifact: Screenshot 2026-10-18 at 10.12.42.png, supplied by the user.

The screenshot shows a full-width table with ID, Date, Applicant (name, phone, address), Email, Postal Code, Business, Message, Source, and a row menu. Business is a dropdown displaying Unassigned in the sample. Bottom-right controls contain page size, result range, Previous, page number, and Next. The screenshot contains only the table region; it does not establish page-header, tab, or filter behavior.

```text
┌─ Full-width current HO table ──────────────────────────────────┐
│ ID | Date | Applicant | Email | Postal Code | Business |       │
│ Message | Source | Row menu                                   │
│                                                               │
│ Rows: stacked applicant details; Business dropdown             │
├───────────────────────────────────────────────────────────────┤
│                   [50 / page] 1–3 of 3 [Previous] 1 [Next]    │
└───────────────────────────────────────────────────────────────┘
```

**Required:** reuse this table layout for the operator-facing page and display the operator name in Business. **Recommended:** show Business as text in the operator view; the Admin assignment selector remains separate. The screenshot's row menu does not establish which actions an operator may perform. **Recommended:** use Client as the contact-column label for operator messages, consistent with R-01; Applicant in R-03 belongs to the employment example.

## Proposed Screen List

Dashboard entry and destination below reflect the user's explicit direction. Other presentation choices remain **Recommended** until approved.

| ID | Screen/state | Purpose | Trigger | Reference |
|---|---|---|---|---|
| S-01 | Admin Message Center | Entry point for manual creation and operator-message visibility | Open Message Center | R-01 |
| S-02 | Create Message drawer | Select type, complete fields, assign operator when applicable | Click Create Message | R-01; existing edit-panel pattern |
| S-03 | Operator Dashboard | Show the assigned, unresolved message count in Action Center | Open Dashboard | R-02; user correction |
| S-04 | Operator Message Center page | View assigned messages and mark them as resolved | Click Messages for you | R-01 / R-03; user correction |

The earlier proposed standalone dashboard message block, assigned-message list drawer, and separate operator message-detail drawer are superseded. The new initial proposal has four screens/states and uses the table's Message column to display message content.

### S-01 — Admin Message Center

Purpose: let Admin create messages and find the new type. Add Create Message aligned to the right of the title. Append Message for Operator to the existing tabs. **Recommended:** use the existing Business column for the assigned operator in the new type's table. Exact Source value for manual entries is **Open**; do not fabricate an existing source value.

```text
Message Center                              [Create Message]
┌─ Tabs ─────────────────────────────────────────────────────┐
│ Office | Lead | Complaint | Warranty | Employment |       │
│ Message for Operator                                     │
└───────────────────────────────────────────────────────────┘
[Existing filters appropriate to selected type]
┌─ Table — Message for Operator selected ─────────────────────┐
│ ID | Date | Client | Email | Postal Code | Business | Message | Source  │
│ Message records / empty state                             │
└───────────────────────────────────────────────────────────┘
```

The existing types retain their existing table behavior. New-type editing, conversion, and reassignment behavior are **Open**, not added as new controls in this initial proposal.

### S-02 — Create Message drawer

Purpose: manually submit a selected message type through the existing creation logic. **Required by user feedback:** omit Division from this form. The existing global-header Division selector is separate. **Recommended:** a right-side drawer, consistent with the documented edit-panel pattern. The screenshot does not itself show a drawer.

```text
┌─ Message Center behind drawer ─────┬─ Create Message ──────┐
│                                   │ Heading          [×] │
│ Existing tabs, filters, and table  │ Message type [▼]     │
│                                   │                      │
│                                   │ Selected type fields │
│                                   │                      │
│                                   │ Operator [▼]         │
│                                   │ (operator type only) │
│                                   │ Message              │
│                                   │ [Multiline input]    │
│                                   │ Inline field errors  │
│                                   ├──────────────────────┤
│                                   │ [Cancel] [Create]    │
└───────────────────────────────────┴──────────────────────┘
```

States share this layout:

- Before a type is selected, show the type selector and prompt to choose a type.
- For an existing type, show its existing required fields and apply existing validations and downstream behavior. Lead subtypes and their exact labels must follow the current creation contract.
- For Message for Operator, show the operator selector and agreed fields. Required fields are **Open** pending the user's answer; no required markers or new validation contract are confirmed here.
- While submitting, show progress on Create and prevent repeat submission in the preview.
- On validation or save failure, preserve inputs and show the returned errors in the same drawer so Admin can correct and retry.
- On success, close the drawer and refresh the relevant list. Proposed success copy: “Message created.” Notification delivery success is separate from successful message creation.
- Cancel / close return to the unchanged list. A confirmation for unsaved changes is **Open**, so it is not assumed.

### S-03 — Operator Dashboard

Purpose: expose assigned messages after login through the existing Action Center. **Required:** add a row labeled Messages for you with a right-aligned number, clickable to open S-04. **Recommended:** place it first within Action Center so it is visible immediately; reuse existing row styling and count alignment. **Required:** the count includes all unresolved messages currently assigned to the operator, irrespective of whether they have been viewed. Successfully marking one as resolved removes that message from the count; opening it does not reduce the count.

```text
┌─ Nav ─┬─ Existing top bar ────────────────────────────────────┐
│       ├─ Existing welcome banner ───────────────────────────┤
│       ├────────────────────────────────┬────────────────────┤
│       │ Company Stats                  │ Action Center      │
│       │                                │ Messages for you 3 │
│       │                                │ Existing rows ...  │
│       ├──────────────────────────┬─────┴────────────────────┤
│       │ Company Message          │ Upcoming Events         │
└───────┴──────────────────────────┴──────────────────────────┘
```

The number 3 is illustrative sample data; the metric is all assigned, unresolved messages. Loading/failure should use the existing Action Center pattern and must not falsely display zero on failure. Zero-message behavior is **Recommended:** keep the row visible with 0, opening the empty S-04 page. Opening or reading a message does not decrement this count. Successful resolution refreshes the count, including when the operator returns to Dashboard. Do not introduce unread styling as part of this metric.

### S-04 — Operator Message Center page

Purpose: let the signed-in operator view messages assigned to them, using the existing HO Message Center screen structure. **Required:** Dashboard → Action Center → Messages for you opens a full Message Center page. Business displays the operator name. The page's dataset is restricted to that operator's assigned messages; it does not grant access to the complete HO inbox.

**Recommended:** keep the existing application navigation and top bar. Use Message Center as the title and Message for Operator as the current message category; no other category is exposed in this new operator entry. Reuse existing table and pagination components. The operator-filter control is unnecessary for this scoped page; Business in each row already identifies the recipient.

```text
┌─ Nav ─┬─ Existing top bar ────────────────────────────────────┐
│       │ Message Center                                     │
│       │ Message for Operator                               │
│       │ [Search ID] [Source ▼]                             │
│       ├─ Reused Message Center table ───────────────────────┤
│       │ ID | Date | Client | Email | Postal Code |          │
│       │ Business | Message | Source | Status | Row menu   │
│       │ 000081 | ... | Caller details | ... | ... |         │
│       │ Operator name | Message | ... | Unresolved | [⋮]  │
│       │                           [Mark as resolved]      │
│       │ ... only messages assigned to this operator ...    │
│       ├────────────────────────────────────────────────────┤
│       │       [50 / page] 1–3 of 3 [Previous] 1 [Next]     │
└───────┴────────────────────────────────────────────────────┘
```

The selected category, Search ID, and Source filter are reuse recommendations based on R-01. Newest-first order is **Recommended**. Message text should wrap so the operator can read it without a new detail drawer. If the current table requires an existing detail interaction for long content, confirm and reuse it rather than inventing another screen.

Loading, empty, and error states occupy the table body. Empty copy: “No messages assigned to you.” On load failure, retain the page and show Retry. Returning to Dashboard uses existing navigation. Mark as resolved is confirmed. Separate read tracking, archive, edit, conversion, reassignment, and other row-menu actions remain **Open**; the reference screenshot does not authorize those for operators.

#### Resolution interaction — confirmed behavior and recommended placement

- **Required:** the operator can mark their assigned message as resolved on S-04. A resolved message is excluded from the Action Center count. Example: three assigned unresolved messages → resolve one → Messages for you shows 2.
- **Recommended:** reuse the existing row menu: **⋮ → Mark as resolved**. Add a Status column with Unresolved / Resolved so resolution is visible without depending on color.
- **Required:** a message is counted only once. Repeating the operation on an already resolved message must not reduce the count again.
- **Recommended:** show progress while saving. Once persistence succeeds, show Resolved, remove/disable Mark as resolved for that row, and refresh the dashboard count. On failure, preserve the unresolved state and count; show an error and allow retry.
- **Recommended, pending review:** retain resolved rows in the list with their Resolved status so the history remains accessible. Default list filtering and whether resolved rows should be hidden are **Open**. Do not equate resolution with deletion or archiving.
- Reopening resolved messages, Admin resolution rights, and resolution-triggered notifications are **Open** and are not included as controls or new notification events in this proposal.

Notification links are proposed to open this operator-scoped Message Center page, focused on the referenced message when the existing screen supports that behavior. The final route/focus mechanism is **Open**. Apply existing sign-in and access checks before displaying content.

## Notification content proposal

These are draft templates, not new notification settings controls. Use the existing Message Center channel settings; event-to-settings mapping needs confirmation from dev. Do not create separate channel preferences in the creation drawer.

| Channel | Proposed content |
|---|---|
| In-app | Title: “Message Center - Action Required”. Body: “A new Message for Operator has been received and needs your attention.” |
| SMS | “Message Center: A new Message for Operator has been received and needs your attention.” No link. |
| Email | Subject: “New Message Assigned to You — [Sender Name]”. Detailed approved body includes caller contact details, postal code, optional Job / Agreement, full message, received time, source, Message ID, View Details, coach support, and Mark as resolved guidance. Full template is in client-proposal-draft.md and the UI notification panel. |

Wording approved by the user before this UI update. Email omits unavailable optional fields. SMS and in-app use the existing generic notification wording with item name Message for Operator.

The Action Center entry and assigned-message page remain available independently of which notification channels are enabled. This proposal does not define retries, new channel defaults, or notifications on reassignment.

## Open decisions

1. Required fields for the new type: a simplified caller/operator/message form versus all existing API-required fields. The documented API requires postal code, disposition, message, first name, last name, address, email, phone, datetime, and division. Division has explicitly been removed from the form. Dev must confirm how the existing API receives division without that input, along with any other contract change; do not silently populate placeholder data.
2. How resolved messages appear in the list: recommended retention with a Resolved label versus hiding from the initial list. Separate read tracking, archiving, and reopening are not confirmed and are excluded from the initial controls.
3. Dev to confirm the new type's identifier, recipient mapping, manual Source value, and existing notification-settings event mapping. Do not assign an arbitrary numeric disposition ID in a prototype.

## Approval gate

- [x] User directed an Action Center count row and a full operator Message Center page reusing the HO table.
- [x] Count clarified by user: all assigned, unresolved messages; viewing does not reduce it, successful resolution does.
- [ ] Revised S-01 through S-04 inventory and ASCII layouts approved as a whole.
- [x] Operator action confirmed: Mark as resolved.
- [ ] New-type required fields confirmed.
- [ ] Recommended resolution control placement and resolved-row presentation reviewed.
- [x] User requested the updated UI be shown; interactive review draft generated with open fields labeled.

The product-ui-spec skill requires explicit approval of the screen inventory and ASCII layouts before generating the real UI. The user subsequently requested the UI be shown, and an interactive review draft was built from the corrected layout. This document and preview are not a production implementation or BA document.
