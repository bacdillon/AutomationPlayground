# Inventory Management System: Kiddy Lah!

A complete, low-code inventory management solution built on the Microsoft Power Platform for a toy store, "Kiddy Lah!" It tracks stock levels across product categories, and includes a formal, approval-driven workflow for requesting more inventory, complete with manager approvals delivered by email and Microsoft Teams, and a full audit trail of every request.

## 1. Project Overview

This project is a working inventory management system for a toy retailer, built using Microsoft Dataverse, Power Apps, and Power Automate. It tracks every item in stock, including quantity, category, supplier, price, and stock status, and gives the business live dashboards to monitor inventory health at a glance. Beyond tracking, it includes a structured process for requesting additional stock: a request is submitted, automatically routed to a manager for approval by email or Teams, and the outcome is recorded and linked back to the original inventory item, creating a complete, traceable history.

## 2. Business Problem & Objectives

**The problem:** A retailer selling physical products, in this case toys across categories like LEGO playsets, soft toys, learning toys, and racing toys, needs constant visibility into what's in stock, what's running low, and what needs to be reordered. Restocking decisions typically require a manager's sign-off, since they involve spending money and committing to supplier orders. Without a structured system, this process tends to happen informally, through conversations, spreadsheets, or emails, with no consistent record of who requested what, when, or why. Stock levels are hard to monitor at a glance without a live, visual view of what's low, out, or well-stocked. Restock requests lack structure, and informal requests are easy to lose track of and don't leave a clear record. Approvals get delayed or lost when they depend on someone remembering to follow up, rather than being actively routed to the right person. There's also no traceability connecting a restock request back to the specific inventory item, its outcome, and when it was approved.

**The objectives:**
- Maintain an accurate, centralized record of all inventory items and their stock levels.
- Provide live dashboards summarizing stock health across categories.
- Allow staff to formally request additional inventory when stock runs low.
- Route every request to a manager for approval automatically, without manual follow-up.
- Deliver approval requests through familiar channels, email and Microsoft Teams, so managers can respond quickly.
- Maintain a complete, traceable history of every request and its outcome.

## 3. Solution

A Power Apps model-driven application, "Inventory Management System App," gives staff and managers a central place to track inventory and manage restock requests. An Inventory Dashboard provides live visuals of stock health, and a detailed Inventories list shows every product, including item name, price, current and initial quantity, description, supplier, category, items sold, and stock status. When stock runs low, staff create a new Inventory Request, guided by a Business Process Flow with four clear stages: Request, Approval, Inventory Check and Stock Update, and Request Closure. Triggering the approval process launches a Power Automate flow using the Approvals connector, which routes the decision to the relevant manager through both Microsoft Teams and Outlook.

### What the Video Demonstrates

The video walks through the full lifecycle of a restock request for a LEGO set running low on stock. The manager receives the approval request both as a Microsoft Teams notification and an Outlook email, and approves it with a comment directly from either channel. The flow automatically updates the underlying Dataverse record once approved, setting the approval date and marking the request status as Approved. An Inventory Request Dashboard summarizes request activity, including status breakdown and request reasons such as "Bundle promotion," and the completed request appears in the inventory item's own record, linked as part of its history. The Power Automate run history is also shown, displaying past flow executions with their outcomes and durations, confirming the process runs reliably over time.

### End-to-End Workflow, Step by Step

1. **Monitor stock via the dashboard.** Staff review the Inventory Dashboard to see current stock levels and identify items running low.
2. **Submit a restock request.** A new Inventory Request is created for the relevant item, specifying the quantity needed and the reason for the request.
3. **Enter the approval stage.** The Business Process Flow automatically advances the request to the Approval stage.
4. **Trigger the approval flow.** Running the linked Power Automate flow sends an approval request to the designated approver.
5. **Manager reviews and responds.** The approver receives the request by email and Teams, and approves or rejects it with an optional comment.
6. **The system updates automatically.** Once a decision is made, the flow updates the request record with the approval date and final status.
7. **Move to inventory check and closure.** The process flow advances to confirm the inventory update and close out the request.
8. **The full history is preserved.** The completed request remains linked to its original inventory item, viewable directly from that item's record.

## 4. Solution Architecture & Technologies

- **Microsoft Dataverse**, the underlying data platform storing inventory and request records.
- **Power Apps (model-driven app)**, the main application interface for staff and managers.
- **Power Automate**, the workflow engine running the approval process.
- **Microsoft Approvals**, the connector handling approval requests and responses.
- **Microsoft Outlook**, delivering approval requests and responses by email.
- **Microsoft Teams**, delivering approval requests and responses via chat.
- **Business Process Flows**, for guiding users through a defined, staged process.
- **Native Dataverse charting**, for the dashboard visuals covering stock levels, request status, and category breakdowns.

The heart of the system is the Business Process Flow, which enforces a consistent structure on every restock request. It must move through Request, Approval, Inventory Check and Stock Update, and Request Closure, in that order, with no way to skip the approval step. When a request reaches the approval stage, a Power Automate flow is triggered that hands off the decision to a human approver through the Approvals connector, waiting for their response before continuing. Once approved, the flow writes the outcome directly back into Dataverse, updating the same record the request started from, so the entire lifecycle of a request, from submission to decision, lives in one place rather than being scattered across emails or chat threads.

## 5. Controls & Validation

- The Business Process Flow structurally prevents a request from skipping the approval stage. Every request must be reviewed before it can proceed.
- Required fields, such as quantity needed and approver, must be completed before a request can move forward, reducing the chance of incomplete requests.
- The Power Automate run history shows both successful and failed flow runs, giving visibility into any issues with the approval process itself, separate from the business data.
- Because approval decisions are captured directly through the Approvals connector, there is no ambiguity about who approved a request or when.
- Every restock request must go through a manager approval before being considered complete, and every request must remain linked to its originating inventory item, preserving a full history per product.

## 6. Business Value

- **Clear visibility into stock health**, reducing the risk of running out of popular items or overstocking slow movers.
- **Faster approvals**, since managers can respond from their inbox or Teams without needing to log into a separate system.
- **Consistent process governance.** Every restock request follows the same structured path, with no steps skipped.
- **Full traceability**, with every request's history preserved and linked to the relevant inventory item.
- **Reduced administrative overhead**, since the system handles routing, tracking, and record-keeping automatically.

## 7. Skills Demonstrated

- Designing a Dataverse data model for inventory and request tracking.
- Building a model-driven Power App with dashboards and structured forms.
- Implementing a Business Process Flow to enforce a consistent, staged process.
- Building a Power Automate flow using the Approvals connector.
- Integrating approval workflows with Outlook and Microsoft Teams.
- Designing a solution with full auditability and traceability built in.
- Applying low-code and no-code tools to solve a real operational business process.

## 8. Enterprise Use Cases

This pattern, track inventory, request more, route for approval, record the outcome, applies broadly, including:

- **Retail and warehouse inventory management**, tracking stock and managing restocking across product lines.
- **Procurement and purchase request approvals**, routing spending requests to the right approver automatically.
- **IT asset requests**, requesting and approving new equipment or software licenses.
- **Facilities and supply requests**, managing and approving requests for office or operational supplies.
- **Any process requiring a formal approval step**, where a decision needs to be made by a specific person, tracked, and recorded.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- A Business Process Flow is a simple but effective way to enforce process discipline. It makes skipping a required step structurally difficult, not just discouraged.
- Delivering approvals through channels people already use, such as email and Teams, dramatically reduces friction compared to requiring a login to a separate system.
- Keeping a request's full history linked to its originating record, rather than in a separate log, makes historical review much more intuitive.
- Low-code platforms like Power Apps and Power Automate can deliver genuinely robust, auditable business processes without custom development.
- Visual dashboards, even simple ones, make a real difference in how quickly people can spot problems, such as low stock, compared to scanning a raw data list.

**Future enhancements:**
- Automatically update stock quantities once a restock request is fulfilled, closing the loop from approval to physical inventory.
- Add low-stock triggers, automatically generating a draft restock request when an item crosses a defined threshold.
- Introduce multi-level approvals for larger or higher-cost restock requests.
- Add supplier integration, allowing approved requests to generate a purchase order automatically.
- Build historical trend reporting, tracking how often specific items are requested and how quickly they are approved.
- Extend the Teams integration with adaptive cards for a richer in-chat approval experience.
