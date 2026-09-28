# Medical Equipment Maintenance & Calibration Tracker

An automation that watches over a hospital's medical equipment inventory and proactively alerts the team whenever a piece of equipment is due, or overdue, for maintenance or calibration. Built around a CMMS-style (Computerized Maintenance Management System) equipment dashboard, it turns a spreadsheet of maintenance dates into automatic, actionable email alerts.

## 1. Project Overview

This project automates the monitoring of maintenance and calibration schedules for medical equipment, the kind of critical hardware found in a hospital's radiology department, such as CT scanners, MRI machines, X-ray units, and ultrasound machines. Instead of someone manually checking a spreadsheet or dashboard to see what's coming due, the automation checks every piece of equipment on its own and sends a clear, detailed email alert the moment something needs attention.

## 2. Business Problem & Objectives

**The problem:** Hospitals and clinics rely on a wide range of expensive, safety-critical equipment that must be regularly maintained and calibrated to stay safe and accurate. This isn't optional. Missed maintenance on something like an X-ray machine or a CT scanner can mean regulatory issues, unreliable readings, or unsafe equipment. Facilities teams typically track this using a CMMS (Computerized Maintenance Management System) or a spreadsheet listing every asset, its last service date, and when it's next due, but keeping track of maintenance schedules across many pieces of equipment is harder than it sounds. It's easy to miss a due date buried in a long spreadsheet or dashboard, especially across multiple departments or rooms. Manual checking doesn't scale, since someone has to remember to look, and to look often enough to catch things before they become overdue. Overdue equipment is a real risk in a healthcare setting, and without a system flagging it, an overdue item can simply be missed until it causes a problem.

**The objectives:**
- Automatically review the full medical equipment inventory on a regular basis.
- Check each item's maintenance and calibration due dates against the current date.
- Send a clear, detailed alert for any equipment that is due or overdue.
- Make sure every alert includes enough detail, location, serial number, manufacturer, notes, that someone can act on it immediately.
- Remove the need for manual spreadsheet-checking as the primary safety net.

## 3. Solution

A CMMS-style equipment dashboard, built as a Python and Streamlit web application, lists a hospital's radiology equipment, including a CT Scanner, MRI Machine, Digital X-Ray Machine, Portable X-Ray Unit, and Ultrasound Machine, with details like location, serial number, manufacturer, last maintenance date, next maintenance date, status, and calibration due date. Behind this dashboard, a UiPath automation reads the same equipment data from a spreadsheet, checks each item's due dates, and automatically sends an email alert for every item that's due or overdue.

### What the Video Demonstrates

The video's execution log shows the robot working through the equipment list, and the final part shows the resulting inbox full of individual alert emails, each one clearly named with the equipment ID and its due date, for example "RAD-001-05/05/2025 00:00:00 Is expired," along with the full notification content, a table of the equipment's details and a clear call to action.

### End-to-End Workflow, Step by Step

1. **Load the equipment inventory.** The automation reads the full list of medical equipment and their maintenance and calibration dates from the source data.
2. **Check each item, one at a time.** For every piece of equipment, the automation compares its next maintenance date and calibration due date against the current date.
3. **Identify items that are due or overdue.** Any equipment whose maintenance or calibration date has arrived or passed is flagged.
4. **Generate a detailed alert.** For each flagged item, the automation builds a notification containing the equipment's ID, name, location, serial number, manufacturer, maintenance history, and any existing notes.
5. **Send the alert automatically.** An email is sent immediately for each flagged item, so nothing waits for a person to notice it.
6. **Repeat across the full inventory.** The process continues through every item in the list, ensuring nothing is skipped.

## 4. Solution Architecture & Technologies

- **A CMMS-style equipment dashboard** (web-based), the visual system of record for the equipment inventory.
- **Python**, the language used to build the CMMS dashboard.
- **Streamlit**, the Python framework powering the CMMS dashboard's web interface.
- **Microsoft Excel**, the underlying data source listing all equipment and their maintenance and calibration schedules.
- **Microsoft Outlook**, used to send the automated maintenance and calibration alerts.
- **UiPath Studio**, used to build the monitoring and alerting automation.
- **UiPath Excel Activities**, for reading the equipment data table.
- **UiPath Mail Activities**, for composing and sending automated Outlook email alerts.
- **Date and time comparison logic**, to determine whether a maintenance or calibration date is due or overdue.

The core logic is straightforward but powerful. For every piece of equipment in the inventory, the automation converts its recorded maintenance and calibration dates into a proper date format, then compares them against today's date. If a date has been reached or already passed, that equipment is treated as needing attention, and a notification is generated and sent immediately, one email per equipment item, so each alert is specific and actionable rather than being buried in a long combined report. This item-by-item approach means the automation naturally scales to any size of equipment inventory without needing to be redesigned.

