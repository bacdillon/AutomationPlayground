# Airline Flight Delays Dashboard

## 1. Project Overview

This project is an interactive Power BI dashboard that summarizes airline flight performance. It shows how many flights were operated, delayed and canceled, which cities and airlines are most affected, and what causes the delays. Every visual is linked, so selecting a city or an airline instantly filters the whole page to that selection.

* **Use case:** Analyzing flight volumes, on-time performance, delays and cancellations
* **Intended audience:** Airline operations analysts, airport planners, or anyone reviewing on-time performance
* **Main technologies:** Microsoft Power BI Desktop (report "Flight Status Dashboard" with KPI cards, bar, column, donut and stacked bar charts)

## 2. Business Problem & Objectives

### Problem

Flight datasets are large. The demo dataset covers around 2 million flights. At that scale, it is hard to answer simple questions from raw data, such as which airports handle the most traffic, which airlines are delayed most often, or why delays happen. Without a summary view, comparing airlines and cities takes repeated manual analysis.

### Objectives

* Show total, delayed and canceled flights at a glance
* Show the share of flights that are on time, delayed or canceled
* Compare busy origin cities and airlines side by side
* Show the main causes of delays
* Let users drill into a specific city or airline with a single click

## 3. Solution

The dashboard brings the key measures together on one page:

* **KPI cards:** Total Flights, Delayed Flights and Canceled Flights, each with a small trend chart in the background (for example, 2M total, 790K delayed and 29K canceled across the full dataset)
* **Flights by city:** A bar chart of the top 10 origin cities by flight count, led by Atlanta, Chicago and Dallas-Fort Worth
* **Airline comparison:** A bar chart ranking airlines by a rate between 0 and 1, which appears to be each airline's delay rate (for example, United Air Lines 0.53 and Hawaiian Airlines 0.24)
* **Delay causes:** A donut chart splitting delays into Weather, Airline/Carrier, National Aviation System and Security
* **Column chart:** Values for categories 1 to 7, which look like days of the week (the axis is not labeled)
* **Flight Status panel:** On-time, delayed and canceled shares (0.58, 0.41 and 0.01 overall)
* **Total Flights by Status:** A stacked bar showing the on-time, delayed and canceled mix as percentages

### End-to-End Workflow

1. **Review the overall picture:** The user starts with totals across all flights, cities and airlines.
2. **Drill into a city:** Selecting a city, such as Dallas-Fort Worth, filters every visual. Total flights drop to 240K, delayed flights to 96K, and the airline ranking and delay causes update for that city.
3. **Drill into an airline:** Selecting an airline, such as JetBlue Airways, shows only that airline's flights (18K total, 8K delayed, 201 canceled) and its on-time and delay shares.
4. **Compare and investigate:** The user switches between cities and airlines to compare performance, spot the routes and carriers with higher delay rates, and see how the causes change.

## 4. Solution Architecture & Technologies

| Component | Role |
|---|---|
| **Power BI Desktop** | Authoring tool for the data model, measures and report page |
| **Measures** | Calculate total, delayed and canceled flights, along with on-time, delayed and canceled rates |
| **KPI cards with trend backgrounds** | Show headline counts with a visual sense of the trend behind them |
| **Bar, column, donut and stacked bar charts** | Compare cities, airlines, delay causes and the status mix |
| **Cross-filtering between visuals** | Lets a selection in one chart filter every other visual on the page |

The original data source is not shown in the demonstration.

## 5. Controls & Validation

This is a reporting solution, so it does not include data entry, approvals or exception handling. The controls that are demonstrated are:

* **Consistent filtering:** One selection updates every visual on the page, so all figures always describe the same subset of flights
* **Consistent measures:** The same definitions of total, delayed and canceled flights are used across the cards, charts and status panel
* **Status breakdown that adds up:** On-time, delayed and canceled shares together account for all flights in the current selection

## 6. Business Value

* **Better visibility:** Flight volumes, delays and cancellations are visible on a single page
* **Faster analysis:** City and airline comparisons take a single click, with no new queries or reports
* **Root-cause insight:** The delay-cause breakdown shows whether weather, carrier issues, the aviation system or security drive delays
* **Performance comparison:** Ranking airlines by delay rate highlights where on-time performance is weakest
* **Consistency:** Everyone reviewing the report sees the same definitions and figures

## 7. Skills Demonstrated

* KPI definition for operational performance (on-time, delayed and canceled rates)
* Power BI report design and page layout
* Measures for flight counts and status rates
* Data visualization with KPI cards, bar, column, donut and stacked bar charts
* Interactive cross-filtering for drill-down analysis
* Working with a large dataset (around 2 million flights)

## 8. Future Enhancements

The following are **potential future enhancements**, not existing functionality:

* **Clearer labels:** Add axis titles (for example, label the 1 to 7 chart and the airline rate chart) and show rates as percentages (58% rather than 0.58)
* **Slicers:** Add filters for date range, month, airline and destination city
* **Delay minutes:** Add average delay time alongside delay counts
* **Route view:** Add origin and destination pairs, or a map, to compare routes
* **Drill-through page:** Add a detail page for a selected airline or airport
* **Tidy the report:** Rename the "Duplicate of Flight Status Dashboard" page before sharing
* **Publishing:** Publish to the Power BI Service with scheduled refresh

---

## Final Summary

The Airline Flight Delays Dashboard is an interactive Power BI report that turns around 2 million flight records into a clear view of on-time performance. KPI cards show total, delayed and canceled flights, while charts compare top cities, airline delay rates and the causes of delays. Selecting any city or airline filters the whole page, making it quick to see where and why delays happen and which carriers perform best.
