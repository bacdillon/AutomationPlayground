# Event Proposal Approval and Notification

## 1. Project Overview

This automates how a community organization, "Pedal Paradise," a cycling club, reviews and approves proposals for new events and activities. A Power Automate flow, "New Event Activities Flow," triggers the moment someone submits a new event proposal to a SharePoint list, routes it to a designated approver through Microsoft Teams Approvals, and automatically posts a notification to a shared Teams channel once a decision is made. This closes the loop from submission to team-wide visibility without any manual chasing.

## 2. Business Problem & Objectives

**The problem:** Organizing events and activities usually involves someone submitting a proposal, with a date, venue, budget, and supporting details, that then needs a manager or committee member's sign-off before it can proceed. Handled manually, this means emailing a proposal document, waiting for a reply, and separately telling the rest of the team once a decision is made. Each of these steps is a place where things get delayed, lost, or simply forgotten.

**The objectives:**
- Automatically start an approval request the moment a new event proposal is submitted.
- Route the request to the right approver through a tool they already use daily, Microsoft Teams.
- Capture a clear, structured decision (Approve or Reject) along with any approver comments.
- Automatically notify the wider team once a final decision has been made, without requiring the approver or submitter to do it manually.
- Keep a single, authoritative record of every proposal's status in one place.

## 3. Solution

A Power Automate flow triggers on a SharePoint list called "Event Activities." Every new item, an event proposal with its date, venue, budget, and a supporting document, automatically starts a Microsoft Teams Approval request, sent directly to a named approver. The approver reviews the proposal, including opening the attached supporting document such as a safety inspection guide, and responds Approve or Reject from within Teams. Based on the outcome, the flow updates the SharePoint list item's status and posts a notification message to a shared Teams channel, so the whole team sees the outcome without needing to check the list themselves.

### What the Video Demonstrates

The video shows the flow's design in Power Automate alongside a live demonstration:

- The flow's structure: a trigger on "When an item is created" in the "Event Activities" SharePoint list, followed by "Start and wait for an approval" (Approve or Reject, first to respond), configured with the event's key details (event or activity name, budget, event date, submitted by, and a link back to the SharePoint item) shown to the approver.
- A live walkthrough of submitting a new proposal, "Bike Safety Inspection Day," scheduled for 14 November 2026 at the "Pedal Paradise Workshop," with 60 participants and a $1,000.00 budget, including searching for and selecting the submitter from the organization directory, and attaching a supporting PDF document, a detailed cycling safety inspection guide, shown being reviewed directly in Adobe Acrobat.
- The existing "Event Activities" list, showing several prior proposals already carrying a status of Approved, Rejected, or Pending, confirming this flow has been used repeatedly, not just for this one demo.
- The flow being tested and run, followed by the approval request landing in Microsoft Teams' Approvals inbox, alongside a history of prior approval requests, including ones for a different but related process, customer approvals, showing the same pattern reused elsewhere.
- A final notification posted to a shared Teams channel: "A new proposal has submitted for approval: Pedal Paradise Appreciation Ride," followed by "Final status: Approved," confirming the end-to-end notification step working as designed.

### End-to-End Workflow, Step by Step

1. **A new proposal is submitted.** Someone adds a new item to the "Event Activities" SharePoint list, filling in the event name, date, venue, participant count, budget, and attaching a supporting proposal document.
2. **The flow triggers automatically.** Power Automate detects the new item and starts the approval process without any manual step.
3. **An approval request is sent.** The designated approver receives a structured request in Microsoft Teams, showing the event's key details and a link back to the full item.
4. **The approver reviews and decides.** They can open the attached proposal document for full context, then respond Approve or Reject, optionally adding a comment.
5. **The flow checks the outcome.** A condition checks whether the response was "Approve."
6. **The SharePoint list is updated.** The item's Approval Status field is updated to reflect the decision.
7. **The team is notified.** A message is posted automatically to a shared Teams channel, announcing the proposal and its final status, so the whole team stays informed without needing to check the list directly.

## 4. Solution Architecture & Technologies

- **Microsoft SharePoint**, hosting the "Event Activities" list, the system of record for every proposal and its current status.
- **Microsoft Power Automate (cloud flow)**, orchestrating the entire process, triggered by the SharePoint "When an item is created" event.
- **Microsoft Teams Approvals**, using the "Start and wait for an approval" action (Approve or Reject, first to respond), delivering the request directly into the approver's Teams client.
- **Microsoft Teams channel messaging**, using the "Post message in a chat or channel" action to broadcast the final outcome to a shared channel ("Alfred Bot Channel").
- **A condition checking whether Outcome equals Approve**, which branches the flow's downstream behaviour based on the approver's decision.

The proposal itself, submitted as an attached document such as a PDF safety inspection guide, travels with the SharePoint list item, so the approver has full supporting context available directly from the approval request.

## 5. Controls & Validation

- **Every new proposal is automatically captured.** Because the flow triggers directly off SharePoint's "item created" event, no proposal can be submitted without also kicking off the approval process.
- **A single, named approver is explicitly assigned** on every request, so there is no ambiguity about who is responsible for the decision.
- **The approval outcome is a structured, binary decision** (Approve or Reject), not a free-text reply, which is what allows the flow to branch reliably afterward.
- **Every proposal's status is tracked centrally** in the SharePoint list itself, with values observed including Approved, Rejected, and Pending, giving a single source of truth rather than relying on scattered emails or chat messages.
- **The final outcome is broadcast automatically**, removing any dependency on the approver remembering to tell anyone else.

## 6. Business Value

- **Removes manual chasing.** No one has to email a proposal, wait, and then separately notify the team. The whole cycle is automatic.
- **Faster decisions.** Because the approval request lands directly in the approver's Teams client, a tool they are already using, there is no delay waiting for someone to check a separate system or inbox.
- **Full visibility for the whole team.** Everyone sees the outcome of a proposal through the shared Teams channel, not just the submitter and approver.
- **A reliable, centralized record.** The SharePoint list always reflects the current, accurate status of every proposal.

## 7. Skills Demonstrated

- Building event-driven, trigger-based automation in Power Automate.
- Integrating SharePoint lists as both a data source and a system of record.
- Configuring Microsoft Teams Approvals for structured, trackable decision-making.
- Using conditional logic to branch a flow based on an approval outcome.
- Automating team-wide notifications through Teams channel messaging.
- Designing a complete submit, approve, and notify pattern that removes manual follow-up at every step.

## 8. Enterprise Use Cases

This submit, approve, and notify pattern applies broadly across many organizations:

- **Event and activity proposal approval**, as demonstrated here.
- **Purchase or expense request approvals**, routed to a budget owner.
- **Content or marketing material sign-off**, before publication.
- **Vendor or supplier onboarding approval.**
- **Policy or document review workflows**, where a change needs sign-off before taking effect.
- **Any process where a submission needs a decision, and that decision needs to be visible to a wider team.**

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Routing approvals through a tool people already check daily, such as Teams, removes a major source of delay compared to email-based approval chains.
- Keeping the proposal's supporting document attached directly to the list item means the approver never has to go hunting for context elsewhere.
- Automatically notifying a shared channel, rather than just the submitter, makes outcomes visible to the whole team, not just the two people directly involved.
- Centralizing status in the SharePoint list itself avoids the common problem of an approval decision living only in an email thread that others cannot see.

**Future enhancements:**
- Add a reminder or escalation step if an approval request goes unanswered after a set period.
- Route different types of proposals, for example by budget size, to different approvers automatically.
- Add a rejection reason field that is surfaced clearly to the submitter, not just logged as a comment.
- Extend notifications to email, for team members who may not be active in the Teams channel.
- Build a simple dashboard summarizing proposal volume, approval rates, and average decision time over time.
