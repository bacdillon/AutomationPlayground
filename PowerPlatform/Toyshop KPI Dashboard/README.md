# KiddyLah! Toyshop KPI Dashboard

An interactive Power BI dashboard built for a toy retail chain ("Kiddy Lah!"), giving the business a clear, filterable view of sales performance orders, revenue, and profit across its store locations and product categories. This project is a business intelligence and reporting piece, complementing the "Kiddy Lah!" inventory management system elsewhere in this portfolio.

## 1. Project Overview

This project is a multi-page Power BI report that turns raw sales data from a toy retail chain into a clear, interactive picture of business performance. It includes a branded introduction page, and a core KPI dashboard showing total orders, revenue, and profit,broken down by store location, product category, and month with full drill down and filtering built in.

## 2. Business Context

A retail chain operating multiple store locations such as Airport, Commercial, and Downtown stores needs a clear, consolidated view of how each location and product category is performing. Without a shared dashboard, requires someone to manually pull and combine sales data, which is slow and makes it hard to spot trends or compare locations quickly.

## 3. Business Problem

Retail businesses with multiple locations and product lines commonly struggle with:

- **Fragmented visibility** — sales data often lives in different places, making it hard to get a single, trustworthy view of overall performance.
- **Slow, manual reporting** — building a performance summary by hand takes time and needs to be repeated every reporting period.
- **Limited ability to compare locations or categories** — without an interactive tool, comparing "Airport" vs. "Downtown" performance, or seeing which product category drives the most orders, requires manual data slicing.
- **Missed trends** — without an easy way to look at performance over time, gradual shifts (a slow month, a growing category) can go unnoticed.

## 4. Project Objectives

- Consolidate sales data into a single, reliable reporting source.
- Present key performance indicators the orders, revenue, and profit clearly at a glance.
- Allow filtering by store location to compare performance across sites.
- Show trends over time, with the ability to drill into specific months.
- Break down performance by product category to highlight what's driving sales.
- Present the report in a clean, branded, easy to navigate format.

## 5. What the Video Demonstrates

The video walks through a Power BI report titled **"KiddyLah Toyshop KPI Report,"** showing:

- A branded **Intro page** for "Kiddy Lah! Toy Shop," styled like an internal company hub including an About Us / Mission section and quick-access links (team information, handbook, time-off requests, store directory, weekly reports, and more).
- The core **KPI Report page**, featuring:
  - A **Store Location filter** (Airport, Commercial, Downtown), which instantly updates all figures on the page when a location is selected.
  - Headline KPI cards for **Total Orders**, **Revenue**, and **Profit**, which update dynamically based on the selected filter for an example, showing company wide totals of roughly 29,933 orders, $455,690 in revenue, and $123,495 in profit, versus location-specific figures when a single store is selected.
  - A **Total Orders by Product Category** chart, showing which categories are driving order volume.
  - A **Revenue by Month** trend chart, with interactive drill-down, hovering or clicking a point reveals the exact revenue for that specific date. For example, revealing a detailed daily figure within a given month).

## 6. End-to-End Workflow, Step by Step

1. **Open the report.** The user lands on a introduction page for the Kiddy Lah! Toy Shop.
2. **Navigate to the KPI dashboard.** The user moves to the main KPI Report page.
3. **Review headline metrics.** Total Orders, Revenue, and Profit are immediately visible as summary cards.
4. **Filter by store location.** Selecting a specific location (Airport, Commercial, or Downtown) updates every visual on the page to reflect that location's performance.
5. **Explore by category.** The Total Orders by Product Category chart shows which categories are contributing most to order volume.
6. **Explore trends over time.** The Revenue by Month chart shows the overall trend, and can be drilled into for a closer look at performance on a specific date.

## 7. Systems and Applications Involved

- **Microsoft Power BI Desktop** — used to build and present the report
- An underlying **sales dataset** covering orders, revenue, profit, store locations, and product categories

## 8. Technologies Used

- **Power BI Desktop** — for report design, data modeling, and visualization
- **Power BI measures and calculations** — for computing Total Orders, Revenue, and Profit dynamically based on filter selections
- **Interactive filtering and cross-highlighting** — selecting a store location updates every visual on the page
- **Drill-down enabled time-series charts** — allowing users to move from a monthly view down to a specific date

## 9. Automation Logic

While this project isn't a process automation in the RPA sense, it relies on **automated calculation logic** built into the Power BI data model: KPIs like Total Orders, Revenue, and Profit are defined once as measures and automatically recalculate based on whatever filters are applied and no manual recalculation is needed when switching between store locations or drilling into a specific month. This is what makes the dashboard genuinely interactive rather than a static report: the same underlying logic serves every possible view of the data.

## 10. AI Capabilities

This project doesn't use AI. It is a traditional, well-structured business intelligence dashboard. Its value comes from clear data modeling and thoughtful visual design, not predictive or generative features. (Power BI's Copilot capability is visible in the toolbar during the demo, but the report itself does not appear to rely on AI-generated content or insights.)

## 11. User Interactions

- Users navigate between report pages (Intro and KPI Report) to move from general company information to performance data.
- Users apply the **Store Location filter** to instantly narrow the dashboard to a specific site.
- Users can **hover or click** on chart elements such as a point on the Revenue by Month trend line to drill into more detailed, date specific figures.
- No data entry is required; the dashboard is a read-only, exploratory reporting tool.

## 12. Inputs and Outputs

**Inputs:**
- Underlying sales data covering orders, revenue, profit, store location, product category, and date

**Outputs:**
- Summary KPI cards for Total Orders, Revenue, and Profit
- Visual breakdowns by product category and by month
- Location-specific performance views, generated instantly through filtering

## 13. Error Handling and Validation

- Because KPIs are calculated through defined measures rather than hardcoded values, the figures shown remain consistent and accurate regardless of which filters are applied.
- Centralizing the data in a single report reduces the risk of inconsistent figures that can arise when different people manually calculate the same metrics separately.

## 14. Business Rules

- KPI figures (Orders, Revenue, Profit) must always reflect the currently selected store location filter.
- Visuals must update together and consistently when a filter is applied. No visual should show data inconsistent with the current selection.
- Drill-down on the Revenue by Month chart must reveal accurate, date specific figures consistent with the higher-level monthly totals.

## 15. Key Features Demonstrated

- A clean, branded introduction/landing page within the report
- Dynamic KPI cards for Total Orders, Revenue, and Profit
- Store-location filtering with instant visual updates
- Category-level breakdown of order volume
- Interactive, drill down-enabled trend analysis over time

## 16. Business Value and Benefits

- **Faster, clearer decision-making**, since performance data is available at a glance rather than requiring manual compilation.
- **Easy comparison across locations**, helping identify which stores are over- or under-performing.
- **Category-level insight**, showing which product lines are driving sales.
- **Trend visibility**, making it easier to spot patterns in revenue over time rather than only seeing a single snapshot.
- **A single source of truth**, reducing the risk of conflicting figures from separately maintained spreadsheets.

## 17. Productivity Improvements

- Removes the need to manually compile sales summaries for each store location or time period.
- Lets anyone with access answer their own performance questions (e.g., "how did the Airport store do last quarter?") without needing to request a custom report.
- Cut down the time needed to prepare for performance reviews or planning discussions, since the data is always current and ready to explore.

## 18. Time or Cost Savings (If Evident)

The video demonstrates instant recalculation of KPIs and charts as different filters are applied. Figures that would otherwise require manual recompilation update in real time. It doesn't show a direct time or cost comparison against a manual reporting process, so no specific savings figure is claimed here. Replacing manual, ad hoc sales reporting with a self-service, interactive dashboard is a well-established way to save significant reporting time for retail and multi location businesses.

## 19. Skills Demonstrated

- Designing a multi-page Power BI report, including a landing page
- Building KPI measures and calculations for core business metrics
- Implementing interactive filtering across multiple visuals
- Designing drill-down-enabled time-series visualizations
- Structuring a report for clear, self-service business use

## 20. Real-World Enterprise Use Cases

This kind of KPI dashboard applies to a wide range of business reporting needs, including:

- **Multi-location retail performance tracking** — comparing sales across stores or regions
- **Sales and revenue reporting** — giving leadership a live view of business performance
- **Product or category performance analysis** — identifying top and underperforming product lines
- **Executive dashboards** — consolidating key metrics into a single, shareable view
- **Operational reporting hubs** — combining reporting with easy access to related resources (as shown in the Intro page's quick-access links)

## 21. Lessons Learned

- Defining KPIs as reusable measures, rather than static numbers, is what makes a dashboard genuinely interactive and trustworthy across every filter combination.
- A well-designed landing page can make a BI report feel like a proper internal tool rather than just a chart, improving adoption.
- Giving users the ability to filter and drill down themselves reduces the burden on whoever would otherwise be asked to produce ad hoc breakdowns.
- Combining headline KPIs with both categorical and time-based breakdowns gives a more complete picture than any single view could on its own.

## 22. Possible Future Enhancements

- Add **year-over-year comparison** views to show growth or decline more clearly.
- Introduce **product-level drill-down**, not just category-level, for more granular insight.
- Add **target vs. actual tracking**, showing performance against sales goals.
- Build **automated alerts** for significant changes in revenue or profit trends.
- Integrate the dashboard directly with the **inventory management system**, connecting sales performance to stock levels for a fuller operational picture.
- Add **mobile-optimized views** for store managers checking performance on the go.
