# Agentic RPA: Invoice Processing with Human-in-the-Loop

**Automation Playground Portfolio Project**

An agentic automation solution that combines RPA, an AI decision-making agent, and a governed human-in-the-loop checkpoint to automate vendor invoice approval — auto-clearing routine invoices while reliably escalating exceptions to a human reviewer.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Business Context](#2-business-context)
3. [Business Problem](#3-business-problem)
4. [Project Objectives](#4-project-objectives)
5. [What the Video Demonstrates](#5-what-the-video-demonstrates)
6. [End-to-End Workflow](#6-end-to-end-workflow-explained-step-by-step)
7. [Systems and Applications Involved](#7-systems-and-applications-involved)
8. [Technologies Used](#8-technologies-used)
9. [Automation Logic](#9-automation-logic)
10. [AI Capabilities](#10-ai-capabilities)
11. [User Interactions](#11-user-interactions)
12. [Inputs and Outputs](#12-inputs-and-outputs)
13. [Error Handling and Validation](#13-error-handling-and-validation)
14. [Business Rules](#14-business-rules)
15. [Key Features Demonstrated](#15-key-features-demonstrated)
16. [Business Value and Benefits](#16-business-value-and-benefits)
17. [Productivity Improvements](#17-productivity-improvements)
18. [Time or Cost Savings](#18-time-or-cost-savings-if-evident)
19. [Skills Demonstrated](#19-skills-demonstrated)
20. [Real-World Enterprise Use Cases](#20-real-world-enterprise-use-cases)
21. [Lessons Learned](#21-lessons-learned)
22. [Possible Future Enhancements](#22-possible-future-enhancements)

---

## 1. Project Overview

This project is a working demonstration of **agentic automation** applied to a core finance operations process: invoice approval. It combines three distinct automation paradigms — deterministic RPA, an AI decision-making agent, and a governed human-in-the-loop checkpoint — into a single orchestrated workflow built on UiPath's Agentic Automation platform.

The system watches for incoming invoices, extracts their data, and lets an AI agent decide whether each invoice can be approved automatically or must be escalated to a human reviewer. Every invoice resolves to a clear, auditable outcome, whether that decision was made by the AI or by a person.

## 2. Business Context

Accounts payable and procurement teams process a continuous stream of vendor invoices. The overwhelming majority are routine: known vendors, standard amounts, normal terms. A smaller but consequential subset carries elevated risk — unusually large amounts, unfamiliar vendors, or values outside a team's delegated approval authority. Organizations need a way to move fast on the routine cases while keeping firm human control over the exceptions, without forcing every invoice through the same slow, manual review process.

## 3. Business Problem

Invoice approval workflows commonly fail in one of two directions:

- **Over-reliance on manual review** — every invoice, regardless of risk, requires a person to open it, assess it, and approve it, creating unnecessary bottlenecks and reviewer fatigue.
- **Over-automation** — invoices are approved automatically without any risk-based judgment, removing the financial controls and accountability that audit and compliance functions require.

Traditional rule-based RPA struggles here too: encoding every nuance of "should this invoice be escalated?" into if/else logic becomes brittle and hard to maintain as business rules evolve. The core problem is the absence of a **scalable judgment layer** that can triage invoices intelligently while still keeping a human accountable for higher-risk decisions.

## 4. Project Objectives

- Automate the mechanical, repetitive parts of invoice intake and data extraction.
- Introduce an AI agent capable of making a bounded, explainable approve/escalate decision.
- Preserve a mandatory human checkpoint for any invoice the agent flags as higher-risk.
- Ensure every invoice — regardless of path — reaches a single, unambiguous, auditable outcome.
- Demonstrate an enterprise-viable pattern for combining RPA, AI agents, and human oversight in one governed process.

## 5. What the Video Demonstrates

The demonstration walks through the live execution of the workflow in UiPath Studio, covering both possible outcomes:

- A **routine invoice** that the AI agent evaluates and approves automatically, with no human involvement.
- An **exception invoice** (a $10,825 invoice flagged for exceeding a spending limit) that the agent routes to a human reviewer, who opens the task in UiPath Action Center, reviews the invoice summary and the agent's stated reason for escalation, and rejects it.

The video also shows the platform's execution trail — the live BPMN diagram, step-by-step run log (agent invocation, LLM call, decision output, gateway routing, human task duration), and the resulting file movement into "Approved" or "Rejected" storage folders — giving a transparent view into both the automation's logic and its runtime behavior.

## 6. End-to-End Workflow Explained Step-by-Step

1. **Trigger:** A new invoice is submitted into the monitored intake location, starting a new process instance.
2. **Extraction:** The invoice file is retrieved and its key fields (vendor, invoice number, date, total amount) are extracted into structured data.
3. **AI Evaluation:** The Invoice Decision Agent reviews the extracted data against business criteria and produces a decision — approve or escalate — along with a stated reason.
4. **Decision Gateway:** The process branches automatically based on the agent's output.
5. **Auto-Approval Path:** Cleared invoices are approved and filed without any human action.
6. **Escalation Path:** Flagged invoices generate a human review task containing the invoice summary and the agent's reasoning.
7. **Human Decision:** A reviewer evaluates the case and approves or rejects it, optionally adding a comment.
8. **Outcome Resolution:** Regardless of path, the invoice is filed into its final state (approved or rejected), and the complete decision trail — automated and human — is logged against the process instance.

## 7. Systems and Applications Involved

- **UiPath Studio** — process design, orchestration, and execution monitoring
- **UiPath Action Center** — human task management and approval interface
- **UiPath Apps** — purpose-built approval form for reviewers
- **Google Drive** — invoice intake source and outcome storage (Approved/Rejected folders)

## 8. Technologies Used

- **UiPath Agentic Process (BPMN)** — the orchestration backbone defining triggers, gateways, and task nodes
- **UiPath AI Agent** — an LLM-backed decisioning node embedded directly in the process
- **UiPath RPA Workflow (XAML)** — deterministic activities for file handling and data extraction
- **Structured data extraction** — converting unstructured invoice content into usable fields
- **Cloud file storage integration** — Google Drive as both trigger source and system of record for outcomes

## 9. Automation Logic

The workflow is architected as an explicit **state machine** with exactly three terminal outcomes for any invoice: auto-approved, human-approved, or rejected. This prevents ambiguous or "stuck" cases. The AI agent's role is deliberately scoped to a single, bounded decision — approve or escalate — rather than open-ended authority over the invoice lifecycle. Critically, the agent's output includes a **stated reason** for its decision, which is preserved and carried into the human review step, making the escalation explainable rather than a black-box flag.

## 10. AI Capabilities

- **Autonomous decisioning:** The AI agent independently evaluates extracted invoice data against business criteria without a human writing exhaustive rule trees.
- **Reasoned output:** The agent doesn't just classify the invoice — it articulates *why* it made its decision (e.g., "Over limit"), which is surfaced directly to the human reviewer.
- **Bounded autonomy:** The agent's authority is limited to routing, not final approval — it can clear a routine invoice, but cannot itself approve a flagged one; that decision stays with a person.
- **Runtime transparency:** The agent's reasoning steps (model call, decision output) are captured in the execution trail, supporting explainability and auditability.

## 11. User Interactions

- A reviewer receives a task in their **Action Center** inbox when an invoice is escalated.
- The reviewer assigns the task to themselves and opens an **Approve or Reject** form pre-populated with the invoice's key details and the agent's reason for flagging it.
- The reviewer can add a free-text comment before submitting their decision.
- Beyond this single review-and-decide interaction, the process runs unattended — no manual triage or data entry is required from the user.

## 12. Inputs and Outputs

**Inputs:**
- A vendor invoice file submitted to the monitored intake location
- Business rule parameters used by the AI agent (e.g., approval thresholds)
- Optional reviewer comments during human review

**Outputs:**
- A finalized invoice disposition: approved or rejected
- The invoice file relocated to the corresponding outcome folder
- A complete, timestamped execution log capturing the decision path (automated or human) and the stated reasoning

## 13. Error Handling and Validation

- The process is structured so every invoice must resolve through an explicit decision gateway — there is no path that leaves an invoice unclassified.
- Extracted invoice data feeds directly into the decision agent, reducing the risk of a decision being made on incomplete or malformed input.
- The runtime execution trail records failures, errors, and status at each step (visible in Studio's monitoring view), supporting troubleshooting and process auditing.
- The human review step itself acts as a validation layer — any invoice the AI agent is not confident enough to auto-approve is guaranteed a second, qualified assessment before being finalized.

## 14. Business Rules

- Invoices meeting standard criteria (e.g., within an approved spending threshold, from a recognized vendor) are eligible for automatic approval.
- Invoices exceeding defined thresholds are automatically escalated for mandatory human review — auto-approval is never available for out-of-policy amounts.
- Every escalation must include a stated reason, ensuring reviewers are never asked to evaluate a flagged invoice without context.
- Final disposition (approved/rejected) is binary and always explicitly recorded — there is no partial or indeterminate state.

## 15. Key Features Demonstrated

- End-to-end orchestration of RPA, AI decisioning, and human review in a single governed process
- Explainable AI escalation, with reasoning passed through to the human reviewer
- Real-time execution monitoring, including live BPMN status and step-level run logs
- Automated outcome routing and filing based on final disposition
- A dedicated, purpose-built approval interface for human reviewers

## 16. Business Value and Benefits

- **Reduced manual workload** — reviewers are only engaged for invoices that genuinely require judgment.
- **Maintained financial control** — high-risk invoices always receive human sign-off, preserving compliance posture.
- **Faster resolution of exceptions** — reviewers work from a pre-summarized case rather than raw invoice data.
- **Improved auditability** — every decision, automated or human, is logged with its rationale and outcome.
- **Adaptability** — evolving business criteria can be refined at the agent level rather than requiring a full workflow rebuild.

## 17. Productivity Improvements

- Eliminates manual triage for the (typically large) share of invoices that are routine and low-risk.
- Reduces the cognitive load on reviewers by presenting a synthesized case (data + reason) instead of a raw document to interpret from scratch.
- Removes manual file movement and status tracking — outcome-based filing happens automatically.

## 18. Time or Cost Savings (If Evident)

The demonstration shows the human review step completing in under a minute of active reviewer time once the task is opened, and the routine invoice path completing with zero human touch time. The video does not provide enterprise-scale volume or dollar figures, so no cost projection is claimed here — but the underlying mechanism (removing manual handling from the majority-routine invoice population while focusing review time only on genuine exceptions) is a well-established driver of measurable cycle-time and labor-cost reduction in accounts payable operations.

## 19. Skills Demonstrated

- Agentic process design and orchestration (BPMN-based)
- AI agent configuration and prompt/decision design for business decisioning
- RPA development for structured data extraction and file handling
- Human-in-the-loop workflow design, including task routing and approval UI
- Business rule translation into automated decision logic
- Solution architecture balancing automation, AI, and governance
- Process observability and debugging using platform execution tooling

## 20. Real-World Enterprise Use Cases

This pattern generalizes well beyond invoice approval, including:

- **Expense report review** — auto-approve routine claims, escalate outliers
- **Purchase order approvals** — route based on value or vendor risk
- **Contract clause review** — flag non-standard terms for legal review
- **Customer refund/credit approvals** — auto-clear small amounts, escalate large ones
- **Loan or credit application triage** — combine automated scoring with mandatory human sign-off on edge cases
- **Compliance exception handling** — any process where most cases are routine but a minority require accountable human judgment

## 21. Lessons Learned

- Scoping an AI agent's authority narrowly (a single, bounded decision) makes agentic automation far easier to trust and govern than giving it broad discretion.
- Explainability is not optional — surfacing the agent's reasoning is what makes human review efficient and defensible.
- Human-in-the-loop steps should be modeled as first-class workflow nodes (tracked, timed, logged), not informal side channels like email.
- Designing a process as an explicit state machine, with a fixed set of terminal outcomes, is a simple but effective way to prevent silent failures or ambiguous states in automation.
- Runtime observability (execution trails, live status) is as important to enterprise adoption as the automation logic itself — stakeholders need to trust *why* a decision was made, not just *what* it was.

## 22. Possible Future Enhancements

- Add **confidence scoring** to the agent's output to differentiate clear-cut decisions from borderline ones.
- Introduce **multi-tier approval** for very high-value invoices requiring more than one reviewer.
- Enrich agent context with **vendor risk history** to sharpen escalation criteria beyond simple thresholds.
- Add **proactive notifications** (Slack/Teams/email) so reviewers aren't dependent on manually checking their task inbox.
- Build an **analytics dashboard** tracking agent decisions versus human overrides, to monitor and continuously tune agent accuracy.
- Implement a **feedback loop** where review outcomes inform future agent decision criteria.

---

*This project was developed as part of an Automation Playground portfolio to demonstrate practical, governed agentic automation design — combining RPA, AI decisioning, and human oversight into a single enterprise-viable workflow.*
