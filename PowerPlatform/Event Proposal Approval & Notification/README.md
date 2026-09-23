# Event Proposal Approval & Notification

## Cross-Platform Event Approval and Notification Automation

> **Portfolio project summary:** A Microsoft Power Platform workflow that routes a newly submitted event proposal for approval, captures the decision, and communicates the approved result to the relevant team channel.

This description is based on the supplied automation demonstration video. It documents the behaviour visible in that recording and does not assume features that were not shown. [1]

## 1. Project Overview

**Event Proposal Approval & Notification
** is a low-code business process automation solution for managing event proposals at the fictional organisation, Pedal Paradise. A user submits event information through a Microsoft SharePoint list. Microsoft Power Automate then creates an approval request, waits for the approver's decision, evaluates the result, and posts an approved-status notification in Microsoft Teams.

The project demonstrates a practical approval pattern that combines a structured data source, a human decision point, automated notifications, and execution records. It is suitable for a GitHub portfolio because it shows both workflow configuration and the business process that the automation supports.

## 2. Business Context

Event activities can involve budgets, venue arrangements, participant numbers, external speakers, and supporting documents. These proposals often need formal approval before the wider team proceeds with planning or communication.

Without a central process, teams may rely on email chains, chat messages, and manual follow-ups. This makes it difficult to see the current status, confirm who approved the request, and maintain a reliable audit trail. The solution uses Microsoft 365 tools that many organisations already use to centralise the process.

## 3. Business Problem

The process addresses the risk that event proposals are submitted without a consistent approval route or visible status. Manual approval handling can cause delays, duplicated communication, incomplete records, and uncertainty for event coordinators.

The demonstrated workflow creates a controlled path from proposal submission to approval outcome. It also gives the approver a direct link to the proposal and makes the approved result visible to a defined Teams channel.

## 4. Project Objectives

- Centralise event proposal data in a SharePoint **Event Activities** list.
- Start an approval process automatically when a new proposal is created.
- Give the approver the information and record link needed to make a decision.
- Support a simple **Approve** or **Reject** response through Microsoft 365 approval channels.
- Apply decision logic based on the approval outcome.
- Notify the team when the demonstrated approval path is completed.
- Preserve execution evidence through Power Automate run history and approval outputs.

## 5. What the Video Demonstrates

The video shows an end-to-end test of the workflow using a sample proposal called **Bike Safety Inspection Day**. The proposal includes an event date, venue, participant count, external-speaker indicator, budget, submitter, proposal reference, and supporting safety guide.

It then shows the Power Automate flow configuration, the approval request in Outlook and Teams, the approver's approval action, the resulting Teams notifications, the SharePoint list status, and the successful Power Automate run. The final view inspects approval output data, including the responder, outcome, and completion date.

## 6. End-to-End Workflow Explained Step-by-Step

1. **A requester creates a new event proposal.** The requester adds event details to the SharePoint **Event Activities** list and provides the relevant proposal information.
2. **SharePoint triggers the automation.** The flow starts when a new list item is created in the configured Pedal Paradise SharePoint site.
3. **Power Automate creates an approval request.** The workflow uses the **Start and wait for an approval** action with the approval type **Approve/Reject – First to respond**.
4. **The approver receives the request.** The approval is visible through Microsoft 365 approval channels, including Outlook and Microsoft Teams. The request contains dynamic event information and a link to the SharePoint item.
5. **The approver reviews the proposal.** The demonstration opens the supporting safety guide and then records an approval response.
6. **The flow waits for the decision.** Power Automate does not continue past the approval action until a response is received.
7. **The flow evaluates the outcome.** A condition checks whether the approval **Outcome** equals **Approve**.
8. **The success path communicates the result.** For the approved test case, Power Automate posts a proposal notification and an **Approved** final-status message to the configured Microsoft Teams channel.
9. **The process is verified.** The recording shows the proposal in SharePoint, the approval status visible in the list, the Teams activity, and a successful flow run with inspectable output data.

## 7. Systems and Applications Involved

| System or application | Role in the process |
|---|---|
| **Microsoft SharePoint Online** | Stores event proposals in the **Event Activities** list and provides the submission interface. |
| **Microsoft Power Automate** | Orchestrates the trigger, approval request, condition logic, notification, and run monitoring. |
| **Microsoft Approvals** | Provides the human approve/reject decision experience. |
| **Microsoft Outlook** | Delivers an actionable approval email to the approver. |
| **Microsoft Teams** | Presents the approval request and receives workflow status messages in the configured channel. |
| **Adobe Acrobat Reader** | Opens the supporting safety guide reviewed during the demonstration. |

## 8. Technologies Used

- **Microsoft Power Platform**, primarily Power Automate.
- **SharePoint Online connector** for the new-item trigger and list integration.
- **Approvals connector/action** for the decision request and response capture.
- **Microsoft Teams connector/action** for channel notifications.
- **Microsoft 365 Outlook and Teams** as approval interaction channels.
- **Dynamic content tokens** to insert SharePoint values into approval details and notifications.
- **JSON run-output inspection** to validate captured approval data.

## 9. Automation Logic

The flow uses an event-driven design rather than a scheduled process. Its primary trigger is **When an item is created** for the SharePoint **Event Activities** list.

After the trigger, the workflow starts and waits for an approval. The approval request is configured for the first response and includes dynamic values such as the event/activity name, budget, event date, submitter, and a direct item link. A condition then compares the approval outcome with **Approve**. The approved test path posts messages to the selected Microsoft Teams channel, including the final approved status.

This structure separates the automated routing work from the human decision. The workflow automatically handles the repeatable steps, while the approver retains responsibility for the approval decision.

## 10. AI Capabilities

No custom artificial intelligence capability is used in the workflow shown. The flow is based on deterministic rules, Microsoft 365 connectors, dynamic content, and a human approval response.

Some Microsoft 365 interfaces may offer built-in features such as email summarisation, but the video does not show an AI action being configured or used in the automation logic. This is therefore an **RPA/low-code workflow automation project**, not an AI-enabled decision system.

## 11. User Interactions

The requester enters the event proposal into SharePoint and provides the required business details. The approver receives a request through Outlook or Teams, reviews the linked proposal and supporting document, and chooses **Approve** or **Reject**. The project team receives the approved-result notification in Teams.

User involvement is intentionally limited to the steps that require business judgement. Data routing, request creation, waiting, result evaluation, status communication, and run recording are automated.

## 12. Inputs and Outputs

| Category | Items demonstrated |
|---|---|
| **Inputs** | Event/activity name, event date, venue, number of participants, external-speaker indicator, budget, proposal reference, submitter, and supporting document. |
| **Trigger** | A new item created in the SharePoint **Event Activities** list. |
| **Decision input** | An approver's **Approve** or **Reject** response, with optional comments. |
| **Approval output** | The captured response includes the approver identity, outcome, response date, and completion date. |
| **Business outputs** | Approval request in Outlook and Teams; proposal record and visible approval status in SharePoint; approved-result messages in Teams. |
| **Operational output** | Power Automate run history and raw action output for audit and troubleshooting. |

## 13. Error Handling and Validation

The recording demonstrates **operational validation** rather than a full exception-management design. The completed run shows successful execution for the SharePoint trigger, approval action, condition, and Teams notification. The approval action output is also inspected to confirm that the responder, outcome, and completion date were captured.

The video does not show explicit retry policies, timeout escalation, reassignment, malformed-data handling, or a dedicated rejection-notification path. These should not be claimed as implemented. In a production version, these controls would be added according to the organisation's service-level requirements and governance rules.

## 14. Business Rules

The following rules are visible in the workflow configuration or test execution:

- A newly created SharePoint **Event Activities** item starts the flow.
- The approval uses **Approve/Reject – First to respond**.
- The request is sent to a configured approver.
- The approval details include relevant event values and a direct link to the SharePoint record.
- The flow continues only after an approval response is available.
- A condition checks whether the returned outcome equals **Approve**.
- The demonstrated approved path posts the proposal and final-status information to the configured Microsoft Teams channel.

The video includes existing rejected examples in the SharePoint list, but it does not demonstrate the automation steps taken for a rejection. The public documentation should therefore describe only the approved route as verified behaviour.

## 15. Key Features Demonstrated

- **Event-driven automation** that starts immediately after a new SharePoint record is created.
- **Structured request capture** through a business-focused SharePoint list.
- **First-response approval routing** through the Power Automate Approvals action.
- **Multi-channel approval access** through Outlook and Teams.
- **Dynamic content mapping** from SharePoint fields into the approval request.
- **Document-supported decision making** through the linked safety guide.
- **Outcome-based branching** using a condition on the approval response.
- **Teams-based status communication** for the approved test case.
- **Audit visibility** through SharePoint status, Power Automate run history, and raw approval outputs.

## 16. Business Value and Benefits

The solution provides a single, visible process for submitting and approving event proposals. SharePoint gives coordinators a central record, while Power Automate reduces the manual work required to send requests, chase responses, and communicate completed outcomes.

The workflow also improves accountability. It records the approval result and exposes run data that can be reviewed during support, process assurance, or audit activities. Teams notifications give the wider team timely visibility once the approval route is completed.

## 17. Productivity Improvements

The automation removes repeated administrative tasks that would otherwise be performed manually. These include preparing approval requests, copying event details into emails or chat messages, sending record links, monitoring for an answer, and informing the team after approval.

It also reduces context switching. Requesters work from SharePoint, approvers respond in their usual Microsoft 365 channels, and the team receives a single channel notification. This allows staff to focus on evaluating the proposal and planning the event rather than coordinating the process.

## 18. Time or Cost Savings

The demonstration does not include a measured baseline, process-volume data, labour rate, or formal time study. For that reason, this project does **not** claim a specific number of hours, percentage improvement, or cost saving.

The process has clear potential to save time by automating routing and stakeholder communication. A production business case could measure the average manual effort per proposal, approval turnaround time, number of follow-ups, and monthly proposal volume to calculate a defensible saving.

## 19. Skills Demonstrated

- Business process analysis and requirement translation.
- SharePoint list design for structured operational data.
- Power Automate cloud-flow design and configuration.
- Microsoft 365 connector integration.
- Approval workflow design and human-in-the-loop automation.
- Dynamic content mapping between systems.
- Conditional logic based on business outcomes.
- Teams notification design for stakeholder communication.
- Test execution, run-history review, and output validation.
- Clear separation between demonstrated functionality and production enhancement opportunities.

## 20. Real-World Enterprise Use Cases

This pattern can be adapted for many controlled business processes, including:

- **Event and marketing approvals:** Review budgets, venues, suppliers, and proposed attendance before promotion or booking.
- **Training requests:** Approve courses, certifications, workshop budgets, and participant allocations.
- **Procurement requests:** Route low-value purchase requests with quotation or supporting-document links.
- **Facilities and maintenance work:** Approve site activities, safety documentation, contractor access, and planned expenditure.
- **Project governance:** Review project-change requests, release activities, or funding requests before execution.
- **Human resources activities:** Route employee engagement events, training activities, or policy-related requests for management approval.

## 21. Lessons Learned

A strong workflow begins with a clear data model. The SharePoint list captures the business information required for the approver to make a decision, which reduces clarification requests later in the process.

Human approval should be embedded only where judgement is needed. In this design, the automation performs the consistent administrative work and pauses for the decision that requires accountability. Dynamic content and direct record links are important because they keep the approval request relevant and reduce manual lookup effort.

Finally, successful business automation needs observable execution. Reviewing run history and approval outputs validates the integration and supports later troubleshooting. The demonstration shows this practice by checking the completed action data rather than relying only on the visible notification.

## 22. Possible Future Enhancements

- Add a defined **rejection path** that updates the record, captures comments, and informs the requester.
- Update SharePoint approval status and approver comments explicitly within the flow for consistent lifecycle reporting.
- Add reminders, approval deadlines, escalation, and reassignment for overdue requests.
- Use rule-based routing for budget thresholds, event type, external speakers, or venue risk.
- Support multi-stage or parallel approval for high-value or high-risk proposals.
- Validate mandatory fields, budget values, dates, duplicate submissions, and required attachments before routing.
- Add failure notifications, retry policies, and a support queue for connector or delivery errors.
- Create Power BI reporting for proposal volume, approval turnaround time, approval outcomes, and bottlenecks.
- Apply environment variables, solution packaging, role-based access, and data-loss-prevention policies for enterprise deployment.
- Add document management controls, including versioning and retention for proposals and supporting evidence.

## References

[1]: file:///home/ubuntu/upload/NewEventActivitiesFlow.mp4 "NewEventActivitiesFlow — supplied Automation Playground demonstration video"
