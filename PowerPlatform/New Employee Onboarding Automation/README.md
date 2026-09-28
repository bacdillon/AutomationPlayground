# New Employee Onboarding Automation

A Power Automate flow, "Create Onboarding Record," that turns a Microsoft Forms submission into an approval-driven onboarding process for a new hire. It records the hire in SharePoint, asks a manager to approve through Microsoft Teams, and then completes an approval path or a rejection path automatically.

## 1. Project Overview

This project automates the first stage of bringing a new employee into an organization, in this case "Pedal Paradise," a cycling club. Everything starts from a single online form. When it is submitted, the flow creates an onboarding record, requests a manager's approval, and carries out the correct follow-up steps based on the decision. The demonstration runs both outcomes end to end: one hire is approved and one is rejected.

## 2. Business Problem & Objectives

**The problem:** Onboarding involves many small steps that are easy to delay or forget: capturing the new hire's details, recording them centrally, getting sign-off, notifying the new employee, and flagging equipment needs. When this happens through scattered emails and manual data entry, details are retyped incorrectly, approvals sit unanswered, and there is no single place showing where each request stands. Rejected requests are especially easy to lose track of.

**The objectives:**
- Capture new hire details once, through a structured form.
- Automatically create a central record for every onboarding request.
- Route each request to an approver through Microsoft Teams.
- Handle both approval and rejection as designed outcomes.
- Keep the record's status and the approver's comments up to date automatically.

## 3. Solution

A Microsoft Forms form, "New Employee Onboarding," collects the employee name, personal email, job title, department (Training, Engineering, Research, or Marketing), start date, employment type (full-time or part-time), whether equipment is required, and optional notes. Submitting the form triggers a Power Automate flow that creates a record in the "Employee onboarding" SharePoint list and starts a Teams approval request: "[Name] is joining us on [date]. Please approve the onboarding process to start." The flow then follows one of two branches, depending on the decision.

### What the Video Demonstrates

**An approved hire.** Maria Garcia, a full-time UX/UI Designer in Research starting 1 October 2026, with equipment required. Her SharePoint record first shows "Pending approval." The manager approves in Teams with a comment ("Looking forward to starting. Need a second monitor if possible."), and the record updates to an onboarding-in-progress status with that comment stored. A welcome email to the new employee's personal address also appears in the mailbox.

**A rejected hire.** Aisha Khan, a part-time Marketing Analyst in Marketing, with no equipment required. The manager rejects the request with the comment "Position request declined per budget constraints / head-count hold." The record updates to "Rejected" with the comment stored, and an "Onboarding Rejected" email arrives stating: "The onboarding request for Aisha Khan is rejected. Here is the approver comments: Position request declined per budget constraints / head-count hold."

The flow's details page shows an automated flow triggered by Microsoft Forms, a successful run, and an average run duration of 1 minute 37 seconds, which includes the time spent waiting for the approver. The Teams Approvals history shows earlier requests with both Approved and Rejected outcomes.

### End-to-End Workflow, Step by Step

1. **A form is submitted.** The new hire's details are entered, with required fields and fixed choices.
2. **The flow starts.** Power Automate reads the new response.
3. **A record is created.** A new item is added to the SharePoint list with a status of "Pending approval."
4. **An approval is requested.** A Teams approval is sent to the manager.
5. **The manager decides.** They approve or reject and can add a comment.
6. **The outcome is checked.** An "Is Approved" condition splits the flow into two branches.
7. **If approved,** the flow creates an employee folder, emails the new hire, and checks whether equipment is needed. The record is updated with the new status and comments.
8. **If rejected,** the flow marks the record rejected, stores the comments, and sends the "Onboarding Rejected" email.

## 4. Solution Architecture & Technologies

- **Microsoft Forms**, the intake form that triggers the flow.
- **Microsoft Power Automate (cloud flow)**, orchestrating the process from the "When a new response is submitted" trigger through both branches.
- **Microsoft SharePoint (list)**, the "Employee onboarding" list on the Pedal Paradise site, holding the employee details, status, and approval comments.
- **Microsoft Teams Approvals**, delivering the request and capturing the decision.
- **Microsoft Outlook (email actions)**, sending the welcome and rejection emails.
- **Conditional logic**, an "Is Approved" condition, with a nested "Equipment is needed for new hire" condition inside the approval branch.

