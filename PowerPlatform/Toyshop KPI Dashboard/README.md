# KiddyLah Toyshop KPI Report

An interactive Power BI Desktop dashboard built for a multi-location toy retailer, combining a portal-style landing page with a fully interactive KPI reporting page — enabling stakeholders to monitor orders, revenue, and profit by store location and drill into daily trends.

**Tech stack:** Power BI Desktop · DAX · Interactive Slicers · Drill-down Analytics

---

## Overview

This report was designed for **Kiddy Lah! Toy Shop**, a multi-location toy retailer, to give staff and stakeholders a single place to check on company mission/onboarding info alongside real-time sales performance. Rather than dropping users straight into raw charts, the report opens with a friendly, portal-style landing page before moving into the analytical KPI dashboard.

## Report Structure

The `.pbix` file contains 3 pages:

| Page | Purpose |
|---|---|
| **Intro** | Company landing page: welcome message, mission statement, and a Quick Access panel of internal links |
| **KPI Report** | Main analytical dashboard: KPI cards, category breakdown, and revenue trend with drill-down |
| **Duplicate of Page 1** | Work-in-progress / template copy of the Intro page |

---

## 1. Intro / Landing Page

The report opens on an **"Intro"** page styled as a company landing screen:

- **"Welcome to Kiddy Lah! Toy Shop"** header with mission statement
- A **Quick Access panel** of navigation shortcuts:
  - Employee Handbook
  - Product Details and SKUs
  - Week Reports
  - Store Directory
  - Request Time Off
  - Update Your Profile

This page functions like an internal portal front page rather than a typical chart-first BI report, orienting staff before they dive into the numbers.

## 2. KPI Report Page

The main **"KPI Report"** page includes:

- A **Store Location slicer** with four options: `Airport`, `Commercial`, `Downtown`, `Residential`
- Three headline **KPI cards**: Total Orders by Month, Revenue by Month, Profit by Month
- Supporting visuals:
  - Total Orders by Product Category
  - Revenue by Month (trend chart)

## 3. Interactive Filtering

All KPI cards and visuals are fully **cross-filtered** by the Store Location slicer. Selecting a store location dynamically updates every visual on the page:

| Filter | Orders | Revenue | Profit |
|---|---|---|---|
| **All stores** | 41,830 | $640,778 | $174,620 |
| Downtown | 2,907 | $49,024 | $12,357 |
| Residential | 24,927 | $377,080 | $101,506 |
| Commercial | 5,006 | $78,611 | $21,989 |
| Airport | 29,933 | $455,690 | $123,495 |

## 4. Drill-Down Interaction

The **Revenue by Month** chart supports drill-down analytics. Right-clicking a specific data point (e.g., Thursday, December 1, 2022 — Revenue $505,342) surfaces a **"Drill down"** context menu option, allowing users to move from monthly totals down to a specific day's revenue figure.

---

## Key Features

- ✅ Portal-style landing page for staff onboarding and navigation
- ✅ Real-time cross-filtering via Store Location slicer
- ✅ Drill-down from monthly to daily revenue detail
- ✅ Clean, stakeholder-ready KPI cards for at-a-glance performance monitoring

## Business Value

- Centralizes store performance monitoring (orders, revenue, profit) in a single self-service report
- Enables location-level comparison without manual data slicing in spreadsheets
- Reduces time-to-insight by surfacing daily-level detail on demand via drill-down, rather than requiring a separate report

---

## Notes

This project is part of a broader [Automation Playground](https://bacdillon.github.io/AutomationPlayground/) portfolio showcasing RPA, Power Platform, and BI solutions.
