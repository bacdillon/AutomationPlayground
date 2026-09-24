# Agentic Orchestration: Invoice Processing with Human-in-the-Loop

## 1. Overview

This automates the intake and approval of vendor invoices using UiPath's Agentic Automation platform. It combines three distinct capabilities in one governed workflow: deterministic RPA for data extraction, an AI agent that decides whether to approve or escalate an invoice, and a human-in-the-loop checkpoint (delivered through UiPath Action Center) for any invoice the AI isn't confident enough to clear on its own. Every invoice, whether resolved automatically or by a person, ends in a single, auditable outcome. The orchestration layer, a BPMN-based Agentic Process, coordinates all three components as one coherent process instead of three disconnected tools.

## 2. Business Problem & Objectives

**The problem:** Accounts payable teams process a constant stream of invoices. Most are routine and low-risk. A smaller subset is genuinely high-risk: unusual amounts, new vendors, or out-of-policy terms. Manually reviewing every invoice the same way wastes time on the easy cases, while fully automating approval removes the human accountability that finance controls require. Traditional rule-based RPA also struggles here, since encoding every possible reason an invoice should be escalated into if/else logic becomes brittle fast.

**The objectives:**
- Automate the mechanical work of retrieving and extracting invoice data, without manual effort.
- Let an AI agent make a single, bounded decision, approve or escalate, rather than the full approval call.
- Guarantee a mandatory human checkpoint for anything the agent flags, with no way to bypass it.
- Ensure every invoice reaches a clear, traceable outcome (auto-approved, human-approved, or rejected), with no ambiguous or dropped cases.

## 3. Solution

An **Agentic Process** built in UiPath Studio, using BPMN-based orchestration, wires together three types of automation:

- **Deterministic RPA**, which watches for new invoices and extracts their data.
- **An AI Agent ("Invoice Decision Agent")**, which evaluates the extracted data and decides whether to auto-approve or escalate for human review, always with a stated reason.
- **A human-in-the-loop task**, delivered through **UiPath Action Center**, which serves as the exception path. A reviewer sees the invoice details and the agent's stated reason, then clicks Approve or Reject.

Every path resolves into one of three outcomes, each reflected both in the process's execution log and in the invoice's physical location. The file is automatically moved into an "Approved" or "Rejected" folder in Google Drive, so status is visible without opening the automation tool at all.

### What the Video Demonstrates

The video shows two scenarios executing inside the live Agentic Process:

- A **routine invoice** that the Invoice Decision Agent evaluates and approves automatically. The file moves directly into the "Approved" Google Drive folder with no human involvement.
- An **exception invoice**, a $10,825 invoice from "Cookie Supply Co.," that the agent flags for review with the stated reason **"Over limit."** The demo shows the task appearing, unassigned, in UiPath Action Center. A reviewer assigns it to themselves, opens the "Approve or Reject" form showing the extracted invoice fields alongside the agent's reason for escalation, and clicks Reject. The workflow then automatically completes the loop: the invoice moves into the "Rejected" Google Drive folder and the execution trail marks the instance complete.

Throughout, UiPath Studio's debug and execution view is visible, showing the BPMN diagram highlighting live in green as each step completes, alongside a step-by-step execution trail (agent run, LLM call, model run, agent output, gateway decision, user task) and a global variables panel.

### End-to-End Workflow, Step by Step

1. **New Invoice Uploaded.** The process starts when a new invoice file lands in the monitored Google Drive folder.
2. **Download and Extract Invoice Details.** An RPA activity retrieves the file and extracts its structured data: vendor, invoice number, date, and total amount.
3. **Invoice Decision Agent.** The AI agent evaluates the extracted data against business criteria, such as spending thresholds, and outputs a decision, either Approve or Route to Review, along with a stated reason.
4. **Gateway: "Approve or Review."** The process branches based on the agent's decision.
5. **Auto-Approve path.** If cleared, the process sends an approval notification and moves the invoice into the "Approved" folder, with no human involvement.
6. **Review path.** If flagged, a task is created in UiPath Action Center containing the invoice details and the agent's reason for escalation.
7. **Human decision.** A reviewer opens the task, reads the summary and flag reason, optionally adds a comment, and clicks Approve or Reject.
8. **Second gateway: outcome routing.** The human's decision routes the process to the "Approve" endpoint (if approved on review) or the "Rejected" endpoint.
9. **Resolution.** The invoice file is moved into the corresponding Google Drive folder, and the process instance closes with a full execution log.

## 4. Solution Architecture & Technologies

- **UiPath Studio**, for Agentic Process (BPMN) design, orchestration, and live execution monitoring.
- **UiPath AI Agent**, the LLM-backed decisioning node embedded directly in the process ("Invoice Decision Agent").
- **UiPath RPA Workflow (XAML)**, powering the "Download and Extract Invoice Details" activity that retrieves and parses invoice data.
- **UiPath Action Center**, the human task inbox and approval interface used for escalated invoices.
- **UiPath Apps**, providing a purpose-built "Approve or Reject" form for reviewers.
- **Google Drive**, the storage system that both triggers the process when a new invoice is detected and receives the final outcome in the Approved/Rejected folders.

The BPMN diagram itself encodes the architecture as a strict state machine: New Invoice Uploaded flows to Download and Extract Invoice Details, then to the Invoice Decision Agent, then to a gateway ("Approve or Review"). From there the path leads either to Approve, or to Review as a human task, then through a second gateway to Approved or Rejected. Every path converges on exactly one of two terminal states. This orchestration layer, not any single tool, is what makes the RPA, AI, and human review function as one governed process instead of three separate, disconnected systems.

## 5. Controls & Validation

- **Bounded AI authority.** The agent can only choose between two outcomes, approve or escalate, never the final call on a flagged invoice. That decision always stays with a person.
- **Mandatory human review for flagged cases.** The gateway logic makes it structurally impossible for a flagged invoice to skip the Action Center review step.
- **Explainable escalation.** The agent's output includes a stated reason (for example, "Over limit") that's carried forward and shown directly to the human reviewer. The escalation is never a black-box flag.
- **Full runtime observability.** UiPath Studio's live execution trail shows every step of a run, including agent invocation, LLM call, model output, gateway decision, and the human task's duration, giving a transparent audit trail of exactly what happened and why, for both automated and human-made decisions.
- **State consistency.** Every invoice ends in exactly one of three terminal states, with its Google Drive location always matching its logged status, avoiding orphaned or ambiguous cases.

## 6. Business Value

- **Reduces manual triage load.** Routine, low-risk invoices require zero human involvement.
- **Preserves financial control.** High-value or anomalous invoices are reliably routed to a person, closing the compliance gap that pure automation would leave open.
- **Improves auditability.** Every decision, automated or human, is logged with a timestamp, a reason, and a final disposition.
- **Shortens cycle time on exceptions.** Reviewers get a pre-summarized approval form instead of digging through the original invoice themselves.
- **Scales without re-engineering.** Because judgment lives in an AI agent rather than a hardcoded rules engine, evolving criteria, such as adjusting spending thresholds, doesn't require rebuilding the workflow.

## 7. Skills Demonstrated

- Designing agentic processes that combine RPA, AI decisioning, and human oversight in one governed BPMN workflow.
- Configuring an AI agent with bounded, explainable decision authority.
- Building human-in-the-loop approval tasks with UiPath Action Center and UiPath Apps.
- Structuring a process as an explicit state machine to prevent silent failures or ambiguous outcomes.
- Using UiPath Studio's execution trail for runtime debugging and audit-level observability.

## 8. Enterprise Use Cases

This pattern generalizes well beyond invoice approval:

- **Expense report review.** Auto-approve routine claims, escalate outliers.
- **Purchase order approvals.** Route based on value or vendor risk.
- **Contract clause review.** Flag non-standard terms for legal review.
- **Customer refund or credit approvals.** Auto-clear small amounts, escalate large ones.
- **Loan or credit application triage.** Combine automated scoring with mandatory human sign-off on edge cases.
- **Compliance exception handling.** Any process where most cases are routine but a minority require accountable human judgment.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Scoping an AI agent's authority narrowly, to a single, bounded decision, makes agentic automation far easier to trust and govern than giving it broad discretion.
- Explainability isn't optional. Surfacing the agent's reasoning is what makes human review efficient and defensible.
- Human-in-the-loop steps should be modeled as first-class workflow nodes that are tracked, timed, and logged, not informal side channels like email.
- Structuring a process as an explicit state machine, with a fixed set of terminal outcomes, is a simple but effective way to prevent silent failures in automation.
- Naming the project around its orchestration layer, rather than the RPA component alone, more accurately reflects what makes the solution valuable: coordinating RPA, AI, and human review as one governed process, not any single piece in isolation.

**Future enhancements:**
- Add confidence scoring to the agent's output, so borderline cases can be weighted differently from clear-cut ones.
- Introduce multi-tier approval for very high-value invoices.
- Enrich agent context with vendor risk history to sharpen escalation criteria beyond amount thresholds.
- Add Slack, Teams, or email notifications alongside the Action Center task.
- Build an analytics dashboard tracking agent decisions versus human overrides over time.
