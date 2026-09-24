# My Budgee: Expense Tracker & Approval App

A complete, low-code expense management app built on Microsoft Power Apps and Power Automate. "My Budgee" lets employees log expenses against a budget, routes each submission to a manager for approval automatically by email, and gives both employee and approver a full, transparent history of every request, including the ability to fix and resubmit a rejected claim.

## 1. Project Overview

This project is a working expense tracking and approval application, built for everyday business use. Employees log expenses, with amount, category, description, and a receipt attachment, against a running budget. Each submission automatically notifies the assigned approver by email, who can review and approve or reject it, with a comment, directly through the app. The employee is then notified of the outcome, and if a claim is rejected, they can see exactly why and correct it. Every step of this process, from submission to final decision, is tracked and visible.

## 2. Business Problem & Objectives

**The problem:** Almost every organization needs a way for employees to submit expenses, such as travel, meals, accommodation, and other work-related costs, and get them approved by a manager before reimbursement. This is a small but constant administrative process, and how well it's handled affects both employee experience and financial control. Done informally, through paper forms, email chains, or spreadsheets, it's slow and easy to lose track of. Submissions get lost or delayed, approvers aren't notified promptly so requests sit untouched, and rejected claims often lack clear feedback, leaving an employee unsure why a claim was turned down or what to fix. Employees may also have no real-time sense of how much of their budget they've already used, and there's typically no single, traceable history of a request's journey from submission to decision.

**The objectives:**
- Let employees easily log expenses with full details and supporting attachments.
- Show employees a live view of their budget: how much has been spent and how much remains.
- Automatically notify the correct approver whenever a new expense is submitted.
- Let approvers review, approve, or reject requests with comments, directly and quickly.
- Automatically notify employees of the outcome of their request.
- Allow employees to see rejection reasons clearly and correct and resubmit a claim.
- Maintain a full, visible history of every request's status and actions.

## 3. Solution

A Power Apps application, "My Budgee Expense Tracker," gives employees a Home screen showing their current budget status alongside a quick-access expense logging form. On the Log New Expense screen, a user enters the date, category, amount, and description, sees the approver automatically assigned, and can attach a supporting file before submitting. Submission triggers an automatic "Expense Approval Needed" email to the designated approver, who reviews the full request on the Approval Expense Reporting Details screen and sets a decision, Approved or Rejected, along with a comment. An automatic "Status for Expense Request" email is then sent back to the original requester, closing the loop.

### What the Video Demonstrates

The Home screen shows the current budget status, for example "$533.00 of $2,000.00" spent, with the remaining balance clearly shown. After a "Submitted Successfully" confirmation, the approver's Approval Expense Reporting screen lists all requests awaiting their decision, filterable and sortable by status and date, with a visible history log of each request's actions. On the employee side, the View Past Expenses screen shows their own submissions with clear status badges: Pending, Approved, Rejected. For a rejected claim, an Edit Submitted Expense screen shows the approver's comment and history, and allows the employee to attach the missing information, such as a receipt, and resubmit.

### End-to-End Workflow, Step by Step

1. **Check the budget.** The employee views their current budget status on the home screen before logging a new expense.
2. **Log a new expense.** The employee fills in the date, category, amount, and description, and attaches a supporting file if needed.
3. **Submit the request.** On submission, the app confirms success and records the expense with a "Pending" status.
4. **Notify the approver.** An automated email is sent to the assigned approver, alerting them that a new request needs review.
5. **Approver reviews the request.** The approver opens the request, reviews the details and attachment, and decides to approve or reject it, adding a comment if needed.
6. **Notify the employee.** An automated email is sent back to the employee, letting them know their request's status has been updated.
7. **Employee reviews the outcome.** The employee checks their past expenses list to see the final status and any comments.
8. **Correct and resubmit if needed.** If a claim was rejected, the employee can open it, review the reason, attach any missing information, and resubmit.

## 4. Solution Architecture & Technologies

- **Microsoft Power Apps**, the application employees and approvers use to log, review, and manage expenses.
- **Microsoft Power Automate**, the workflow engine sending automated email notifications.
- **Microsoft Outlook**, the channel through which approval and status notifications are delivered.
- **Power Apps (canvas app)**, for building the expense submission, approval, and reporting screens.
- **Power Automate (cloud flows)**, for triggering email notifications on submission and on status change.
- **A structured data source** behind the app, storing expense records, statuses, comments, and history.
- **File attachment handling**, for supporting receipts and other documentation.

The app is built around a clear status lifecycle: every expense starts as Pending, and can only move to Approved or Rejected through an explicit decision by the assigned approver, so there's no way for a request to be silently ignored or left in limbo. Two automated notifications anchor the process: one the moment a request is submitted, alerting the approver, and one the moment a decision is made, alerting the employee, meaning neither party ever has to manually check for updates. The app also keeps the full history of a request's status changes and comments attached to that same record, so context is never lost, even if a claim needs to be corrected and resubmitted.

## 5. Controls & Validation

- Every expense must move through a defined status lifecycle, Pending to Approved or Rejected, so a submission can't be lost or left unaddressed without a clear record.
- Rejections require a comment, ensuring the employee always receives specific, actionable feedback rather than just a rejected status with no explanation.
- The resubmission flow lets an employee directly address the stated issue, such as attaching a missing receipt, rather than starting over from scratch.
- Automated notifications remove reliance on either party remembering to check for updates manually.
- Every expense request must be routed to a specific, assigned approver, and a request must be explicitly approved or rejected. It cannot remain in limbo indefinitely.

## 6. Business Value

- **Faster approvals**, since approvers are notified immediately rather than needing to be chased.
- **Better employee experience**, with clear budget visibility and specific, actionable feedback on rejected claims.
- **Reduced administrative overhead**, since notifications, status tracking, and history are all handled automatically.
- **Stronger financial control**, with every expense requiring an explicit approval decision and a full audit trail.
- **Fewer repeated errors**, since employees can see exactly what needs fixing on a rejected claim rather than guessing.

## 7. Skills Demonstrated

- Designing a multi-role, employee and approver, business application in Power Apps.
- Structuring a clear status lifecycle for a business process.
- Building automated email notifications with Power Automate.
- Designing user-friendly screens for distinct tasks: submission, approval, history, correction.
- Implementing budget tracking and real-time calculations.
- Designing a transparent, auditable process with full history tracking.

## 8. Enterprise Use Cases

This pattern, submit, notify, approve or reject with feedback, notify again, and allow correction, applies broadly, including:

- **Expense and reimbursement management**, exactly as demonstrated here.
- **Purchase or procurement requests**, routing spending requests for manager approval.
- **Time-off and leave requests**, submitting, approving, and tracking employee leave.
- **Document or contract approvals**, routing materials for sign-off with clear feedback on rejection.
- **Any request-and-approval process**, where clear notifications, visible history, and correction paths improve both speed and trust.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Automatic notifications at both ends of a process, submission and decision, remove the single biggest source of delay: someone forgetting to follow up.
- Requiring a comment on rejection turns a rejection from a dead end into an actionable next step for the employee.
- Giving users a dedicated correction-and-resubmission path, rather than forcing a fresh submission, respects their time and keeps the process moving.
- Real-time budget visibility helps employees make better spending decisions before they submit a request, not just after.
- A well-designed, role-specific interface, with separate views for employees and approvers, makes a shared process feel simple for everyone involved.

**Future enhancements:**
- Add multi-level approval for expenses above a certain amount.
- Introduce spending analytics, showing trends in expense categories over time.
- Add automatic policy checks, flagging expenses that fall outside standard limits before submission.
- Integrate directly with accounting or payroll systems to streamline reimbursement once approved.
- Add mobile-optimized submission, allowing receipts to be captured directly from a phone camera.
- Extend notifications to Microsoft Teams, in addition to email, for faster visibility.
