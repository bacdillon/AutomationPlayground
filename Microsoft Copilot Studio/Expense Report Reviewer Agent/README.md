# Expense Report Reviewer Agent

An AI agent, deployed directly inside Microsoft Teams, that reviews an uploaded expense report the way a careful finance reviewer would: checking for duplicate charges, verifying that each expense is coded to the right accounting category, and producing a clear summary of what needs to be fixed before the report goes to a manager for approval.

## 1. Project Overview

This project is a working AI reviewer for expense reports. An employee simply uploads their expense spreadsheet into a Microsoft Teams chat, and the agent reads it, checks it for common problems, duplicate entries and incorrectly coded expenses, and responds with a clear, itemized summary explaining exactly what's wrong and what to do about it. It doesn't just flag issues. It reasons through each expense the way a person would, considering what kind of business a vendor actually is before deciding whether its accounting code makes sense.

## 2. Business Problem & Objectives

**The problem:** Expense reports are a routine but error-prone part of business travel and reimbursement. Employees fill them out, often assigning accounting codes themselves, and a finance or manager reviewer is expected to catch mistakes before approving payment. With dozens of line items per report and many reports to review, small errors, a duplicated charge, a grocery purchase coded as "office supplies," are easy to miss, but they add up in cost and in the effort needed to correct them later. Duplicate entries are easy to overlook in a long list of expenses, especially when they're not exact copies. Accounting code mistakes require judgment, not just rules, since knowing that a supermarket purchase is more likely a meal-related expense than "office supplies" takes actual reasoning about what kind of business a vendor is, not a simple lookup. Reviewers spend time on routine checking that could be better spent on genuinely ambiguous or high-value cases, and employees don't get fast, specific feedback, so errors often aren't caught until later in the approval chain, creating rework and delay.

**The objectives:**
- Let employees submit an expense report simply by uploading it into a chat conversation.
- Automatically detect duplicate expense entries.
- Automatically review whether each expense is coded to the correct accounting category, using reasoned judgment rather than rigid rules.
- Clearly explain any issues found, with specific, actionable guidance.
- Produce a clean summary report that speeds up the human approval step, rather than replacing it.

## 3. Solution

The "Expense Report Reviewer Agent," deployed inside Microsoft Teams, greets the user and asks them to upload their expense report. Once the user shares an Excel file, "Travel Expenses Report," directly into the chat, the agent confirms it's reading the report, then announces it will perform a few checks to see if there are any errors. It runs two distinct checks: scanning all expense entries for likely duplicates, matching vendor, amount, and closely related dates, and evaluating each expense's assigned accounting code by reasoning about what the vendor actually is, rather than applying a rigid lookup table.

### What the Video Demonstrates

The agent identifies a duplicate expense: two "Singapore Airlines" charges of $850.00 each, on consecutive dates, and asks the user to confirm whether these were genuinely two separate flights or an accidental duplicate submission. It works through all 12 expense line items one by one, restaurants, taxis, hotels, flights, and a supermarket purchase, reasoning about what type of business each vendor is and whether its assigned accounting code makes sense. It correctly identifies one misclassified item, a $999.99 purchase at a grocery store (NTUC FairPrice) coded as "Office Supplies," which the agent reasons should instead be coded as "Meals & Entertainment," explaining its reasoning in the process. The agent produces a final review summary: the employee's name, submission date, total amount, a table of duplicate items found, a table of misclassified items found with the current and corrected codes, and confirmation that all other items were reviewed and found correct, closing with a recommendation to fix the flagged items before submitting the report for manager approval.

### End-to-End Workflow, Step by Step

1. **Start the conversation.** The user opens a chat with the agent, which asks them to upload their expense report.
2. **Upload the report.** The user shares their expense report file directly in the chat.
3. **Read the report.** The agent confirms it has received and is reading the file.
4. **Check for duplicates.** The agent scans all expense entries for likely duplicate charges and flags any it finds.
5. **Review each expense's classification.** The agent goes through every line item, reasoning about whether its assigned accounting code is appropriate given the type of vendor and expense.
6. **Flag misclassified items.** Any expense coded incorrectly is identified, along with the corrected code and an explanation.
7. **Summarize the findings.** The agent presents a clear, structured summary covering duplicates, misclassifications, and confirmation that everything else was reviewed and found correct.
8. **Recommend next steps.** The agent advises the employee to resolve the flagged issues before the report goes to their manager for approval.

## 4. Solution Architecture & Technologies

- **Microsoft Teams**, the chat interface where the employee interacts with the agent and uploads their report.
- **Microsoft Excel**, the format of the submitted expense report.
- **An AI agent platform** (consistent with Microsoft Copilot Studio, based on its behavior and integration style), powering the agent's reasoning and Teams integration.
- **A large language model**, providing the reasoning needed to evaluate whether an expense's accounting code genuinely fits the nature of the vendor, not just a keyword match.
- **File upload and document reading capability**, allowing the agent to ingest and interpret an Excel expense report shared in chat.
- **Structured response formatting**, presenting findings as clear tables and summaries rather than unstructured text.

The agent's core logic runs two distinct checks against the uploaded report, then consolidates everything into one clear summary, explicitly separating "duplicates" from "misclassifications" and confirming which items had no issues at all, so the reviewer's attention goes exactly where it's needed. Its AI capabilities include judgment-based classification review, reasoning about the nature of each business rather than matching against a fixed rule table, duplicate detection with human-in-the-loop confirmation rather than unilateral deletion, document understanding to extract vendor, date, amount, and accounting code from a real-world spreadsheet, and structured, decision-ready output organized to support a fast approval decision.