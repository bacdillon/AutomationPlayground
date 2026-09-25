# Automated Ticket Management System

A Power Automate flow that watches an email inbox for incoming support and issue reports, and automatically turns every one into a tracked task in Microsoft Planner, with a summary posted straight to a Microsoft Teams channel, so nothing reported by email gets missed or has to be manually re-typed into a task board.

## 1. Project Overview

This project automates the first step of handling a support ticket: turning an incoming email report into a properly tracked task that a team can act on. A Power Automate flow, "MS Power Platform Ticket Issues Flow," monitors an Outlook inbox for issue emails, things like a broken approval workflow, a dashboard that won't load, or an app throwing an error, and for every one that arrives, it automatically creates a corresponding task in Microsoft Planner and posts a clear summary to a Teams chat, so the right people see it immediately.

## 2. Business Problem & Objectives

**The problem:** Support and IT teams often receive issue reports by email, a manager noticing a missing notification, an employee unable to submit a form, a dashboard failing to load. For these reports to actually get fixed, someone typically has to read the email, understand the issue, and manually create a task somewhere the team tracks work, like Microsoft Planner. This hand-off step is small but essential, and it's exactly the kind of repetitive administrative work that's easy to delay, forget, or do inconsistently. Emails can sit unread or unactioned, especially during busy periods, delaying the start of any real fix. Manually creating a task for every email is repetitive and takes time away from actually solving the reported issue. Details can be lost or altered when someone retypes an issue description into a task management tool instead of using the original wording, and team visibility depends on someone remembering to tell others a new issue has come in, rather than it being automatically surfaced.

**The objectives:**
- Automatically detect new issue-report emails as they arrive.
- Create a corresponding task in Microsoft Planner for every reported issue, without manual data entry.
- Preserve the original issue details (title, description, sender, priority) accurately in the created task.
- Notify the team immediately through a channel they already monitor, Microsoft Teams.
- Remove the manual hand-off step between "an issue was reported" and "the team is tracking it."

## 3. Solution

The "MS Power Platform Ticket Issues Flow" in Power Automate connects Outlook, Planner, and Teams into one automated hand-off. The flow's details page shows it is active and automated, and confirms it had run multiple times over the past week. When a new issue-report email arrives in the Outlook inbox, the flow reads the relevant information, the issue title, description, sender, and priority, creates a corresponding task in Microsoft Planner, and posts a summary to a Teams chat so the team sees it immediately.

### What the Video Demonstrates

Power Automate's built-in savings tracking estimates that, assuming 10 minutes saved per successful run, the flow had already saved 1 hour across 6 runs in the past week. The Outlook inbox shows a series of real issue-report emails arriving from different senders, including reports titled "Procurement Approval Email Missing," "Sales Dashboard Not Loading," "Leave Approval Workflow Not Triggered" (twice), "Unable to Submit Expense Claim in Expense App," and "Expense App Submission Error." Opening one such email, "Procurement Approval Email Missing," shows a support request from a manager, explaining that their procurement approval process isn't sending notification emails, and asking for the automation flow to be checked. Immediately after, a Microsoft Teams "Workflows" chat message appears, confirming: "A new task has been created in Microsoft Planner," followed by the full ticket details, Issue Title, Issue Description, Sender, and Priority (marked "high" in this case), along with a prompt to review and take action.

### End-to-End Workflow, Step by Step

1. **Monitor the inbox.** The flow watches the Outlook inbox for new incoming emails.
2. **Detect a new issue report.** When a new email arrives, the flow identifies it as a ticket to be processed.
3. **Extract the details.** The flow reads the relevant information from the email, the issue title, description, sender, and priority.
4. **Create a Planner task.** A new task is automatically created in Microsoft Planner, carrying over the extracted details.
5. **Notify the team.** A summary message is posted to a Microsoft Teams chat, presenting the same ticket details clearly and prompting the team to review and act.
6. **Repeat for every new email.** This process runs automatically each time a new issue-report email arrives, with no manual triggering required.

## 4. Solution Architecture & Technologies

- **Microsoft Outlook**, the inbox where issue-report emails are received.
- **Microsoft Planner**, where each reported issue becomes a trackable task.
- **Microsoft Teams**, where the team is notified of each new ticket.
- **Microsoft Power Automate**, the platform running the automated flow connecting all three.
- **An email trigger**, for detecting new incoming issue-report emails.
- **Planner "Create a task" action**, for automatically generating a tracked task from the email's details.
- **Microsoft Teams "Post message" action**, for notifying the team with a structured ticket summary.

The flow follows a simple but effective "listen and relay" pattern. It waits for a new email to arrive, pulls out the specific pieces of information needed, title, description, sender, priority, and pushes that same information into two different places a team already works from, a task board and a chat tool. Because the flow triggers directly off new emails rather than running on a schedule, there's no delay between an issue being reported and it becoming a visible, trackable task. The whole hand-off happens automatically and immediately. This project doesn't use AI. It's a straightforward, trigger-based automation, and its value comes from removing a manual, repetitive hand-off step entirely, ensuring every reported issue reliably becomes a tracked task without depending on someone remembering to create one.

## 5. Controls & Validation

- Because the flow is triggered directly by incoming emails, no ticket can be missed simply because no one checked the inbox in time.
- Carrying the original email's details directly into the Planner task avoids the risk of details being altered, lost, or mistyped during a manual hand-off.
- The flow's run history in Power Automate provides a clear, reviewable record of every ticket processed, supporting easy verification that the automation is working as intended.
- Every incoming issue-report email must result in a corresponding task being created in Planner, and a team notification must be posted for every new ticket, so visibility isn't dependent on someone checking Planner directly.

## 6. Business Value

- **Nothing gets missed.** Every issue-report email automatically becomes a tracked task, regardless of how busy the inbox is.
- **Faster response times.** The team is notified immediately, rather than whenever someone happens to check email.
- **Consistent, accurate task creation.** Every ticket is created the same way, with the same level of detail, every time.
- **Improved team visibility.** A shared Teams notification means the whole team sees new issues, not just whoever opened the email.
- **Reduced administrative burden.** No one needs to spend time manually converting emails into tasks.

## 7. Skills Demonstrated

- Building trigger-based (event-driven) automations in Power Automate.
- Integrating multiple Microsoft 365 tools (Outlook, Planner, Teams) into a single connected workflow.
- Extracting and mapping data from an email into a structured task.
- Designing automated notifications that give a team everything they need in one message.
- Reviewing and interpreting Power Automate's run history and built-in savings tracking.

## 8. Enterprise Use Cases

This "email in, task and notification out" pattern applies to a wide range of support and operational scenarios, including:

- **IT and business systems support**, as demonstrated here.
- **Customer service ticket intake**, converting customer emails into tracked support tickets.
- **Facilities or maintenance requests**, turning reported issues into actionable tasks.
- **HR case management**, automatically logging employee-submitted concerns or requests.
- **Any process where issues or requests arrive by email** but need to be tracked and actioned through a dedicated task management system.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Triggering directly off incoming emails, rather than checking on a schedule, ensures no delay between a report coming in and it becoming visible work.
- Pushing the same information into both a task board and a chat notification covers two different ways people actually keep track of work. Some check task lists, others check chat.
- Preserving original details, rather than requiring manual retyping, keeps the resulting task accurate and trustworthy.
- Power Automate's built-in savings estimates are a convenient way to demonstrate an automation's ongoing value without needing to build separate tracking for it.
- Even a simple, three-step automation, detect, create task, notify, can meaningfully improve how reliably a team responds to reported issues.

**Future enhancements:**
- Add automatic categorization or priority detection, analyzing the email's content to set the task's priority rather than relying on it being stated explicitly.
- Route tickets to different team members or Planner buckets based on the type of issue reported.
- Add acknowledgment emails, automatically replying to the sender to confirm their issue has been logged.
- Track resolution time, measuring how long it takes from ticket creation to task completion in Planner.
- Add escalation logic, flagging tickets that remain unresolved after a certain period.
- Expand the trigger source beyond email, allowing tickets to also be raised through a form or chat command.
