# Medical Equipment Maintenance & Calibration Tracking — RPA Automation

> Automating medical equipment maintenance/calibration due-date monitoring and alerting for a hospital biomedical asset register, using UiPath.

[![Status](https://img.shields.io/badge/status-pilot-yellow)]()
[![Platform](https://img.shields.io/badge/platform-UiPath-orange)]()
[![Docs](https://img.shields.io/badge/docs-complete-brightgreen)]()

---

## Overview

Hospitals must keep diagnostic equipment — CT scanners, MRI machines, X-ray units, ultrasound
machines, and similar assets — on schedule for preventive maintenance and calibration. Missing a
due date is a **patient-safety and regulatory compliance risk**.

This repository documents an RPA solution that replaces a manual, ad-hoc Excel review with a
scheduled **UiPath robot** (`sys_Asset Management_Track equipment maintenance schedules`) that:

1. Reads the equipment register (`Equipment_Maintenance.xlsx`)
2. Evaluates every record's maintenance and calibration due dates
3. Automatically emails a structured alert for every item that is due or overdue
4. Logs every check and every alert sent, for audit purposes

The equipment register is also visualized in a companion **CMMS Dashboard** (Streamlit) used by
biomedical staff for day-to-day visibility.

---

## Process at a Glance

| | As-Is (Manual) | To-Be (Automated) |
|---|---|---|
| **Trigger** | Ad hoc, staff-initiated | Fixed daily schedule (Orchestrator) |
| **Review** | Manual row-by-row date comparison | 100% rule-based coverage every run |
| **Notification** | Manually drafted, inconsistent | Auto-generated HTML email, standardized |
| **Audit trail** | None | Full execution log per run |
| **Effort to scale** | Increases with inventory | Constant |

Full detail: [`As-Is-Process.md`](./As-Is-Process.md) · [`To-Be-Process.md`](./To-Be-Process.md)

---

## Repository Contents

| # | Deliverable | File | Description |
|---|---|---|---|
| 1 | **As-Is Process** | [`As-Is-Process.md`](./As-Is-Process.md) | Current manual review & notification process, pain points |
| 2 | **To-Be Process** | [`To-Be-Process.md`](./To-Be-Process.md) | Automated process design, steps, benefits, future enhancements |
| 3 | **BPMN Workflow** | [`BPMN-Workflow.png`](./BPMN-Workflow.png) | Swimlane diagram: Scheduler → RPA Bot → Outlook → Biomedical Team |
| 4 | **Automation Opportunity** | [`Automation-Opportunity.md`](./Automation-Opportunity.md) | RPA suitability scoring, recommended approach, risks & impact |
| 5 | **PDD** | [`PDD.pdf`](./PDD.pdf) | Process Definition Document — business-level process spec |
| 6 | **SDD** | [`SDD.pdf`](./SDD.pdf) | Solution Design Document — technical implementation in UiPath |
| 7 | **Business Rules** | [`Business-Rule.md`](./Business-Rule.md) | BR-01 to BR-12 rule catalog + open items for sign-off |
| 8 | **Test Cases** | [`test cases.xlsx`](./test%20cases.xlsx) | 16 structured test cases across ingestion, rules, notification, exceptions |
| 9 | **Test Results** | [`test results.xlsx`](./test%20results.xlsx) | UAT execution results + Pass/Fail summary |
| 10 | **SOP** | [`sop.docx`](./sop.docx) | Standard Operating Procedure for running & supporting the robot |
| 11 | **User Guide** | [`User-Guide.docx`](./User-Guide.docx) | End-user guide for staff receiving alert emails |

---

## BPMN Workflow

![BPMN Workflow](./BPMN-Workflow.png)

The robot is triggered on a schedule, opens the Excel register, loops through every equipment
row, evaluates the due/overdue condition, and — where triggered — composes and sends an HTML
alert via Outlook, logging every step along the way.

---

## Solution Summary

| | |
|---|---|
| **Robot** | `sys_Asset Management_Track equipment maintenance schedules` |
| **Platform** | UiPath Studio / Robot / Orchestrator |
| **Dependencies** | `UiPath.Excel.Activities`, `UiPath.Mail.Activities`, `UiPath.System.Activities` |
| **Source of truth** | `Equipment_Maintenance.xlsx` (Sheet1) |
| **Notification channel** | Microsoft Outlook (HTML email) |
| **Schedule** | Daily, via Orchestrator time trigger |
| **Logging** | Write Line + Orchestrator execution log (audit trail) |

Full technical design, activity configuration, and exception handling: [`SDD.pdf`](./SDD.pdf).

---

## Business Rules (Summary)

| ID | Rule |
|---|---|
| BR-01 | Maintenance flagged Due/Overdue when `Next Maintenance` ≤ current date |
| BR-02 | Calibration flagged Due/Overdue when `Calibration Due` ≤ current date |
| BR-06 | Subject line format: `<Equipment ID>-<Due Date> Is expired.` |
| BR-11 | Every read and send action must produce a log entry |
| BR-12 | Robot runs on a fixed Orchestrator schedule (recommended daily) |

Full rule set and open items requiring business sign-off: [`Business-Rule.md`](./Business-Rule.md).

---

## Testing

- **16 test cases** covering data ingestion, rule evaluation, notification content/delivery,
  audit logging, exception handling, and performance — see [`test cases.xlsx`](./test%20cases.xlsx).
- **UAT pilot run results**: core scenarios (TC-01–TC-10, TC-15, TC-16) passed; exception-path
  scenarios (TC-11–TC-14) are scheduled for the next test cycle — see
  [`test results.xlsx`](./test%20results.xlsx).

---

## Operating & Using the Automation

- **Support staff / IT**: see [`sop.docx`](./sop.docx) for scheduled-run monitoring, manual
  triggering, and the exception escalation matrix.
- **Biomedical engineers / alert recipients**: see [`User-Guide.docx`](./User-Guide.docx) for
  how to read an alert email, what to do next, and how to use the CMMS dashboard.

---

## Known Limitations & Roadmap

- No "last notified" tracking in the pilot — an overdue item re-alerts on every scheduled run
  (see BR-07 in [`Business-Rule.md`](./Business-Rule.md)).
- No escalation workflow for unacknowledged alerts (planned enhancement).
- Excel remains the source of truth; a future phase may replace it with a direct CMMS/API
  integration.
- Additional channels (Teams/SMS) and automatic CMMS status updates are out of scope for the
  pilot — see [`Automation-Opportunity.md`](./Automation-Opportunity.md) §3 and
  [`To-Be-Process.md`](./To-Be-Process.md) §7.

---

## Stakeholders

| Role | Responsibility |
|---|---|
| Biomedical Engineering Lead | Process Owner |
| Biomedical Technicians | Maintain equipment register data |
| Biomedical Engineers | Receive alerts, schedule/perform maintenance |
| RPA Delivery Team | Build, test, deploy the automation |
| RPA Support / IT | Monitor scheduled runs, resolve exceptions |
| Compliance / Quality Team | Audit alert history |

---

## Document Status

All deliverables are **Draft v1.0**, pending business and compliance sign-off. See each
document's revision history for details.
