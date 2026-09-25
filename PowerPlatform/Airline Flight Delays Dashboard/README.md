# Airline Flight Delays Dashboard

A Power BI dashboard that turns raw flight records into a clear picture of airline performance, how many flights ran on time, how many were delayed or canceled, and how that breaks down by airline and by city, with full interactive filtering built in.

## 1. Project Overview

This project is a Power BI report, the "Flight Status Dashboard," built around a large dataset of airline flights. It summarizes total flights, delays, and cancellations at a glance, then lets the viewer break that picture down by airline or by departure city with a single click. The video shows the report being actively built and refined in Power BI Desktop, with visuals being formatted, resized, and cross-filtered, giving a look at both the finished dashboard and the process of assembling it.

## 2. Business Problem & Objectives

**The problem:** Airlines, travel platforms, and airport operations teams all care deeply about flight punctuality. It affects customer satisfaction, operational planning, and regulatory reporting. With millions of flight records generated across airlines and airports, understanding overall performance, and knowing which airlines or routes are the biggest problem areas, requires more than a raw data table. It requires a report that summarizes the big picture while still letting someone drill into a specific airline or city. Millions of individual flight records are far too much detail for anyone to review manually, and performance varies significantly by airline and by city, so spotting those patterns requires the ability to filter and compare, not just look at one big total. Static reports go stale and don't invite exploration, since a fixed set of numbers doesn't let a viewer ask their own follow-up questions, and building a clear, well-organized report from scratch takes deliberate visual design, not just dropping charts onto a page.

**The objectives:**
- Summarize total flights, delays, and cancellations clearly at a glance.
- Show how flight status varies by airline and by departure city.
- Allow interactive filtering, so a viewer can focus on a specific airline or location.
- Present the information through well-designed, clearly labeled visuals.

## 3. Solution

The "Flight Status Dashboard" is built and used in Power BI Desktop, anchored by headline KPI cards for Total Flights, Delayed Flights, and Canceled Flights, giving an immediate summary of overall performance. A map visual shows flight volume across major cities, and a bar chart ranks airlines by flight volume or delay rate. A Flight Status breakdown shows On-Time, Delayed, and Canceled flights, both as percentages and as a categorized bar chart.

### What the Video Demonstrates

The map shows flight volume across major cities, including Atlanta, Chicago, Dallas-Fort Worth, Denver, Los Angeles, San Francisco, Phoenix, Houston, Las Vegas, and Minneapolis, with bubble size reflecting the number of flights from each location. The bar chart ranks airlines including United, Southwest, Delta, American Eagle, SkyWest, Alaska Airlines, JetBlue, and Frontier. Interactive cross-filtering is shown in action: clicking a specific city, for example San Francisco, or a specific airline, for example JetBlue Airways or American Airlines, instantly updates every other visual on the page to reflect that selection, showing an airline-specific delay rate, such as 48% delayed for JetBlue in one selected view, rather than the overall average. The report is also shown actively being formatted and refined, with visual size and position, background, color, transparency, borders, shadows, titles, and legends all being adjusted, showing the report-building process itself, not just a finished, static result.

### End-to-End Workflow, Step by Step

1. **Load the flight dataset.** The underlying data, individual flight records including airline, city, and status, is connected as the report's data source.
2. **Build summary KPIs.** Total Flights, Delayed Flights, and Canceled Flights are calculated and displayed as headline figures.
3. **Visualize by location.** A map shows flight volume across major cities.
4. **Visualize by airline.** A bar chart ranks airlines by flight volume and delay rate.
5. **Break down flight status.** On-time, delayed, and canceled flights are shown both as percentages and as a categorized comparison.
6. **Refine the visuals.** Formatting is applied, sizing, color, borders, titles, to make the report clear and easy to read.
7. **Explore interactively.** Clicking a city or airline filters the entire report to that selection, letting the viewer explore performance at a more granular level.

## 4. Solution Architecture & Technologies

- **Microsoft Power BI Desktop**, used to build, format, and interact with the report.
- An underlying **flight records dataset**, covering airline, departure city, and flight status (on-time, delayed, canceled).
- **KPI card visuals**, for headline summary figures.
- **Map visualization**, for geographic representation of flight volume.
- **Bar and categorical charts**, for airline and status comparisons.
- **Interactive cross-filtering**, so selecting one visual updates all others on the page.
- **Visual formatting tools** (background, color, borders, shadows, titles, legends), for report design and polish.

As with other Power BI reports, the "automation" here lies in how the underlying measures are defined. Total Flights, Delayed Flights, and Canceled Flights are each calculated once as reusable measures, and every visual on the page recalculates automatically based on whatever filter is currently applied. This is what allows a single click on an airline or a city to instantly update every chart and KPI card consistently, without needing to manually rebuild anything. The same underlying logic simply gets re-evaluated against a narrower slice of the data. This project doesn't use AI. It's a traditional, well-constructed Power BI report, and its strength is in clear data visualization and interactive design, presenting a large, complex dataset in a way that's genuinely easy to explore and understand at a glance.

## 5. Controls & Validation

- Because all KPIs and charts are driven from the same underlying measures, the numbers stay consistent with each other no matter which filter is applied. There is no risk of one visual showing figures inconsistent with another.
- Centralizing flight performance data into a single report reduces the risk of conflicting figures that can arise from separately maintained summaries or manual calculations.
- Every flight in the dataset must be categorized into exactly one status, On-Time, Delayed, or Canceled, and KPI totals must always reflect the currently applied filter selection.
- All visuals on the report must update together and consistently whenever a filter, city or airline, is applied.

## 6. Business Value

- **Immediate visibility into airline performance**, without needing to manually process raw flight data.
- **Easy identification of problem areas**, whether a specific airline or a specific city is driving a disproportionate share of delays or cancellations.
- **Self-service exploration**, letting stakeholders answer their own follow-up questions without requesting a custom report.
- **Consistent, trustworthy reporting**, since every visual draws from the same underlying data and calculations.

## 7. Skills Demonstrated

- Designing KPI-driven Power BI reports for large datasets.
- Building geographic, map-based, data visualizations.
- Creating interactive, cross-filtered report experiences.
- Applying visual formatting and design principles for clarity and usability.
- Structuring reusable measures to support consistent, filter-driven reporting.

## 8. Enterprise Use Cases

This kind of performance dashboard applies broadly, including:

- **Airline and airport operations reporting**, tracking punctuality and cancellations across routes and carriers, as shown here.
- **Logistics and delivery performance tracking**, monitoring on-time delivery rates across carriers or regions.
- **Customer service level reporting**, tracking response or resolution times across teams or locations.
- **Any operational performance dashboard**, where volume, status breakdown, and geographic or categorical comparison matter.
- **Regulatory or compliance reporting**, where punctuality or service-level data must be tracked and reported consistently.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- A small set of well-chosen KPIs, Total, Delayed, Canceled, can communicate the big picture faster than a detailed table ever could.
- Geographic visualization adds an intuitive layer of understanding that a plain list of cities and numbers doesn't provide.
- Interactive cross-filtering is what turns a static report into a genuine analysis tool. The ability to click into an airline or city is often more valuable than the initial summary view itself.
- Deliberate visual formatting, color, spacing, borders, titles, isn't just cosmetic. It directly affects how easily a report communicates its message.

**Future enhancements:**
- Add time-based trend analysis, showing how delay and cancellation rates change over months or seasons.
- Include root-cause categorization, if data is available, such as weather, mechanical, or carrier-related delays.
- Add benchmark comparisons, showing how an airline or city compares to the overall average.
- Build airport-to-airport route analysis, rather than only city-level summaries.
- Add predictive elements, flagging routes or airlines at higher risk of future delays based on historical patterns.
- Enable export or scheduled reporting, so stakeholders can receive regular performance snapshots automatically.
