# KiddyLah! Toyshop KPI Dashboard

An interactive Power BI dashboard built for a toy retail chain, "Kiddy Lah!," giving the business a clear, filterable view of sales performance, including orders, revenue, and profit, across its store locations and product categories. This project is a business intelligence and reporting piece, complementing the "Kiddy Lah!" inventory management system elsewhere in this portfolio.

## 1. Project Overview

This project is a multi-page Power BI report that turns raw sales data from a toy retail chain into a clear, interactive picture of business performance. It includes a branded introduction page, and a core KPI dashboard showing total orders, revenue, and profit, broken down by store location, product category, and month, with full drill-down and filtering built in.

## 2. Business Problem & Objectives

**The problem:** A retail chain operating multiple store locations, in this case Airport, Commercial, and Downtown stores, needs a clear, consolidated view of how each location and product category is performing. Without a shared dashboard, this kind of insight typically requires someone to manually pull and combine sales data, which is slow and makes it hard to spot trends or compare locations quickly. Sales data often lives in different places, making it hard to get a single, trustworthy view of overall performance. Building a performance summary by hand takes time and needs to be repeated every reporting period. Without an interactive tool, comparing store performance or seeing which product category drives the most orders requires manual data slicing, and gradual shifts, such as a slow month or a growing category, can go unnoticed without an easy way to look at performance over time.

**The objectives:**
- Consolidate sales data into a single, reliable reporting source.
- Present key performance indicators, orders, revenue, and profit, clearly and at a glance.
- Allow filtering by store location to compare performance across sites.
- Show trends over time, with the ability to drill into specific months.
- Break down performance by product category to highlight what's driving sales.
- Present the report in a clean, branded, easy-to-navigate format.

## 3. Solution

A Power BI report titled "KiddyLah Toyshop KPI Report" gives the business a self-service view of sales performance. A branded Intro page for "Kiddy Lah! Toy Shop," styled like an internal company hub, includes an About Us and Mission section along with quick-access links to team information, the handbook, time-off requests, the store directory, and weekly reports. The core KPI Report page presents headline KPI cards for Total Orders, Revenue, and Profit, a Store Location filter, a Total Orders by Product Category chart, and a Revenue by Month trend chart with interactive drill-down.

### What the Video Demonstrates

The Store Location filter, covering Airport, Commercial, and Downtown, instantly updates all figures on the page when a location is selected. The headline KPI cards update dynamically based on the selected filter, for example showing company-wide totals of roughly 29,933 orders, $455,690 in revenue, and $123,495 in profit, versus location-specific figures when a single store is selected. The Total Orders by Product Category chart shows which categories are driving order volume, and the Revenue by Month trend chart supports interactive drill-down, where hovering or clicking a point reveals the exact revenue for that specific date, including a detailed daily figure within a given month.

### End-to-End Workflow, Step by Step

1. **Open the report.** The user lands on a branded introduction page for the Kiddy Lah! Toy Shop.
2. **Navigate to the KPI dashboard.** The user moves to the main KPI Report page.
3. **Review headline metrics.** Total Orders, Revenue, and Profit are immediately visible as summary cards.
4. **Filter by store location.** Selecting a specific location, Airport, Commercial, or Downtown, updates every visual on the page to reflect that location's performance.
5. **Explore by category.** The Total Orders by Product Category chart shows which categories are contributing most to order volume.
6. **Explore trends over time.** The Revenue by Month chart shows the overall trend, and can be drilled into for a closer look at performance on a specific date.

## 4. Solution Architecture & Technologies

- **Microsoft Power BI Desktop**, used to build and present the report.
- An underlying **sales dataset** covering orders, revenue, profit, store locations, and product categories.
- **Power BI measures and calculations**, for computing Total Orders, Revenue, and Profit dynamically based on filter selections.
- **Interactive filtering and cross-highlighting**, so selecting a store location updates every visual on the page.
- **Drill-down enabled time-series charts**, allowing users to move from a monthly view down to a specific date.

While this project isn't a process automation in the RPA sense, it relies on automated calculation logic built into the Power BI data model. KPIs like Total Orders, Revenue, and Profit are defined once as measures and automatically recalculate based on whatever filters are applied, with no manual recalculation needed when switching between store locations or drilling into a specific month. This is what makes the dashboard genuinely interactive rather than a static report, since the same underlying logic serves every possible view of the data.
