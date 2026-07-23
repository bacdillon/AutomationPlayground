# Kiddy Lah! Inventory Management System

A Dataverse, backed inventory management solution for a multi-location toy retailer, built on **Power Apps (model-driven)**, **Microsoft Dataverse**, and **Power Automate** where enabling staff to monitor stock levels via live dashboards, raise restock requests through a guided approval process, and keep every request traceable back to the originating inventory item.

**Tech stack:** Power Apps (Model-Driven) · Microsoft Dataverse · Power Automate · Business Process Flows · Microsoft Teams Approvals · Outlook

## Overview

Retail staff at **Kiddy Lah! Toy Shop** need visibility into stock levels across categories, plus a reliable way to request and approve restocks before items run out. This solution centralizes inventory data in Dataverse, surfaces stock health through Power Apps dashboards, and automates the restock approval cycle end-to-end using a Business Process Flow and Power Automate. So a low-stock alert can become an approved restock request without leaving the app.

## Solution Structure

| Component | Purpose |
|---|---|
| **Inventory Dashboard** | Live stock analytics and category breakdowns |
| **Active Inventories** (table) | Master list of toy items with stock levels and status |
| **Inventory Requests** (table + BPF) | Guided restock request lifecycle with approval routing |
| **BPF Request Inventory Workflow** (Power Automate flow) | Automates approval notifications via Teams and Outlook |
| **Inventory Request Dashboard** | Reporting on request status and reasons |

## 1. Inventory Dashboard (Home)

The app opens on a Power Apps model-driven dashboard with live stock analytics:

- **Active Inventories** Counter
- **Stock Monitoring** Current Stock by Category chart
- **Quick Stock Status Overview** A pie chart (In Stock / Low on Stock / Out of Stock)
- **Top 5 Items with Highest Stock**
- **Inventory by Category** Breakdown

## 2. Browsing the Inventory List

The **"Active Inventories"** list is a Dataverse table of 22 toy items (e.g., LEGO Creator Tree House, LEGO Marvel Iron Man Mech, Cute Plush Dinosaur, Nerf Rival Blaster, Hot Wheels Monster Truck), with columns for:

- Price
- Current Quantity / Initial Quantity
- Supplier
- Category
- Items Sold
- Asset Number
- Computed **Stock Status** (In Stock / Low on Stock / Out of Stock)

## 3. Inspecting an Individual Item

Opening the record for **"LEGO Marvel Iron Man Mech"** shows:

| Field | Value |
|---|---|
| Initial Quantity | 40 |
| Current Quantity | 2 |
| Items Sold | 38 |
| Category | LEGO Playsets |
| Stock Status | Low on Stock |
| Supplier | LEGO Group |
| Price | $49.90 |

This low-stock item becomes the subject of the restocking request that follows.

## 4. Creating an Inventory Request (Business Process Flow)

A **New Inventory Request** is created in the "Inventory Requests" area, governed by a Dataverse **Business Process Flow (BPF)** with stages:

```
Request → Approval → Inventory Check & Stock Update → Request Closure
```

Fields captured:

- **Inventory:** LEGO Marvel Iron Man Mech
- **Quantity Needed:** 12
- **Request Reason:** "Bundle promotion"
- **Remarks:** "Franchise Promo"
- **Approver:** Manager

## 5. Triggering the Approval Flow

Saving the request and clicking **Run Flow** launches the **"BPF Request Inventory Workflow"** A Power Automate flow built on the **Standard Approvals connector**. The flow starts successfully and creates an approval task.

## 6. Approval Notification and Decision

The approval request is delivered two ways:

- A **Microsoft Teams Approvals** notification back to staff an Inventory Item has Request*
- An **Outlook email** with request details and a link back to the Dataverse record

The approver reviews and **approves** the request (comment: "approved"), confirmed by:

- An email response
- A Teams Approvals record showing **Final status: Approved**, with an option to save the approval as PDF

## 7. Flow Run Verification

The flow's run history in the **Power Automate portal** confirms a successful run, including the JSON response payload (responder ID, display name, email) from the Standard Approvals connector.

## 8. Record and Dashboard Updates

- The Inventory Request's BPF advances past the Approval stage, with Approval Date populated
- The **Inventory Request Dashboard** reflects the new request (Top 5 Request Status, Reason Distribution chart showing "Bundle promotion")
- The original **LEGO Marvel Iron Man Mech** inventory record shows the approved request linked in its related **Inventory Requests subgrid** closing the loop from low-stock item to submitted, approved restock request

## Key Features

- ✅ Real-time stock health dashboards (category, status, top items)
- ✅ Guided restock request submission via Business Process Flow
- ✅ Automated manager approval routing through Teams and Outlook
- ✅ Two-way traceability — requests link back to their originating inventory item
- ✅ Full flow run auditability via Power Automate run history

## Business Value

- Replaces manual stock checks and ad hoc restock requests with a governed, guided process
- Reduces approval turnaround time by routing requests directly to managers via Teams/Outlook instead of manual follow-up
- Improves auditability for every restock decision is timestamped, linked, and traceable back to the inventory record that triggered it
- Gives leadership real-time visibility into stock health and request trends without manual reporting
