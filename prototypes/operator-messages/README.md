# Simon — Message Center UI proposal

Interactive review draft built on 2026-10-18 from the supplied screenshots and confirmed discussion.

Open `index.html` directly in a browser, or use the local preview at http://127.0.0.1:8766/ while its server is running. The HTML includes its illustration and has no external dependencies, so it can be attached for client review.

Use the preview toolbar to switch between Admin Message Center, Operator Dashboard, and Operator Message Center.

## Review paths

1. On Operator Dashboard, click **Messages for you: 3** in Action Center.
2. In the assigned-message table, open a row's **⋮** menu and select **Mark as resolved**.
3. Return to Dashboard. The number is now **2**. Resolved messages remain in the list with a Resolved label for this draft.
4. Switch to Admin Message Center, click **Create Message**, select **Message for Operator**, select the operator, and click **Create**. The assigned operator's collection/count updates.
5. Open **Notification copy** for the proposed in-app, SMS, and email wording. The templates use the approved detailed email and existing generic SMS/in-app wording. SMS has no link. No delivery is performed.
6. **Reset demo** restores three unresolved messages for the preview operator and one message for a different operator.

## Scope and open decisions

- This is a local UI simulation. It does not call the creation API, create live business objects, or send notifications. Production must reuse the current API/business rules and existing notification settings as agreed.
- Sample records and resolution states persist in this browser's local storage. This is demonstration scoping, not server authorization. Production must enforce operator access on the server.
- Division has been removed from the Admin Create Message form at the user’s request. Production division mapping needs dev confirmation; the global-header selector is separate.
- Required fields for the new type remain unconfirmed; the preview explicitly labels the form as illustrative and makes no claim that all displayed fields will be mandatory.
- Existing message types are selectable to illustrate the creation entry. Their downstream business flows remain part of the current production rules and are not simulated here.
- The draft keeps resolved messages visible with a status. Final resolved-message filtering and reopening remain open.
- Manual creation uses Office as an illustrative source. Final mapping remains open.
- The notification panel illustrates content and navigation; production delivery follows enabled channels in the existing Message Center settings.

## Verified in browser

- Dashboard entry opens the operator's assigned-message table.
- Resolve changes the dashboard count from 3 to 2, leaving the message visible as Resolved.
- Admin creation adds an assigned message, increasing that operator's unresolved count.
- Operator collection excludes a sample record assigned to another operator.
- The initial narrow browser layout keeps Action Center visible; the desktop layout follows the supplied screens.

Proposal sources: `../../proposals/message-center-operator/ui-screen-proposal.md` and `client-proposal-draft.md` in that directory.
