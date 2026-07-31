# Inventory Management System — "Kiddy Lah!"

**Automation Playground Portfolio Project**

A low-code inventory management solution built on the Microsoft Power Platform for a toy store ("Kiddy Lah!"). It tracks stock levels across product categories, and includes a formal, approval driven workflow for requesting more inventory to be complete with manager approvals delivered by email and Microsoft Teams, and a full audit trail of every request.

## 1. Project Overview

This project is a working inventory management system for a toy retailer, built using Microsoft Dataverse, Power Apps, and Power Automate. It tracks every item in stock  quantity, category, supplier, price, and the status. A dashboards to monitor inventory health at a glance. Beyond tracking, it includes a structured process for requesting additional stock: a request is submitted, automatically routed to a manager for approval by email or Teams, and the outcome is recorded and linked back to the original inventory item, creating a complete, traceable history.

## 2. Business Context

A retailer selling physical products. Toys across categories like LEGO playsets, soft toys, learning toys, and racing toys needs constant visibility into what's in stock, what's running low, and what needs to be reordered. Restocking decisions typically require a manager's sign-off, since they involve spending money and committing to supplier orders. Without a structured system, this process tends to happen informally through conversations, spreadsheets, or emails, with no consistent record of who requested what, when, or why.

## 3. Business Problem

Manually managing inventory and restock requests creates recurring issues:

- **Stock levels are hard to monitor at a glance** without a real information, visual view of what's low, out, or well-stocked.
- **Restock requests lack structure** informal requests (a message, a verbal ask) are easy to lose track of and don't leave a clear record.
- **Approvals get delayed or lost** when they depend on someone remembering to follow up, rather than being actively routed to the right person.
- **There's no traceability** connecting a restock request back to the specific inventory item, its outcome, and when it was approved.

## 4. Project Objectives

- Maintain an accurate, centralized record of all inventory items and their stock levels.
- Provide real time dashboards summarizing stock health across categories.
- Allow staff to formally request additional inventory when stock runs low.
- Route every request to a manager for approval automatically, without manual follow-up.
- Deliver approval requests through familiar channels such as email and Microsoft Teams, so managers can respond quickly.
- Maintain a complete, traceable history of every request and its outcome.

## 5. What the Video Demonstrates

The video walks through a Power Apps model driven application called **"Inventory Management System App,"** built for the "Kiddy Lah!" toy store, showing:

- An **Inventory Dashboard** with real time visuals: current stock by category, a quick stock status overview (In Stock / Low on Stock / Out of Stock), the top 5 items by stock level, and inventory breakdown by category.
- A detailed **Inventories** list showing every product the item name, price, current and initial quantity, description, supplier, category, items sold, and stock status for a real toy inventory including LEGO sets, plush toys, and learning products.
- The process of creating a **new Inventory Request** for a specific item (a LEGO set running low on stock), guided by a **Business Process Flow** with four clear stages: **Request → Approval → Inventory Check & Stock Update → Request Closure**.
- Triggering the approval process directly from the request record, which launches a **Power Automate flow** using the Approvals connector.
- The manager receiving the approval request both as a **Microsoft Teams notification** and an **Outlook email**, and approving it with a comment directly from either channel.
- The flow automatically updating the Dataverse record once approved, setting the approval date and marking the request status as **Approved**.
- An **Inventory Request Dashboard** summarizing request activity with status breakdown and request reasons (e.g., "Bundle promotion") — and the completed request appearing in the inventory item's own record, linked as part of its history.
- The **Power Automate run history**, showing past flow executions with their outcomes and durations, confirming the process runs reliably over time.

## 6. End-to-End Workflow, Step by Step

1. **Monitor stock via the dashboard.** Staff review the Inventory Dashboard to see current stock levels and identify items running low.
2. **Submit a restock request.** A new Inventory Request is created for the relevant item, specifying the quantity needed and the reason for the request.
3. **Enter the approval stage.** The Business Process Flow automatically advances the request to the Approval stage.
4. **Trigger the approval flow.** Running the linked Power Automate flow sends an approval request to the designated approver.
5. **Manager reviews and responds.** The approver receives the request by email and Teams, and approves or rejects it with an optional comment.
6. **The system updates automatically.** Once a decision is made, the flow updates the request record with the approval date and final status.
7. **Move to inventory check and closure.** The process flow advances to confirm the inventory update and close out the request.
8. **The full history is preserved.** The completed request remains linked to its original inventory item, viewable directly from that item's record.

## 7. Systems and Applications Involved

- **Microsoft Dataverse** — the underlying data platform storing inventory and request records
- **Power Apps (model-driven app)** — the main application interface for staff and managers
- **Power Automate** — the workflow engine running the approval process
- **Microsoft Approvals** — the connector handling approval requests and responses
- **Microsoft Outlook** — delivering approval requests and responses by email
- **Microsoft Teams** — delivering approval requests and responses via chat

## 8. Technologies Used

- **Microsoft Dataverse** — for structured data storage (Inventories and Inventory Requests tables)
- **Power Apps** — for the model driven application and dashboards
- **Power Automate (cloud flows)** — for the automated approval workflow
- **Business Process Flows** — for guiding users through a defined, staged process
- **Approvals connector** — for routing and capturing approval decisions
- **Native Dataverse charting** — for the dashboard visuals (stock levels, request status, category breakdowns)

## 9. Automation Logic

The heart of the system is the **Business Process Flow**, which enforces a consistent structure on every restock request: it must move through Request, Approval, Inventory Check & Stock Update, and Request Closure, in that order and there is no way to skip the approval step. When a request reaches the approval stage, a Power Automate flow is triggered that hands off the decision to a human approver through the Approvals connector, waiting for their response before continuing. Once approved, the flow writes the outcome directly back into Dataverse, updating the same record the request started from. The entire lifecycle of a request, from submission to decision, lives in one place rather than being scattered across emails or chat threads.

## 10. AI Capabilities

This project doesn't use AI. It is a structured, workflow driven business process built on low-code tools. Its strength lies in **process design**: routing the right decision to the right person, through the right channel, with a complete record kept automatically.

## 11. User Interactions

- Staff interact with the **Inventory Dashboard** to monitor stock and the **Inventories** list to review item details.
- Staff submit **Inventory Requests** through a guided, stage-based form when stock needs replenishing.
- Managers receive and respond to **approval requests** directly in their email inbox or Microsoft Teams where does not require to log into the inventory system just to approve a request.
- Anyone with access can review the **Inventory Request Dashboard** or an individual item's request history for full visibility into past and pending requests.

## 12. Inputs and Outputs

**Inputs:**
- Inventory item details (name, price, quantity, category, supplier, stock status)
- Restock request details: quantity needed, request reason, and the item being requested
- The approver's decision (approve/reject) and any comments

**Outputs:**
- An updated request record showing final status and approval date
- A live dashboard reflecting current stock and request activity
- A complete, linked history of every request tied to its original inventory item
- Approval notifications and responses delivered by email and Teams

## 13. Error Handling and Validation

- The **Business Process Flow** structurally prevents a request from skipping the approval stage. Every request must be reviewed before it can proceed.
- Required fields such as quantity needed and approver must be completed before a request can move forward, reducing the chance of incomplete requests.
- The Power Automate run history shows both successful and failed flow runs, giving visibility into any issues with the approval process itself, separate from the business data.
- Because approval decisions are captured directly through the Approvals connector, there's no ambiguity about who approved a request or when.

## 14. Business Rules

- Every restock request must go through a manager approval before being considered complete.
- A request must specify the quantity needed and a reason for the request.
- Once approved, the request's approval date and status must be recorded against that specific request.
- Every request must remain linked to its originating inventory item, preserving a full history per product.

## 15. Key Features Demonstrated

- A visual inventory dashboards (stock levels, category breakdown, top items, status overview)
- A structured, staged Business Process Flow for restock requests
- Automated approval routing through Power Automate and the Approvals connector
- Multi-channel approval delivery via email and Microsoft Teams
- Automatic record updates following an approval decision
- A dedicated Inventory Request Dashboard for tracking request activity
- Full request history linked directly to each inventory item
- Flow run history and reliability tracking

## 16. Business Value and Benefits

- **Clear visibility into stock health**, reducing the risk of running out of popular items or overstocking slow movers.
- **Faster approvals**, since managers can respond from their inbox or Teams without needing to log into a separate system.
- **Consistent process governance** every restock request follows the same structured path, with no steps skipped.
- **Full traceability**, with every request's history preserved and linked to the relevant inventory item.
- **Reduced administrative overhead**, since the system handles routing, tracking, and record-keeping automatically.

## 17. Productivity Improvements

- Removes the need for manual follow-up to get a restock request approved.
- Eliminates informal, hard-to-track requests made through ad hoc conversations or messages.
- Saves managers time by letting them approve requests from tools they already use daily (email, Teams).
- Gives staff instant visibility into stock status without needing to ask around or check manually.

## 18. Time or Cost Savings (If Evident)

The video shows a full restock request from submission to manager approval, completed in about one minute, with the approval itself taking under a second once the manager responded. It doesn't show large-scale, real-world request volumes or cost comparisons, so no specific dollar or hour savings figure is claimed here. Replacing informal, ad hoc restock requests with a structured, automatically routed approval process is a well-established way to reduce delays and administrative overhead in inventory heavy businesses.

## 19. Skills Demonstrated

- Designing a Dataverse data model for inventory and request tracking
- Building a model driven Power App with dashboards and structured forms
- Implementing a Business Process Flow to enforce a consistent, staged process
- Building a Power Automate flow using the Approvals connector
- Integrating approval workflows with Outlook and Microsoft Teams
- Designing a solution with full auditability and traceability built in
- Applying low-code/no-code tools to solve a real operational business process

## 20. Real-World Enterprise Use Cases

Track inventory, request more, route for approval, record the outcome, applies broadly, including:

- **Retail and warehouse inventory management** — tracking stock and managing restocking across product lines
- **Procurement and purchase request approvals** — routing spending requests to the right approver automatically
- **IT asset requests** — requesting and approving new equipment or software licenses
- **Facilities and supply requests** — managing and approving requests for office or operational supplies
- **Any process requiring a formal approval step** — where a decision needs to be made by a specific person, tracked, and recorded

## 21. Lessons Learned

- A **Business Process Flow** is a simple but effective way to enforce process discipline. It makes skipping a required step structurally difficult, not just discouraged.
- Delivering approvals through channels people already use (email, Teams) dramatically reduces friction compared to requiring a login to a separate system.
- Keeping a request's full history linked to its originating record (rather than in a separate log) makes historical review much more intuitive.
- Low-code platforms like Power Apps and Power Automate can deliver robust, auditable business processes without custom development.
- Visual dashboards, even simple ones, make a real difference in how quickly people can spot problems (like low stock) compared to scanning a raw data list.

## 22. Possible Future Enhancements

- Automatically **update stock quantities** once a restock request is fulfilled, closing the loop from approval to physical inventory.
- Add **low-stock triggers**, automatically generating a draft restock request when an item crosses a defined threshold.
- Introduce **multi-level approvals** for larger or higher-cost restock requests.
- Add **supplier integration**, allowing approved requests to generate a purchase order automatically.
- Build **historical trend reporting**, tracking how often specific items are requested and how quickly they're approved.
- Extend the Teams integration with **adaptive cards** for a richer in-chat approval experience.
