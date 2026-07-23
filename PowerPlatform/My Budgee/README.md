# My Budgee Expense Tracker

A self-service expense management app built on **Power Apps (Canvas)** with an integrated **Power Automate** approval workflow — enabling employees to submit and track personal/business expenses against a budget, while managers review, approve, or reject requests with full auditability.

**Tech stack:** Power Apps (Canvas App) · Power Automate · Outlook · Dataverse/SharePoint (data source)

## Overview

Manually tracking expenses via spreadsheets or email threads makes it hard to enforce budgets, chase down missing receipts, or keep a clear audit trail of who approved. **My Budgee Expense Tracker** solves this with a guided, receipt backed submission flow, automated email notifications for approvers.

## Solution Structure

| Component | Purpose |
|---|---|
| **Home Dashboard** (Requestor) | Budget progress tracking and quick-launch navigation |
| **Log New Expense** | Guided expense submission form with attachment support |
| **View Past Expenses / History** | Requestor facing status tracking |
| **Approval Expense Reporting** (Approver) | Manager review queue with filtering |
| **Approval Expense Reporting Details** | Decision screen with status, comments, and history |
| **Settings Management** (Approver) | Configurable overall budget cap |
| **Power Automate Flow** | Email notifications on submission and status change |

## 1. Home Dashboard (Requestor View)

The app opens on a dashboard showing:

- **Total Expense vs. Budget** progress bar (e.g., $720 / $1,500)
- **Remaining Amount**
- Quick-launch tiles: **Log Expense**, **View Past Expenses/History**

## 2. Submitting a New Expense

On the **"Log New Expense"** form, the user enters:

- **Date**
- **Category** (dropdown — Meal, Transportation, Accommodation, etc.)
- **Amount** and **Description**
- Auto-filled **Request By** (current user) and assigned **Approval By** (e.g., "Jack Black")
- An optional **file attachment** (e.g., a receipt)

Submitting shows a **"Submitted Successfully"** confirmation, and the new entry appears in **View Past Expenses** with status **Pending**.

## 3. Automated Approval Notification

A Power Automate flow sends an email via Outlook to the approver:

> **"Expense Approval Needed"** A new expense has been submitted for your approval, including the requestor's name and a link back to the Power Apps portal.

## 4. Approver Review

Logging in as the approver ("Jack Black"), the **Approval Expense Reporting** screen lists pending requests (e.g., Transportation $45, Meal $210). Opening a request's **Approval Expense Reporting Details** screen shows:

- Requestor's info
- Amount and description
- Attachments
- **Approval Information** section with Status dropdown, Comments field

## 5. First Decision — Rejection

The approver sets **Status: Rejected** with a comment (*"Receipt needed"*) and submits. This triggers a status-update email back to the requestor:

> "Expense Status has updated... please review it in the Power Apps portal."

The requestor's history list now shows **[Rejected]** for the affected entry.

## 6. Requestor Resubmission

The requestor opens the **"Edit Submitted Expense"** screen for the rejected item, uploads the missing receipt (a screenshot attachment), and clicks **Update** to resubmit with an **Approval History** timeline logging each status change with timestamps.

## 7. Second Decision — Approval

The approver reviews the resubmitted request (now with the attachment included), sets **Status: Approved** with the comment *"All good. Approved,"* and submits — triggering another status-update email to the requestor.

## 8. Final State & Admin Settings

- The requestor's **View Past Expenses** list now shows multiple entries as **Approved** (e.g., Accommodation $300, Accommodation $120, team dinner $210), reflecting the cumulative approved total.
- The approver's **Settings Management** screen allows configuring the overall **Budgeted Amount** (e.g., $2,000).
- The **Approval Reporting** screen includes a **Sort/Filter by status** (Pending, Approved, Rejected) dropdown.

## Key Features

- ✅ Budget-aware dashboard with real-time remaining balance
- ✅ Guided expense submission with receipt attachment support
- ✅ Automated approver notifications via Power Automate + Outlook
- ✅ Full reject-and-resubmit correction loop
- ✅ Timestamped Approval History for every decision
- ✅ Configurable organizational budget cap
- ✅ Status filtering (Pending / Approved / Rejected) for approvers

## Business Value

- Replaces manual, email-based expense approval with a governed, self service workflow
- Reduces approval turnaround time through automatic email routing to the assigned approver
- Improves compliance by requiring receipts before final approval, with a built in correction path for missing documentation
- Provides full auditability for every request, decision, comment, and timestamp is tracked end-to-end
- Gives budget owners real-time visibility into spend against a configurable budget cap
