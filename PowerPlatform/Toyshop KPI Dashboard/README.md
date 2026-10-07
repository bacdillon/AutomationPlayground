# KiddyLah! Toyshop KPI Report

## 1. Project Overview

This project is an interactive KPI report for **Kiddy Lah! Toy Shop**, built in Power BI. It summarizes the shop's sales performance in one view, showing total orders, revenue and profit, how orders split across product categories, and how revenue has moved month by month. A store location filter lets users compare performance across different store types.

* **Use case:** Monitoring retail sales performance across store locations and product categories
* **Intended audience:** Toy shop managers and staff who review sales results
* **Main technologies:** Microsoft Power BI Desktop (report pages, KPI cards, slicer, bar and line charts, measures)

## 2. Business Problem & Objectives

### Problem

Sales data on its own does not give managers a quick answer to questions like "How are we doing this month?" or "Which store type and product category contribute most?" Without a summary view, these answers have to be pulled together by hand, and comparing store locations takes extra effort.

### Objectives

* Present the shop's headline KPIs (orders, revenue and profit) at a glance
* Show which product categories drive the most orders
* Show how revenue changes over time
* Let users filter every view by store location
* Give the report a branded, easy-to-read front page

## 3. Solution

The report has a branded **Intro** page and a **KPI Report** page.

* **Intro page:** A Kiddy Lah! Toy Shop welcome page with the shop's mission statement and a Quick Access panel (Our Team, Retail associate handbook, Request time off, Store directory, Upcoming training, Product details and SKUs, Weekly reports, Update your profile).
* **KPI Report page:**
  * **KPI cards** for Total Orders, Revenue and Profit, each shown over a background trend chart by month
  * **Store Location slicer** with Airport, Commercial, Downtown and Residential options
  * **Total Orders by Product Category** bar chart covering Toys, Games, Art & Crafts, Sports & Outdoors and Electronics
  * **Revenue by Month** line chart from January 2022 to 2023, with tooltips showing the revenue for each month

### End-to-End Workflow

1. **Open the report:** The user starts on the Intro page and moves to the KPI Report page.
2. **Review headline KPIs:** With no filter applied, the cards show totals across all stores (for example, 41,830 orders, $640,778 revenue and $174,620 profit).
3. **Filter by store location:** The user selects one or more store locations. All cards and charts update together to show only those stores. For example, Downtown and Residential together show 29,933 orders and $455,690 revenue.
4. **Compare categories:** The bar chart shows which product categories bring in the most orders for the selected stores.
5. **Explore trends:** The user hovers over the revenue line to see the exact revenue for a given month and spot peaks and dips.

## 4. Solution Architecture & Technologies

| Component | Role |
|---|---|
| **Power BI Desktop** | Authoring tool for the data model, measures and report pages |
| **Data model and measures** | Calculate total orders, revenue and profit, aggregated by month, product category and store location |
| **KPI cards with trend backgrounds** | Show headline figures with a visual sense of the monthly trend behind them |
| **Store Location slicer** | Multi-select filter applied across all visuals on the page |
| **Bar and line charts** | Compare orders by product category and track revenue over time |
| **Intro page** | Branded landing page with the shop's mission and quick access links |

The original data source is not shown in the demonstration.

## 5. Controls & Validation

This is a reporting solution, so it does not include data entry, approvals or exception handling. The controls that are demonstrated are:

* **Consistent filtering:** One slicer drives every KPI card and chart, so all figures on the page always reflect the same store selection
* **Multi-select comparison:** Users can combine store locations (such as Downtown and Residential) for a grouped view
* **Accurate drill-in:** Tooltips show exact monthly revenue values, so users can check a figure without leaving the chart

## 6. Business Value

* **Better visibility:** Orders, revenue and profit are visible at a glance on one page
* **Faster analysis:** Store-level comparisons take a single click, not a manual report
* **Clearer decisions:** Category and monthly views highlight which products and periods drive performance
* **Consistency:** Everyone reviewing the report sees the same definitions for orders, revenue and profit
* **Better user experience:** A branded Intro page and a clean layout make the report approachable for store staff

## 7. Skills Demonstrated

* Business KPI definition for retail sales (orders, revenue, profit)
* Power BI report design and page layout
* Data modeling and measures for time-based and category-based aggregation
* Interactive filtering with slicers across multiple visuals
* Data visualization with KPI cards, bar charts and line charts
* Branded report design and data storytelling

## 8. Future Enhancements

The following are **potential future enhancements**, not existing functionality:

* **Data quality:** Resolve the "(Blank)" product category so all orders are assigned to a category
* **Targets and variance:** Add monthly targets and show performance against them
* **Margin and growth KPIs:** Add profit margin, average order value and month-over-month growth
* **More filters:** Add date range and product category slicers
* **Drill-through:** Add a detail page by store location or category
* **Publishing:** Publish to the Power BI Service with scheduled refresh and shared access for managers

---

## Portfolio Summary

An interactive Power BI KPI report for Kiddy Lah! Toy Shop that brings sales performance into one view. KPI cards show total orders, revenue and profit, while charts break down orders by product category and track revenue month by month. A store location slicer updates every visual at once, making it easy to compare Airport, Commercial, Downtown and Residential stores. The report gives managers fast, consistent visibility of sales results.
