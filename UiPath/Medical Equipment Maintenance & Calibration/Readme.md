# Medical Equipment Maintenance & Calibration

**Automation Playground Portfolio Project**

An automation that watches over a hospital's medical equipment inventory and proactively alerts the team whenever a piece of equipment is due or overdue, for maintenance or calibration. Built around a CMMS-style (Computerized Maintenance Management System) equipment dashboard, it turns a spreadsheet of maintenance dates into automatic, actionable email alerts.

## 1. Project Overview

This project automates the monitoring of maintenance and calibration schedules for medical equipment — the kind of critical hardware found in a hospital's radiology department, like CT scanners, MRI machines, X-ray units, and ultrasound machines. Instead of someone manually checking a spreadsheet or dashboard to see what's coming due, the automation checks every piece of equipment on its own and sends a clear, detailed email alert the moment something needs attention.

## 2. Business Context

Hospitals and clinics rely on a wide range of expensive, safety-critical equipment that must be regularly maintained and calibrated to stay safe and accurate. This isn't optional to missed maintenance on something like an X-ray machine or a CT scanner can mean regulatory issues, unreliable readings, or unsafe equipment. Facilities teams typically track this using a CMMS (Computerized Maintenance Management System) or a spreadsheet listing every asset, its last service date, and when it's next due.

## 3. Business Problem

Keeping track of maintenance schedules across many pieces of equipment is harder than it sounds:

- **It's easy to miss a due date** buried in a long spreadsheet or dashboard, especially across multiple departments or rooms.
- **Manual checking doesn't scale** — someone has to remember to look, and to look often enough to catch things before they become overdue.
- **Overdue equipment is a real risk** — in a healthcare setting, equipment that's overdue for calibration or servicing can affect patient safety and compliance.
- **There's no automatic accountability** — without a system flagging it, an overdue item can simply be missed until it causes a problem.

The business need was a way to continuously watch the equipment list and proactively flag anything due or overdue, without relying on someone remembering to check.

## 4. Project Objectives

- Automatically review the full medical equipment inventory on a regular basis.
- Check each item's maintenance and calibration due dates against the current date.
- Send a clear, detailed alert for any equipment that is due or overdue.
- Make sure every alert includes enough detail (location, serial number, manufacturer, notes) that someone can act on it immediately.
- Remove the need for manual spreadsheet-checking as the primary safety net.

## 5. What the Video Demonstrates

The video shows a **CMMS (Computerized Maintenance Management System) dashboard**, built as a web application, listing a hospital's radiology equipment, including a CT Scanner, MRI Machine, Digital X-Ray Machine, Portable X-Ray Unit, and Ultrasound Machine with details like location, serial number, manufacturer, last maintenance date, next maintenance date, status, and calibration due date.

It then shows the underlying **UiPath automation** running in Studio, which reads this same equipment data from a spreadsheet, checks each item's due dates, and automatically sends an email alert for every item that's due or overdue. The video's execution log shows the robot working through the equipment list, and the final part shows the resulting **inbox full of individual alert emails**, each one clearly named with the equipment ID and its due date (for an example, "RAD-001-05/05/2025 00:00:00 Is expired"), along with the full notification content with a table of the equipment's details and a clear call to action.

## 6. End-to-End Workflow, Step by Step

1. **Load the equipment inventory.** The automation reads the full list of medical equipment and their maintenance/calibration dates from the source data.
2. **Check each item, one at a time.** For every piece of equipment, the automation compares its next maintenance date and calibration due date against the current date.
3. **Identify items that are due or overdue.** Any equipment whose maintenance or calibration date has arrived or passed is flagged.
4. **Generate a detailed alert.** For each flagged item, the automation builds a notification containing the equipment's ID, name, location, serial number, manufacturer, maintenance history, and any existing notes.
5. **Send the alert automatically.** An email is sent immediately for each flagged item, so nothing waits for a person to notice it.
6. **Repeat across the full inventory.** The process continues through every item in the list, ensuring nothing is skipped.

## 7. Systems and Applications Involved

- **A CMMS-style equipment dashboard** (web-based) — the visual system of record for the equipment inventory
- **Microsoft Excel** — the underlying data source listing all equipment and their maintenance/calibration schedules
- **Microsoft Outlook** — used to send the automated maintenance and calibration alerts

## 8. Technologies Used

- **UiPath Studio** — used to build the monitoring and alerting automation
- **UiPath Excel Activities** — for reading the equipment data table
- **UiPath Mail Activities** — for composing and sending automated Outlook email alerts
- **Date/time comparison logic** — to determine whether a maintenance or calibration date is due or overdue
- **A Streamlit-based web dashboard** — providing a visual, browsable view of the same equipment data

## 9. Automation Logic

The core logic is straightforward but powerful: for every piece of equipment in the inventory, the automation converts its recorded maintenance and calibration dates into a proper date format, then compares them against today's date. If a date has been reached or already passed, that equipment is treated as needing attention, and a notification is generated and sent immediately. One email per equipment item, so each alert is specific and actionable rather than being buried in a long combined report. This item-by-item approach means the automation naturally scales to any size of equipment inventory without needing to be redesigned.

## 10. AI Capabilities

This project doesn't use AI. It is a rules based monitoring automation, and that's exactly the right tool for the job here. The value comes from **consistency and reliability**: the same check, applied to every single item, every time the automation runs, with nothing depending on a person remembering to look. It's a good example of how not every valuable automation needs AI. Sometimes dependable, rules-based logic applied consistently is the more appropriate (and more trustworthy) solution, especially in a safety-critical setting like healthcare equipment.

## 11. User Interactions

- The automation runs on its own — no one needs to trigger or watch it directly.
- The main way a team member interacts with the outcome is through their **email inbox**, receiving a clear, individual alert for each piece of equipment that needs attention.
- The CMMS dashboard remains available at any time for someone who wants to browse the full equipment list directly, but they don't need to check it proactively whereas the automation does that for them.

## 12. Inputs and Outputs

**Inputs:**
- The equipment inventory data: equipment ID, name, location, serial number, manufacturer, last maintenance date, next maintenance date, status, and calibration due date

**Outputs:**
- An individual email alert for every piece of equipment that is due or overdue for maintenance or calibration
- Each alert includes the equipment's full details and a clear call to action

## 13. Error Handling and Validation

- Dates from the source data are explicitly parsed into a proper date format before comparison, reducing the risk of a formatting issue causing a missed or incorrect alert.
- Because each equipment item is processed independently, one problematic record doesn't stop the rest of the inventory from being checked.
- The automation works directly from the same data that populates the CMMS dashboard, so the alerts and the dashboard reflect a single, consistent source of truth.

## 14. Business Rules

- Every piece of equipment must be checked against both its maintenance due date and its calibration due date.
- If either date is due or has already passed, an alert must be generated for that equipment.
- Each alert must include enough detail (location, serial number, manufacturer, and notes) for someone to act without needing to look anything up separately.
- Equipment that isn't due doesn't generate an alert and keeping notifications relevant and avoiding alert fatigue.

## 15. Key Features Demonstrated

- Automated, item-by-item review of a full equipment inventory
- Rules-based due-date and overdue-date detection
- Individualized, detailed email alerts rather than a single bulk report
- Integration between a data source, a visual dashboard, and an automated notification system
- A pattern suited to safety-critical, compliance-sensitive environments

## 16. Business Value and Benefits

- **Reduces risk.** Equipment maintenance and calibration issues are caught automatically, instead of depending on someone remembering to check.
- **Improves compliance posture.** Consistent, documented alerts make it easier to demonstrate that maintenance schedules are being actively monitored.
- **Saves staff time.** No one needs to manually scan the equipment list on a regular basis.
- **Improves patient safety indirectly.** Well-maintained, properly calibrated equipment is safer and more reliable for patient care.
- **Scales easily.** The same process works whether there are 5 pieces of equipment or 500.

## 17. Productivity Improvements

- Removes the need for manual, recurring reviews of the equipment maintenance spreadsheet or dashboard.
- Converts a passive dashboard (something someone has to remember to check) into an active alerting system (something that reaches out on its own).
- Frees up facilities and biomedical engineering staff to focus on responding to alerts rather than searching for them.

## 18. Time or Cost Savings (If Evident)

The video shows the automation working through roughly ten pieces of equipment in a single run, generating an individual alert for each one that was due or overdue. It doesn't demonstrate large scale figures like the total size of a real hospital's inventory or the cost of a missed maintenance event, so no specific dollar or hour savings number is claimed here. In a healthcare setting, the cost of a single missed piece of equipment maintenance, in compliance risk or safety terms can be significant, which is where this kind of proactive, no-effort monitoring delivers real value.

## 19. Skills Demonstrated

- Designing a rules-based monitoring and alerting automation
- Working with structured data from Excel as a source of truth
- Implementing date/time comparison logic for due-date tracking
- Automating detailed, individualized email notifications
- Understanding compliance and safety considerations in a healthcare automation context
- Connecting a data source, a dashboard, and an automated alerting layer into one coherent solution

## 20. Real-World Enterprise Use Cases

This same pattern applies to any scenario involving scheduled, must-not-miss actions across a list of assets or records, including:

- **Facilities and equipment maintenance** — in manufacturing, healthcare, or any asset-heavy industry
- **Compliance and certification tracking** — flagging licenses, permits, or certifications nearing expiry
- **Contract renewal monitoring** — alerting teams before vendor or customer contracts lapse
- **Software license and subscription tracking** — flagging renewals or expirations before they cause disruption
- **Vehicle fleet maintenance** — tracking service and inspection due dates across a fleet
- **Any scheduled, recurring compliance task** — where missing a date has real consequences

## 21. Lessons Learned

- Turning a passive dashboard into active alerts is often more valuable than the dashboard itself where visibility only helps if someone actually looks.
- Sending individual, detailed alerts (rather than one long combined report) makes each notification easier to act on immediately.
- Reliable date handling logic is a small but critical detail in any automation involving due dates, getting the comparison right is what makes the whole system trustworthy.
- Not every valuable automation needs AI for safety-critical, rules-based checks like this one, consistent, predictable logic is exactly what's needed.
- In regulated or safety-sensitive environments, automation isn't just about saving time,it's about reducing the risk of a costly or dangerous oversight.

## 22. Possible Future Enhancements

- Add **escalation logic** — if an alert isn't acknowledged within a set time, escalate it to a supervisor or send a follow-up reminder.
- Integrate directly with the **CMMS system** to automatically update equipment status once maintenance is completed.
- Add a **summary digest** alongside individual alerts, giving managers a quick overview of everything currently due or overdue.
- Include **severity levels**, so significantly overdue equipment is flagged more urgently than something just becoming due.
- Add **SMS or chat notifications** (in addition to email) for more urgent or safety-critical alerts.
- Build in **historical tracking**, so the team can see maintenance compliance trends over time, not just point-in-time alerts.
