# Airline Flight Delays Dashboard
A Power BI dashboard that turns raw flight records into 
airline performance. It shows how many flights ran on time, 
how many were delayed or canceled, and how that breaks down 
by airline and by city, with full interactive filtering built                             in.

## 1. Project Overview

This project is a Power BI report, the **"Flight Status Dashboard,"** built around a large dataset of airline flights. It summarizes total flights, delays, and cancellations at a glance, then lets the viewer break that picture down by airline or by departure city with a single click. The video shows the report being actively built and refined in Power BI Desktop — visuals being formatted, resized, and cross-filtered — giving a look at both the finished dashboard and the process of assembling it.

## 2. Business Context

Airlines, travel platforms, and airport operations teams all care deeply about flight punctuality — it affects customer satisfaction, operational planning, and regulatory reporting. With millions of flight records generated across airlines and airports, understanding overall performance (and knowing which airlines or routes are the biggest problem areas) requires more than a raw data table. It requires a report that summarizes the big picture while still letting someone drill into a specific airline or city.

## 3. Business Problem

Working with raw flight data presents a few common challenges:

- **Millions of individual flight records** are far too much detail for anyone to review manually.
- **Performance varies significantly by airline and by city**, and spotting those patterns requires the ability to filter and compare, not just look at one big total.
- **Static reports go stale and don't invite exploration** — a fixed set of numbers doesn't let a viewer ask their own follow-up questions.
- **Building a clear, well-organized report from scratch** takes deliberate visual design, not just dropping charts onto a page.

## 4. Project Objectives

- Summarize total flights, delays, and cancellations clearly at a glance.
- Show how flight status varies by airline and by departure city.
- Allow interactive filtering, so a viewer can focus on a specific airline or location.
- Present the information through well-designed, clearly labeled visuals.

## 5. What the Video Demonstrates

The video shows the **"Flight Status Dashboard"** being built and used in **Power BI Desktop**, including:

- Headline **KPI cards** for Total Flights, Delayed Flights, and Canceled Flights, giving an immediate summary of overall performance.
- A **map visual** showing flight volume across major cities (Atlanta, Chicago, Dallas-Fort Worth, Denver, Los Angeles, San Francisco, Phoenix, Houston, Las Vegas, and Minneapolis), with bubble size reflecting the number of flights from each location.
- A **bar chart ranking airlines** (including United, Southwest, Delta, American Eagle, SkyWest, Alaska Airlines, JetBlue, Frontier, and others) by flight volume or delay rate.
- A **Flight Status breakdown** (On-Time, Delayed, Canceled), shown both as percentages and as a categorized bar chart.
- **Interactive cross-filtering** in action: clicking a specific city (for example, San Francisco) or a specific airline (for example, JetBlue Airways or American Airlines) instantly updates every other visual on the page to reflect that selection — showing, for instance, an airline-specific delay rate (like 48% delayed for JetBlue in one selected view) rather than the overall average.
- The report actively being **formatted and refined** — adjusting visual size and position, background, color, transparency, borders, shadows, titles, and legends — showing the report-building process itself, not just a finished, static result.

## 6. End-to-End Workflow, Step by Step

1. **Load the flight dataset.** The underlying data — individual flight records including airline, city, and status — is connected as the report's data source.
2. **Build summary KPIs.** Total Flights, Delayed Flights, and Canceled Flights are calculated and displayed as headline figures.
3. **Visualize by location.** A map shows flight volume across major cities.
4. **Visualize by airline.** A bar chart ranks airlines by flight volume and/or delay rate.
5. **Break down flight status.** On-time, delayed, and canceled flights are shown both as percentages and as a categorized comparison.
6. **Refine the visuals.** Formatting is applied — sizing, color, borders, titles — to make the report clear and easy to read.
7. **Explore interactively.** Clicking a city or airline filters the entire report to that selection, letting the viewer explore performance at a more granular level.

## 7. Systems and Applications Involved

- **Microsoft Power BI Desktop** — used to build, format, and interact with the report
- An underlying **flight records dataset**, covering airline, departure city, and flight status (on-time, delayed, canceled)

## 8. Technologies Used

- **Power BI Desktop** — for report design, data modeling, and visualization
- **KPI card visuals** — for headline summary figures
- **Map visualization** — for geographic representation of flight volume
- **Bar and categorical charts** — for airline and status comparisons
- **Interactive cross-filtering** — so selecting one visual updates all others on the page
- **Visual formatting tools** (background, color, borders, shadows, titles, legends) — for report design and polish

## 9. Automation Logic

As with other Power BI reports, the "automation" here lies in how the underlying measures are defined: Total Flights, Delayed Flights, and Canceled Flights are each calculated once as reusable measures, and every visual on the page recalculates automatically based on whatever filter is currently applied. This is what allows a single click on an airline or a city to instantly update every chart and KPI card consistently, without needing to manually rebuild anything — the same underlying logic simply gets re-evaluated against a narrower slice of the data.

## 10. AI Capabilities

This project doesn't use AI — it's a traditional, well-constructed Power BI report. Its strength is in clear data visualization and interactive design: presenting a large, complex dataset (flight records across many airlines and cities) in a way that's genuinely easy to explore and understand at a glance.

## 11. User Interactions

- Users can view headline KPIs immediately, without needing to interact with anything.
- Users can **click on a city** in the map to filter the entire report down to that location's flights.
- Users can **click on an airline** in the bar chart to see that airline's specific performance across all visuals.
- The report supports this kind of free exploration without requiring any technical knowledge of the underlying data.

## 12. Inputs and Outputs

**Inputs:**
- A dataset of individual flight records, including airline, departure city, and flight status

**Outputs:**
- Summary KPIs for total, delayed, and canceled flights
- A geographic view of flight volume by city
- An airline-by-airline performance comparison
- An interactive, filterable view of flight status across the entire dataset

## 13. Error Handling and Validation

- Because all KPIs and charts are driven from the same underlying measures, the numbers stay consistent with each other no matter which filter is applied — there's no risk of one visual showing figures inconsistent with another.
- Centralizing flight performance data into a single report reduces the risk of conflicting figures that can arise from separately maintained summaries or manual calculations.

## 14. Business Rules

- Every flight in the dataset must be categorized into exactly one status: On-Time, Delayed, or Canceled.
- KPI totals (Total Flights, Delayed Flights, Canceled Flights) must always reflect the currently applied filter selection.
- All visuals on the report must update together and consistently whenever a filter (city or airline) is applied.

## 15. Key Features Demonstrated

- Clear, at-a-glance KPI summaries for a large dataset
- Geographic visualization of flight volume by city
- Airline-level performance comparison
- Fully interactive, cross-filtered report design
- Deliberate visual formatting and report design practices

## 16. Business Value and Benefits

- **Immediate visibility into airline performance**, without needing to manually process raw flight data.
- **Easy identification of problem areas** — whether a specific airline or a specific city is driving a disproportionate share of delays or cancellations.
- **Self-service exploration**, letting stakeholders answer their own follow-up questions without requesting a custom report.
- **Consistent, trustworthy reporting**, since every visual draws from the same underlying data and calculations.

## 17. Productivity Improvements

- Removes the need to manually aggregate and summarize a large flight dataset.
- Lets anyone explore performance by airline or city without writing a query or building a spreadsheet pivot table.
- Speeds up the process of identifying which airlines or locations need closer attention.

## 18. Time or Cost Savings (If Evident)

The video shows KPIs and visuals recalculating instantly as different cities and airlines are selected — filtering and recalculation that would otherwise require manually re-querying or re-summarizing the underlying data. It doesn't demonstrate a direct time comparison against manual reporting or a large-scale operational cost impact, so no specific savings figure is claimed here. That said, replacing manual flight-performance analysis with a self-service, interactive dashboard is a well-established way to save significant analyst time, especially with a dataset this large.

## 19. Skills Demonstrated

- Designing KPI-driven Power BI reports for large datasets
- Building geographic (map-based) data visualizations
- Creating interactive, cross-filtered report experiences
- Applying visual formatting and design principles for clarity and usability
- Structuring reusable measures to support consistent, filter-driven reporting

## 20. Real-World Enterprise Use Cases

This kind of performance dashboard applies broadly, including:

- **Airline and airport operations reporting** — tracking punctuality and cancellations across routes and carriers, as shown here
- **Logistics and delivery performance tracking** — monitoring on-time delivery rates across carriers or regions
- **Customer service level reporting** — tracking response or resolution times across teams or locations
- **Any operational performance dashboard** — where volume, status breakdown, and geographic or categorical comparison matter
- **Regulatory or compliance reporting** — where punctuality or service-level data must be tracked and reported consistently

## 21. Lessons Learned

- A small set of well-chosen KPIs (Total, Delayed, Canceled) can communicate the big picture faster than a detailed table ever could.
- Geographic visualization adds an intuitive layer of understanding that a plain list of cities and numbers doesn't provide.
- Interactive cross-filtering is what turns a static report into a genuine analysis tool — the ability to click into an airline or city is often more valuable than the initial summary view itself.
- Deliberate visual formatting (color, spacing, borders, titles) isn't just cosmetic — it directly affects how easily a report communicates its message.

## 22. Possible Future Enhancements

- Add **time-based trend analysis**, showing how delay and cancellation rates change over months or seasons.
- Include **root-cause categorization**, if data is available (e.g., weather, mechanical, carrier-related delays).
- Add **benchmark comparisons**, showing how an airline or city compares to the overall average.
- Build **airport-to-airport route analysis**, rather than only city-level summaries.
- Add **predictive elements**, flagging routes or airlines at higher risk of future delays based on historical patterns.
- Enable **export or scheduled reporting**, so stakeholders can receive regular performance snapshots automatically.

---

*This project is part of an Automation Playground portfolio, built to demonstrate clear, interactive business intelligence reporting — turning a large, complex flight dataset into an accessible, explorable performance dashboard.*
