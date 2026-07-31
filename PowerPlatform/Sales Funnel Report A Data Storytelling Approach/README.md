# Sales Funnel Report: A Data Storytelling Approach

**Automation Playground Portfolio Project**

An interactive Power BI report that turns raw sales pipeline data into a clear, visual story. Showing how leads move through each stage of the sales process, where they drop off, and how each salesperson is performing. This project focuses on data storytelling: choosing the right visuals to make a sales funnel easy to understand at a glance.

## 1. Project Overview

This project is a Power BI report built around a sales team's pipeline: leads, presentations, offers, and contracts. Rather than presenting raw numbers in a table, the report tells the story of the sales process visually. Showing how many opportunities enter at the top of the funnel, how many make it through each stage, and where the biggest drop-offs happen. It is fully interactive, letting anyone explore performance by salesperson or by time period without needing to ask for a custom report.

## 2. Business Context

Sales teams live and die by their pipeline. Understanding how many leads are being generated, how many convert to presentations, how many of those become offers, and how many offers close as contracts is fundamental to running a sales organization. It shows not just how much revenue is coming, but where the process itself is losing opportunities. Sales leaders need this picture regularly, and ideally without waiting on a manually built report each time.

## 3. Business Problem

Sales pipeline data is often hard to interpret in its raw form:

- **Raw numbers don't tell a story.** A spreadsheet of lead counts doesn't make it obvious where the pipeline is leaking.
- **Comparing salespeople is tedious** without a report built specifically to make that comparison easy.
- **Trends over time are easy to miss** when data is only ever looked at as a single snapshot.
- **Manually rebuilding this view** for every sales meeting or review is a repeated, avoidable effort.

## 4. Project Objectives

- Visualize the sales pipeline as a clear funnel, from lead to contract.
- Make it easy to see where prospects are dropping out of the pipeline.
- Allow performance comparison across individual salespeople.
- Show trends in pipeline activity over time, not just a single snapshot.
- Make the whole report interactive and self-service, so anyone can explore the data themselves.

## 5. What the Video Demonstrates

The video walks through a Power BI report titled **"Sales Funnel Report,"** showing:

- A **Sales Funnel visual**, displaying the four key pipeline stages. **Lead, Presentation, Offer, Contract** with both the count and percentage of opportunities remaining at each stage (for an example, starting at 100% of leads and narrowing down to a smaller percentage of contracts).
- A **"Contract by Salesperson"** bar chart, comparing how many contracts each salesperson (Peter, Alex, Mary, Viktor) has closed.
- **Weekly trend charts** for Leads, Presentations, Offers, and Contracts, spanning a multi-month period (January through March), showing how pipeline activity changes week to week.
- **Interactive filtering** clicking on an individual salesperson's bar instantly updates the funnel and trend charts to show that person's specific pipeline performance, rather than the whole team's.
- A **period selector** (e.g., moving between February and March), letting the viewer look at performance for different timeframes.
- A **"Company list"** element within the funnel visual, allowing a viewer to see or drill into the specific companies sitting at each stage of the pipeline.

## 6. End-to-End Workflow, Step by Step

1. **View the overall funnel.** The report opens showing the full sales funnel from Lead through to Contract for the whole team.
2. **Identify drop-off points.** The percentages at each stage make it immediately clear where the biggest losses in the pipeline occur.
3. **Compare salespeople.** The Contract by Salesperson chart shows who is closing the most deals.
4. **Filter to an individual.** Clicking on a specific salesperson updates the entire report to reflect just their pipeline.
5. **Explore trends over time.** The weekly charts show whether activity at each stage is growing, shrinking, or holding steady.
6. **Adjust the time period.** The period selector lets the viewer move between different months to compare performance over time.
7. **Drill into specifics.** The company list lets a viewer see exactly which companies are sitting at a given pipeline stage.

## 7. Systems and Applications Involved

- **Microsoft Power BI Desktop** — used to build and present the report
- An underlying **sales pipeline dataset**, covering leads, presentations, offers, contracts, salespeople, and dates

## 8. Technologies Used

- **Power BI Desktop** — for report design, data modeling, and visualization
- **Funnel chart visualization** — for representing the multi-stage sales pipeline
- **Interactive cross-filtering** — so selecting a salesperson updates every visual on the report
- **Time-series (trend) charts** — for showing pipeline activity by week
- **Drill-through/detail navigation** — for viewing the specific companies behind the summary numbers

## 9. Automation Logic

While this isn't a process automation project, it relies on the same underlying principle that makes good BI reports work: metrics are calculated once, as reusable measures, and automatically recalculate based on whatever filters are applied. Selecting a salesperson doesn't require rebuilding the report. The funnel, the trend charts, and the percentages all update together, instantly, because they're all built from the same underlying logic. 

## 10. AI Capabilities

This project doesn't use AI. It is a thoughtfully designed, traditional business intelligence report. Its value lies entirely in **data storytelling**: choosing the right visual (a funnel, rather than a plain table) to make a business process instantly understandable, which is a design skill in its own right, independent of any AI involvement.

## 11. User Interactions

- Users can **click on a salesperson** in the bar chart to filter the entire report down to that individual's performance.
- Users can **change the selected time period** to view performance for a different month or range.
- Users can explore the **company list** within the funnel to see which specific companies are behind a given stage's numbers.
- No data entry is required. This is a read-only, exploratory reporting tool designed for quick, self-service insight.

## 12. Inputs and Outputs

**Inputs:**
- Underlying sales pipeline data: lead, presentation, offer, and contract records, tagged by salesperson and date

**Outputs:**
- A visual sales funnel showing conversion at each pipeline stage
- A salesperson comparison of closed contracts
- Weekly trend views of pipeline activity
- Drill-down access to the specific companies at each stage

## 13. Error Handling and Validation

- Because the funnel and trend visuals are built from defined, reusable calculations, the numbers stay consistent no matter which filter or time period is selected.
- Centralizing the pipeline data in a single report reduces the risk of inconsistent figures that can arise when different people track pipeline numbers separately.

## 14. Business Rules

- The funnel must always reflect the four defined pipeline stages, in order: Lead, Presentation, Offer, Contract.
- Percentages at each stage must be calculated relative to the starting number of leads, so drop-off is always shown accurately.
- All visuals on the report must update together and consistently whenever a filter (salesperson or time period) is applied.

## 15. Key Features Demonstrated

- A clear, multi stage sales funnel visualization
- Salesperson-level performance comparison
- Weekly trend tracking across all pipeline stages
- Fully interactive, cross filtering report design
- Drill-down access to underlying company level detail
- Thoughtful visual design aimed specifically at making the data easy to interpret

## 16. Business Value and Benefits

- **Immediate visibility into pipeline health**, without waiting for someone to manually compile a report.
- **Clear identification of where deals are lost**, helping sales leaders focus coaching or process improvements where they'll matter most.
- **Fair, data-driven performance comparison** across the sales team.
- **Trend awareness**, making it easier to catch a slowing pipeline early rather than after a quarter has already ended.
- **Self-service exploration**, freeing up whoever would otherwise be asked to produce custom breakdowns on request.

## 17. Productivity Improvements

- Removes the need to manually build a sales funnel summary for each team meeting or review.
- Lets sales managers answer their own questions about performance without waiting on a report request.
- Cuts the time needed to prepare for pipeline reviews, since the data is always current and ready to explore.

## 18. Time or Cost Savings (If Evident)

The video shows the funnel, trend charts, and salesperson comparisons all updating instantly as different filters are applied, recalculations that would otherwise require manually rebuilding a report. It doesn't show a direct time comparison against manual reporting, so no specific savings figure is claimed here. Replacing manual, ad hoc pipeline reporting with a self-service, interactive dashboard is a well established way to save significant time for sales operations and leadership teams.

## 19. Skills Demonstrated

- Designing effective data visualizations, including funnel charts, for business storytelling
- Building interactive, cross-filtered Power BI reports
- Structuring calculations to support dynamic, filter driven reporting
- Designing time series visuals to show trends, not just snapshots
- Applying data storytelling principles to make a business process instantly understandable

## 20. Real-World Enterprise Use Cases

This kind of funnel-based reporting applies to any multi-stage business process, including:

- **Sales pipeline management** — tracking leads through to closed deals, as shown here
- **Recruitment and hiring funnels** — tracking candidates from application through to hire
- **Customer onboarding funnels** — tracking new customers through setup and activation stages
- **Marketing conversion funnels** — tracking prospects from initial contact through to conversion
- **Any staged business process** — where understanding drop-off at each step is critical to improving outcomes

## 21. Lessons Learned

- Choosing the right visual. A funnel rather than a plain table that makes a multi-stage process far easier to understand at a glance.
- Interactivity (filtering by salesperson, browsing by time period) turns a static report into a genuine exploration tool, increasing its real-world usefulness.
- Pairing a summary view (the funnel) with supporting detail (trend charts and a company list) gives users both the big picture and the ability to dig deeper when needed.
- Good data storytelling is a distinct skill from simply having accurate data: the same numbers, presented differently, can be far more or far less useful to a decision maker.

## 22. Possible Future Enhancements

- Add **conversion rate benchmarks**, showing whether current performance is above or below a target.
- Introduce **year-over-year comparisons** to track long-term pipeline health.
- Add **average time-in-stage** metrics, showing not just how many deals convert, but how long they take.
- Build **automated alerts** for significant pipeline changes, such as a sudden drop in leads.
- Extend the report with **forecasting**, projecting expected contracts based on current pipeline trends.
- Add **team-level rollups**, useful for organizations with multiple sales teams or regions.
