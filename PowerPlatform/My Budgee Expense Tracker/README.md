# My Budgee Expense Tracker

**Automation Playground Portfolio Project**

A low-code expense management app built on Microsoft Power Apps and Power Automate. "My Budgee Expense Tracker" lets employees log expenses against a budget, routes each submission to a manager for approval automatically by email, and gives both employee and approver a full, transparent history of every request including the ability to fix and resubmit a rejected claim.

## 1. Project Overview

This project is a working expense tracking and approval application, built for everyday business use. Employees log expenses with amount, category, description, and a receipt attachment against a running budget. Each submission automatically notifies the assigned approver by email, who can review and approve or reject it with a comment directly through the app. The employee is then notified of the outcome, and if a claim is rejected, they can see exactly why and correct it. Every step of this process, from submission to final decision, is tracked and visible.

## 2. Business Context

Almost every organization needs a way for employees to submit expenses such as travel, meals, accommodation, and other work related costs and get them approved by a manager before reimbursement. This is a small but constant administrative process, and how well it's handled affects both employee experience and financial control. Done informally (paper forms, email chains, spreadsheets), it's slow and easy to lose track of. It should be quick for the employee, easy for the approver, and fully auditable for the business.

## 3. Business Problem

Expense submission and approval processes commonly run into a few recurring issues:

- **Submissions get lost or delayed** when they rely on informal methods like email attachments or paper forms.
- **Approvers aren't notified promptly**, so requests sit untouched until someone follows up.
- **Rejected claims lack clear feedback** an employee may not know exactly why a claim was turned down or what to fix.
- **There's no budget visibility** employees may not have a clear, real-time sense of how much of their budget they've already used.
- **There's no single, traceable history** of a request's journey from submission to decision.

## 4. Project Objectives

- Let employees easily log expenses with full details and supporting attachments.
- Show employees a live view of their budget: how much has been spent and how much remains.
- Automatically notify the correct approver whenever a new expense is submitted.
- Let approvers review, approve, or reject requests with comments, directly and quickly.
- Automatically notify employees of the outcome of their request.
- Allow employees to see rejection reasons clearly and correct and resubmit a claim.
- Maintain a full, visible history of every request's status and actions.

## 5. What the Video Demonstrates

The video walks through a Power Apps application called **"My Budgee Expense Tracker,"** showing:

- The **Home screen**, showing the current budget status (e.g., "$533.00 of $2,000.00" spent, with the remaining balance clearly shown) alongside a quick-access expense logging form.
- The **Log New Expense** screen, where a user enters the date, category (e.g., Meal, Transportation, Accommodation), amount, and description, sees the approver automatically assigned, and can attach a supporting file before submitting.
- A **"Submitted Successfully"** confirmation, followed by an automatic email. **"Expense Approval Needed"** sent to the designated approver, informing them a new request needs review.
- The **Approval Expense Reporting** screen, used by the approver to see all requests awaiting their decision, filterable and sortable by status and date.
- The **Approval Expense Reporting Details** screen, where the approver reviews the full request (amount, description, attachments) and sets a decision — **Approved** or **Rejected** along with a comment (for example, "Receipt needed"), with a visible history log of the request's actions.
- An automatic **"Status for Expense Request"** email sent back to the original requester once a decision is made, closing the loop.
- The employee's **View Past Expenses** screen, showing their own submissions with clear status badges (Pending, Approved, Rejected).
- An **Edit Submitted Expense** screen for a rejected claim, showing the approver's comment and history, and allowing the employee to attach the missing information such as a receipt and resubmit.

## 6. End-to-End Workflow, Step by Step

1. **Check the budget.** The employee views their current budget status on the home screen before logging a new expense.
2. **Log a new expense.** The employee fills in the date, category, amount, and description, and attaches a supporting file if needed.
3. **Submit the request.** On submission, the app confirms success and records the expense with a "Pending" status.
4. **Notify the approver.** An automated email is sent to the assigned approver, alerting them that a new request needs review.
5. **Approver reviews the request.** The approver opens the request, reviews the details and attachment, and decides to approve or reject it, adding a comment if needed.
6. **Notify the employee.** An automated email is sent back to the employee, letting them know their request's status has been updated.
7. **Employee reviews the outcome.** The employee checks their past expenses list to see the final status and any comments.
8. **Correct and resubmit if needed.** If a claim was rejected, the employee can open it, review the reason, attach any missing information, and resubmit.

## 7. Systems and Applications Involved

- **Microsoft Power Apps** — the application employees and approvers use to log, review, and manage expenses
- **Microsoft Power Automate** — the workflow engine sending automated email notifications
- **Microsoft Outlook** — the channel through which approval and status notifications are delivered

## 8. Technologies Used

- **Power Apps (canvas app)** — for building the expense submission, approval, and reporting screens
- **Power Automate (cloud flows)** — for triggering email notifications on submission and on status change
- **A structured data source** - behind the app where storing expense records, statuses, comments, and history
- **File attachment handling** — for supporting receipts and other documentation

## 9. Automation Logic

The app is built around a clear status lifecycle: every expense starts as **Pending**, and can only move to **Approved** or **Rejected** through an explicit decision by the assigned approver. There is no way for a request to be ignored or left in limbo. Two automated notifications anchor the process: one the moment a request is submitted (alerting the approver), and one the moment a decision is made (alerting the employee). Neither party ever has to manually check for updates. The app also keeps the full history of a request's status changes and comments attached to that same record, so context is never lost, even if a claim needs to be corrected and resubmitted.

## 10. AI Capabilities

This project doesn't use AI. It is a structured, workflow-driven business application. Its strength is in **clear, considerate process design**: automatic notifications, visible budget tracking, transparent rejection feedback, and a straightforward resubmission.

## 11. User Interactions

- **Employees** log new expenses, monitor their budget, view their submission history, and correct and resubmit rejected claims.
- **Approvers** receive requests by email, then review, approve, or reject them directly in the app, adding comments as needed.
- Both roles interact with the app primarily through short, focused screens designed for a specific task such as logging, reviewing, or checking status rather than one complex, all-in-one interface.

## 12. Inputs and Outputs

**Inputs:**
- Expense details: date, category, amount, description, and an optional file attachment
- The approver's decision (approved/rejected) and any comments

**Outputs:**
- An updated expense record with current status and full history
- Automated email notifications to the approver (on submission) and the employee (on decision)
- A live, updated view of the employee's remaining budget
- A complete, browsable history of past expenses and their outcomes

## 13. Error Handling and Validation

- Every expense must move through a defined status lifecycle (Pending to be Approved or Rejected), so a submission can't be lost or left unaddressed without a clear record.
- Rejections require a comment, ensuring the employee always receives specific, actionable feedback rather than just a rejected status with no explanation.
- The resubmission flow lets an employee directly address the stated issue such as attaching a missing receipt rather than starting over from scratch.
- Automated notifications remove reliance on either party remembering to check for updates manually.

## 14. Business Rules

- Every expense request must be routed to a specific, assigned approver.
- A request must be explicitly approved or rejected.
- A rejection must include a comment explaining the reason.
- The employee's budget total and remaining balance must reflect submitted expenses accurately and in real time.
- A rejected request must remain editable, so the employee can correct and resubmit it.

## 15. Key Features Demonstrated

- Self-service expense submission with attachment support
- Live budget tracking (spent vs. remaining)
- Automated email notifications at both the submission and decision stages
- A dedicated approver interface for reviewing, approving, or rejecting requests with comments
- Full request history and status tracking
- A clear correction-and-resubmission path for rejected claims

## 16. Business Value and Benefits

- **Faster approvals**, since approvers are notified immediately rather than needing to be chased.
- **Better employee experience**, with clear budget visibility and specific, actionable feedback on rejected claims.
- **Reduced administrative overhead**, since notifications, status tracking, and history are all handled automatically.
- **Stronger financial control**, with every expense requiring an explicit approval decision and a full audit trail.
- **Fewer repeated errors**, since employees can see exactly what needs fixing on a rejected claim rather than guessing.

## 17. Productivity Improvements

- Removes the need for manual follow-up to get an expense approved.
- Eliminates informal, hard-to-track submission methods like emailed receipts or paper forms.
- Saves approvers time by presenting requests clearly, with all relevant details and attachments in one place.
- Speeds up correction of rejected claims by making the reason and required fix immediately clear.

## 18. Time or Cost Savings (If Evident)

The video shows a submitted expense reaching the approver by email within about a minute, and the employee receiving a status update automatically once a decision is made. Both steps that would otherwise depend on manual follow-up. It doesn't show large scale, real world usage figures, so no specific dollar or hour savings number is claimed here. Replacing manual, informal expense processes with automated notifications and a clear approval workflow is a well-established source of time savings and reduced administrative friction in day-to-day business operations.

## 19. Skills Demonstrated

- Designing a multi-role (employee/approver) business application in Power Apps
- Structuring a clear status lifecycle for a business process
- Building automated email notifications with Power Automate
- Designing user-friendly screens for distinct tasks (submission, approval, history, correction)
- Implementing budget tracking and real-time calculations
- Designing a transparent, auditable process with full history tracking

## 20. Real-World Enterprise Use Cases

This pattern — submit, notify, approve or reject with feedback, notify again, and allow correction — applies broadly, including:

- **Expense and reimbursement management** — exactly as demonstrated here
- **Purchase or procurement requests** — routing spending requests for manager approval
- **Time-off and leave requests** — submitting, approving, and tracking employee leave
- **Document or contract approvals** — routing materials for sign-off with clear feedback on rejection
- **Any request-and-approval process** — where clear notifications, visible history, and correction paths improve both speed and trust

## 21. Lessons Learned

- Automatic notifications at both ends of a process (submission and decision) remove the single biggest source of delay: someone forgetting to follow up.
- Requiring a comment on rejection turns a rejection from a dead end into an actionable next step for the employee.
- Giving users a dedicated correction-and-resubmission path, rather than forcing a fresh submission, respects their time and keeps the process moving.
- Real-time budget visibility helps employees make better spending decisions before they submit a request, not just after.
- A well-designed, role-specific interface (separate views for employees and approvers) makes a shared process feel simple for everyone involved.

## 22. Possible Future Enhancements

- Add **multi-level approval** for expenses above a certain amount.
- Introduce **spending analytics**, showing trends in expense categories over time.
- Add **automatic policy checks**, flagging expenses that fall outside standard limits before submission.
- Integrate directly with **accounting or payroll systems** to streamline reimbursement once approved.
- Add **mobile-optimized submission**, allowing receipts to be captured directly from a phone camera.
- Extend notifications to **Microsoft Teams**, in addition to email, for faster visibility.
