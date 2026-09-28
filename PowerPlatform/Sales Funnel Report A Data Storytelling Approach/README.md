# Sales Funnel Report: A Data Storytelling Approach

An interactive Power BI report that turns raw sales pipeline data into a clear, visual story, showing how leads move through each stage of the sales process, where they drop off, and how each salesperson is performing. This project focuses on data storytelling: choosing the right visuals to make a sales funnel genuinely easy to understand at a glance.

## 1. Project Overview

This project is a Power BI report built around a sales team's pipeline: leads, presentations, offers, and contracts. Rather than presenting raw numbers in a table, the report tells the story of the sales process visually, showing how many opportunities enter at the top of the funnel, how many make it through each stage, and where the biggest drop-offs happen. It's fully interactive, letting anyone explore performance by salesperson or by time period without needing to ask for a custom report.

## 2. Business Problem & Objectives

**The problem:** Sales teams live and die by their pipeline. Understanding how many leads are being generated, how many convert to presentations, how many of those become offers, and how many offers close as contracts is fundamental to running a sales organization. It shows not just how much revenue is coming, but where the process itself is losing opportunities. Sales leaders need this picture regularly, and ideally without waiting on a manually built report each time. Raw numbers don't tell a story, since a spreadsheet of lead counts doesn't make it obvious where the pipeline is leaking. Comparing salespeople is tedious without a report built specifically to make that comparison easy, trends over time are easy to miss when data is only ever looked at as a single snapshot, and manually rebuilding this view for every sales meeting or review is a repeated, avoidable effort.

**The objectives:**
- Visualize the sales pipeline as a clear funnel, from lead to contract.
- Make it easy to see where prospects are dropping out of the pipeline.
- Allow performance comparison across individual salespeople.
- Show trends in pipeline activity over time, not just a single snapshot.
- Make the whole report interactive and self-service, so anyone can explore the data themselves.

## 3. Solution

A Power BI report titled "Sales Funnel Report" presents a Sales Funnel visual displaying the four key pipeline stages, Lead, Presentation, Offer, Contract, with both the count and percentage of opportunities remaining at each stage. A "Contract by Salesperson" bar chart compares how many contracts each salesperson has closed, and weekly trend charts for Leads, Presentations, Offers, and Contracts span a multi-month period, showing how pipeline activity changes week to week.

### What the Video Demonstrates

Clicking on an individual salesperson's bar instantly updates the funnel and trend charts to show that person's specific pipeline performance, rather than the whole team's, for salespeople including Peter, Alex, Mary, and Viktor. A period selector lets the viewer move between different timeframes, for example between February and March. A "Company list" element within the funnel visual allows a viewer to see or drill into the specific companies sitting at each stage of the pipeline, and the funnel shows percentages starting at 100% of leads and narrowing down to a smaller percentage of contracts, making drop-off immediately visible.

### End-to-End Workflow, Step by Step

1. **View the overall funnel.** The report opens showing the full sales funnel, from Lead through to Contract, for the whole team.
2. **Identify drop-off points.** The percentages at each stage make it immediately clear where the biggest losses in the pipeline occur.
3. **Compare salespeople.** The Contract by Salesperson chart shows who is closing the most deals.
4. **Filter to an individual.** Clicking on a specific salesperson updates the entire report to reflect just their pipeline.
5. **Explore trends over time.** The weekly charts show whether activity at each stage is growing, shrinking, or holding steady.
6. **Adjust the time period.** The period selector lets the viewer move between different months to compare performance over time.
7. **Drill into specifics.** The company list lets a viewer see exactly which companies are sitting at a given pipeline stage.

## 4. Solution Architecture & Technologies

- **Microsoft Power BI Desktop**, used to build and present the report.
- An underlying **sales pipeline dataset**, covering leads, presentations, offers, contracts, salespeople, and dates.
- **Funnel chart visualization**, for representing the multi-stage sales pipeline.
- **Interactive cross-filtering**, so selecting a salesperson updates every visual on the report.
- **Time-series (trend) charts**, for showing pipeline activity by week.
- **Drill-through and detail navigation**, for viewing the specific companies behind the summary numbers.

While this isn't a process automation project, it relies on the same underlying principle that makes good BI reports work: metrics are calculated once, as reusable measures, and automatically recalculate based on whatever filters are applied. Selecting a salesperson doesn't require rebuilding the report. The funnel, the trend charts, and the percentages all update together, instantly, because they're all built from the same underlying logic. This is what turns a static picture of the sales pipeline into something genuinely explorable.
