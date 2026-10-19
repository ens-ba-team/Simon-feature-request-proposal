# Client proposal draft — Message Center enhancement

Status: Draft with an interactive UI available. Required creation fields remain open. No message has been sent.

Hi [Client Name],

We’d like to propose an enhancement to the Message Center that lets Admins manually create messages and send messages directly to an operator.

**What’s new**

- A **Create Message** button in the Admin Message Center. Admins can select the message type and complete its required fields.
- A new **Message for Operator** type, which can be assigned to an operator for requests such as a callback or rescheduling an estimate. This type saves a message and notifies the assigned operator without creating a separate operational action.
- A **Messages for you** row showing the total number of assigned, unresolved messages in the operator dashboard’s **Action Center**. Clicking it opens an operator-facing **Message Center** page, reusing the current HO table layout. The **Business** column shows the operator’s name. Viewing a message does not reduce the count; marking it as resolved does.

- A **Mark as resolved** action on the operator Message Center page. Once a message is resolved, it no longer contributes to the Action Center count.

**Proposed workflow**

1. The Admin opens Message Center and clicks **Create Message**.
2. They select a message type, enter its required information, and click **Create**. Existing types continue to use the current creation API and business rules.
3. For **Message for Operator**, the Admin selects the recipient operator and enters the caller’s message.
4. Once saved and assigned, the message becomes available in that operator’s Message Center, accessible through the **Messages for you** row in Action Center. Notifications are sent through the in-app, SMS, and email channels enabled in the existing Message Center notification settings.
5. The operator clicks **Messages for you** in Action Center, or follows a notification, to open Message Center and view their assigned messages, caller details, and requests.

6. Once the request has been handled, the operator selects **Mark as resolved**. After the update succeeds, the **Messages for you** count decreases. For example, resolving one of three unresolved messages changes the count from **3 to 2**.

**Approved notification wording**

- **SMS:** “Message Center: A new Message for Operator has been received and needs your attention.” No link is included.
- **In-app title:** “Message Center - Action Required”
- **In-app body:** “A new Message for Operator has been received and needs your attention.”
- **Email subject:** “New Message Assigned to You — [Sender Name]”

**Email body:**

Dear [Operator Name],

A new message from **[Sender Name]** has been assigned to you. Please review their request and follow up as appropriate. If you need support, contact your coach.

Message details:

- Sender: [Sender Name]
- Phone number: [Sender Phone Number]
- Address: [Sender Address]
- Email: [Sender Email]
- Postal Code: [Sender Postal Code]
- Job / Agreement: [Sender Agreement]
- Message: [Sender Message]
- Time Received: [Time Received]
- Source: [Source]
- Message ID: [ID saved in the system]

[View Details]

Once you have handled the request, select **Mark as resolved** in Message Center.

Best regards,  
SIMON Team

Unavailable optional fields are omitted. Division is not included in the Admin Create Message form.

**Interactive UI:** Please open the attached **index.html — Simon Message Center proposal** in your browser. Use the preview toolbar to switch between the Admin and Operator screens.

This is a draft interactive UI, so some components may look or behave differently from the current system. The final implementation will follow the current system’s UI styles and component behavior.

Please review the proposed flow, Action Center entry and operator Message Center screen, and notification wording and let us know your feedback.


---
Sender note: Attach [the standalone interactive HTML](../../prototypes/operator-messages/index.html). The [local preview](http://127.0.0.1:8766/) is available on this computer; an external client needs the attached HTML or a separately hosted URL.
