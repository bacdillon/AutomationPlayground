# Agentic Orchestration: Invoice Processing with Human-in-the-Loop

This simple project shows how to automate invoice approval by combining RPA (robotic process automation), an AI agent that makes decisions, and a human reviewer who steps in only when needed. Simple invoices get approved automatically. Risky or unusual ones are sent to a person to check. Every invoice ends with a clear, tracked decision.

## 1. Project Overview

This project automates the process of approving vendor invoices. Instead of a person checking every single invoice, the system does most of the work on its own. It reads each invoice, decides if it looks normal or risky, and either approves it right away or sends it to a person for a final decision. 

## 2. Business Context

Companies receive invoices from vendors all the time. Most of these invoices are normal — same vendors, expected amounts, nothing unusual. But some invoices are different: maybe the amount is unusually high, or the vendor is new, or something doesn't match the company's rules. Businesses need a way to handle the normal invoices quickly, while still making sure a person reviews the ones that carry more risk.

## 3. Business Problem

Most companies handle invoice approval in one of two ways, and both have problems:

- **Reviewing everything by hand** — every invoice needs a person to look at it, even the simple, low-risk ones. This wastes time and slows the whole process down.
- **Approving everything automatically** — invoices get approved with no human check at all, which is risky. If a large or unusual invoice slips through, there's no one making sure it's correct.

Basic automation tools also struggle here, because they can only follow fixed rules. Teaching a bot every possible reason an invoice might be risky becomes complicated and hard to maintain. What's missing is a smart way to sort invoices — one that can make good judgment calls, but still lets a person step in for the cases that matter.

## 4. Project Objectives

- Automate the repetitive parts of invoice handling, like reading the file and pulling out the details.
- Use an AI agent to decide whether an invoice can be approved right away or needs a human to look at it.
- Make sure a person always reviews invoices that are flagged as risky. The AI never approves those on its own.
- Make sure every invoice ends in a clear result: approved or rejected, with a record of what happened.
- Show a real, practical way to combine automation, AI, and human oversight in one smooth process.

## 5. What the Video Demonstrates

The video shows the workflow running live in UiPath Studio, and it walks through two situations:

- A **normal invoice** that the AI agent checks and approves on its own, with no human involved.
- A **flagged invoice** one for $10,825 that goes over the spending limit, which the AI sends to a human for review. The video shows a reviewer opening the task in UiPath Action Center, reading the invoice details and the reason it was flagged, and then rejecting it.

The video also shows the behind-the-scenes view in UiPath Studio: the workflow diagram lighting up step by step as it runs, a log of each action (like the AI's decision and how long the human review took), and the invoice file being moved into an "Approved" or "Rejected" folder depending on the outcome.

## 6. End-to-End Workflow, Step by Step

1. **A new invoice comes in.** This starts the process.
2. **The system reads the invoice.** It pulls out key details like the vendor name, invoice number, date, and total amount.
3. **The AI agent checks it.** It looks at the details and decides: approve it, or send it for human review and it gives a reason for its decision.
4. **The process splits based on that decision.**
5. **If approved:** the invoice is marked approved and filed automatically. No person needs to do anything.
6. **If flagged:** a task is created for a human reviewer, showing the invoice details and why the AI flagged it.
7. **A person reviews it.** They read the summary, can add a comment, and choose to approve or reject it.
8. **The result is recorded.** Whether the AI or the human made the call, the invoice is filed as approved or rejected, and everything that happened is logged.

## 7. Systems and Applications Involved

- **UiPath Studio** — where the workflow is built, run, and monitored
- **UiPath Action Center** — where human reviewers see and complete their tasks
- **UiPath Apps** — the approval form reviewers use to approve or reject an invoice
- **Google Drive** — where invoices come in, and where approved/rejected files are stored

## 8. Technologies Used

- **UiPath Agentic Process (BPMN)** — the main workflow that ties everything together
- **UiPath AI Agent** — the AI component that makes the approve-or-escalate decision
- **UiPath RPA Workflow** — handles the mechanical steps, like downloading files and pulling out data
- **Data extraction** — turns the invoice file into usable, structured information
- **Google Drive integration** — used both to receive invoices and to store the final results

## 9. User Interactions

- When an invoice is flagged, a task shows up in the reviewer's **Action Center** inbox.
- The reviewer assigns the task to themselves and opens a simple **Approve or Reject** form. It already shows the invoice details and the reason it was flagged.
- The reviewer can type a comment before making their decision.
- Aside from this one review step, the whole process runs on its own, no manual data entry or sorting needed.

## 10. Inputs and Outputs

**Inputs:**
- The invoice file itself
- The business rules the AI uses to judge invoices (like a spending limit)
- Any comments the reviewer adds during their review

**Outputs:**
- A final decision for the invoice: approved or rejected
- The invoice file moved into the right folder based on that decision
- A full record of what happened, who or what made the decision, and why

## 11. Error Handling and Validation

- Every invoice has to pass through a decision step. There is no way for one to get stuck or skipped.
- The AI makes its decision based on the data pulled from the invoice, which lowers the chance of a bad decision from missing or broken information.
- UiPath Studio keeps a log of every step, including any errors, so issues can be found and fixed easily.
- The human review step itself acts as a safety net, any invoice the AI isn't confident enough to approve automatically always gets a second, human check before it's finalized.

## 12. Business Rules

- Invoices that meet normal conditions (within the spending limit, from a known vendor, etc.) can be approved automatically.
- Invoices that go over the set limit are always sent for human review. The AI is never allowed to auto approve those.
- Every flagged invoice must come with a clear reason, so the reviewer always knows why they're looking at it.
- Every invoice ends with one of two clear results, approved or rejected. There's no unclear or unfinished state.

## 13. Business Value and Benefits

- **Less manual work** — people only get involved when an invoice actually needs their judgment.
- **Stronger financial control** — risky invoices always get a human check, so nothing slips through.
- **Faster handling of exceptions** — reviewers get a clear summary instead of having to dig through the invoice themselves.
- **Better tracking** — every decision, whether made by AI or a person, is recorded with the reasoning behind it.
- **Easy to adjust** — if business rules change, the AI's criteria can be updated without rebuilding the whole workflow.

## 14. Productivity Improvements

- Cuts out manual review for the majority of invoices, which are usually routine and low-risk.
- Makes review faster for the invoices that do need attention, since the reviewer gets a ready-made summary instead of raw data.
- Removes manual filing and tracking the system handles that automatically based on the outcome.

## 15. Real-World Enterprise Use Cases

This same approach can be used for many other business processes, such as:

- **Expense report approval** — approve small, normal claims automatically, and send unusual ones to a manager
- **Purchase order approval** — route based on cost or vendor risk
- **Contract review** — flag unusual contract terms for a lawyer to check
- **Refunds and credits** — approve small amounts automatically, escalate larger ones
- **Loan or credit applications** — combine automated scoring with a required human check on edge cases
- **Compliance checks** — any process where most cases are simple, but some need a person to make the final call

## 16. Lessons Learned

- Giving an AI a narrow, well-defined job (like "approve or escalate") makes it much easier to trust than giving it broad decision-making power.
- Explaining *why* the AI made a decision is just as important as the decision itself, it's what makes human review quick and trustworthy.
- Human review steps work best when they're built directly into the workflow (tracked and logged), not handled through side channels like email.
- Designing a process so every case has to end in one of a few clear outcomes helps avoid confusing or "stuck" situations.
- Being able to see exactly what happened at each step (not just the final result) builds trust in the automation — people need to understand *why*, not just *what*.

## 17. Possible Future Enhancements

- Add a **confidence score** to the AI's decision, so it's easier to tell a clear case from a borderline one.
- Add a **second approval step** for very large invoices, so more than one person signs off.
- Give the AI more context, like a vendor's **history**, to make smarter decisions beyond just checking the amount.
- Add **notifications** (like Slack, Teams, or email) so reviewers don't have to keep checking their inbox manually.
- Build a **dashboard** that tracks how often the AI's decisions match what a human would decide, to help fine-tune it over time.
- Let human decisions **feed back into** the AI's rules, so it keeps improving as it sees more real cases.

