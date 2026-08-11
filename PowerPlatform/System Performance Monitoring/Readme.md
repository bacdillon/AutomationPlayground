# System Performance Monitoring with Python, SQL Server & Power BI

A real-time system monitoring solution that continuously collects a computer's performance data, stores it in a database, and visualizes it live on a Power BI dashboard. This project shows a small-scale data pipeline from data collection, through storage, to live reporting,built entirely from foundational tools.

## 1. Project Overview

This project continuously monitors a computer's performance for CPU usage, memory usage, disk usage, network activity, and streams that data into a Power BI dashboard. A Python script collects system metrics in a constant loop and writes them into a SQL Server database, while Power BI connects directly to that database and updates its visuals in near real time. The result is a live, at a glance view of system health, built without any specialized monitoring software.

## 2. Business Context

Organizations rely on servers, workstations, and other systems staying healthy where running out of memory, disk space, or network capacity can quietly degrade performance long before anything fails outright. IT and infrastructure teams often need visibility into this kind of system health data, ideally in a live, easy to read format rather than buried in logs or requiring someone to check manually.

## 3. Business Problem

Without a structured monitoring setup, system performance issues are easy to miss:

- **Performance problems often build up gradually** a slow memory leak or rising disk usage isn't obvious without ongoing tracking.
- **Raw system data isn't useful on its own** a stream of numbers from an operating system's performance counters means little without context or visualization.
- **Manual checking doesn't scale** no one can watch a system's live stats around the clock.
- **Off-the-shelf monitoring tools aren't always available or practical** for every environment, and understanding how to build monitoring from first principles is a valuable, transferable skill.

## 4. Project Objectives

- Continuously collect key system performance metrics from a running computer.
- Store that data reliably in a structured, queryable database.
- Build a live dashboard that visualizes system health as it changes.
- Demonstrate a complete, working data pipeline for collection, storage, and visualization.
## 5. What the Video Demonstrates

The video shows a three-part system built from the ground up:

- A **Python script** (`performance.py`) that runs continuously, using the `psutil` library to read live system metrics such as CPU usage, memory usage, CPU interrupts and calls, memory used/free, bytes sent/received over the network, and disk usage. Inserts a new record into a SQL Server database every second.
- **SQL Server Management Studio**, used to directly query the resulting `Performance` table, confirming that new rows of timestamped performance data are being reliably written in real time as the Python script runs.
- A **Power BI dashboard** ("System Information and Performance Monitoring"), connected live to the same SQL Server database using DirectQuery, showing CPU, disk, and memory usage as gauges, along with time series charts for network activity (bytes sent/received) and CPU activity (calls/interrupts) while all refreshing automatically as new data streams in.

## 6. End-to-End Workflow, Step by Step

1. **Collect system metrics.** The Python script continuously reads live performance data from the operating system — CPU, memory, disk, and network statistics.
2. **Write to the database.** On each loop cycle, the script inserts a new, timestamped record into a SQL Server table.
3. **Store a continuous history.** Over time, the database builds up a detailed, timestamped log of the system's performance.
4. **Connect a live dashboard.** Power BI connects directly to the SQL Server table using DirectQuery, rather than a static import, so it always reflects the latest data.
5. **Visualize in real time.** The dashboard's gauges and charts automatically refresh, showing current CPU, memory, and disk usage, along with trends in network and CPU activity over time.

## 7. Systems and Applications Involved

- **Microsoft SQL Server** — the database storing the collected performance data
- **SQL Server Management Studio** — used to inspect and verify the stored data directly
- **Microsoft Power BI** — the live dashboard visualizing the data
- **Python** (running via Visual Studio Code) — the script collecting and logging the performance data

## 8. Technologies Used

- **Python** — for writing the data collection script
- **psutil** — a Python library for reading system performance metrics (CPU, memory, disk, network)
- **pyodbc** — a Python library for connecting to and writing into SQL Server
- **Microsoft SQL Server** — the relational database storing the performance history
- **Power BI Desktop** — for building the live dashboard
- **DirectQuery** — Power BI's live-connection mode, used here so the dashboard reflects new data without manual refreshes or re-imports

## 9. Automation Logic

The core of the system is a simple but effective loop: read the current system metrics, write them to the database, and repeat continuously, with each cycle capturing a fresh timestamped snapshot of system health. Because the data is written directly into a proper database rather than a log file, it becomes immediately queryable and reportable. Connecting Power BI in DirectQuery mode, rather than importing a static snapshot of the data, is what turns this from a one time report into a live monitoring dashboard where every time the script writes a new row, the dashboard next refresh it.

## 10. AI Capabilities

This project doesn't use AI. Iti is a straightforward, data collection and visualization pipeline. Its value comes from fundamentals: data collection, proper storage, and live visualization. A real-time monitoring doesn't require anything more sophisticated than the right basic tools used well.

## 11. User Interactions

- The Python script runs unattended in the background, requiring no ongoing interaction once started.
- The primary way a person interacts with the system is by viewing the **Power BI dashboard**, which updates on its own as new data arrives.
- Anyone with database access can also query the underlying data directly (as shown using SQL Server Management Studio) for more detailed or custom analysis.

## 12. Inputs and Outputs

**Inputs:**
- Live system performance metrics read directly from the operating system (CPU, memory, disk, and network statistics)

**Outputs:**
- A continuously growing, timestamped performance history stored in SQL Server
- A live Power BI dashboard showing current system status and historical trends

## 13. Error Handling and Validation

- Because each metric is captured and written on its own loop cycle, the system naturally continues logging new data even if a particular snapshot is unusual, rather than stopping altogether.
- Storing data in SQL Server (rather than a flat file or in-memory only) means the collected history is durable and available for inspection independently of the Python script or the dashboard.
- Directly querying the database (as shown in the video) provides a simple way to confirm the data being collected matches what the dashboard displays.

## 14. Business Rules

- A new performance record must be captured and stored on every monitoring cycle.
- Every record must include a timestamp, so performance can be tracked and analyzed over time.
- The dashboard must reflect live data, not a static or manually refreshed snapshot.

## 15. Key Features Demonstrated

- Continuous, automated collection of live system performance metrics
- Reliable storage of time-series performance data in a relational database
- A live-connected Power BI dashboard using DirectQuery
- Multiple visualization types (gauges and time-series charts) covering CPU, memory, disk, and network activity
- A complete, working pipeline from raw data collection to live reporting

## 16. Business Value and Benefits

- **Early visibility into system health**, making it easier to notice trends (like rising memory usage) before they become real problems.
- **No reliance on manual checking** — the dashboard reflects current status automatically.
- **A durable historical record**, useful for troubleshooting or reviewing what happened around a particular point in time.
- **A flexible, low-cost monitoring approach**, built from general-purpose tools rather than a specialized (and potentially expensive) monitoring product.

## 17. Productivity Improvements

- Removes the need for anyone to manually check system resource usage.
- Turns raw, hard-to-interpret system statistics into a clear, visual dashboard anyone can read at a glance.
- Provides an always-current view of system status without requiring manual refreshes or report generation.

## 18. Time or Cost Savings (If Evident)

The video shows the dashboard updating with fresh data roughly every few seconds as the Python script continues running, demonstrating a genuinely live monitoring setup. It doesn't show a real-world incident being caught or a cost comparison against commercial monitoring tools, so no specific dollar or hour savings figure is claimed here. Building monitoring from freely available tools (Python, SQL Server, Power BI) a low-cost alternative to specialized monitoring software for teams that need basic system visibility.

## 19. Skills Demonstrated

- Writing Python scripts to collect live system performance data
- Connecting Python applications to SQL Server for data storage
- Designing a simple, effective database structure for time series data
- Building live, auto refreshing dashboards in Power BI using DirectQuery
- Assembling a complete, working data pipeline from collection through visualization
- Verifying data integrity by querying the database directly

## 20. Real-World Enterprise Use Cases

This applies to many monitoring and reporting scenarios, including:

- **IT infrastructure monitoring** — tracking server or workstation health across an organization
- **Application performance monitoring** — logging and visualizing custom application metrics
- **IoT and sensor data pipelines** — collecting readings from devices and visualizing them live
- **Operational dashboards** — turning any continuously generated data source into a live, visual report
- **Capacity planning** — using historical performance data to anticipate future resource needs

## 21. Lessons Learned

- A live dashboard is only as good as the pipeline feeding it. A continuous data collection is the foundation everything else depends on.
- Storing data in a proper database, rather than a flat file, makes it far easier to query, analyze, and connect to visualization tools later.
- Power BI's DirectQuery mode is what makes a dashboard "live", without a report is just a snapshot of the past.
- Meaningful monitoring doesn't require expensive, specialized tools. A scripting language, a database, and a BI tool are enough to build something useful.
- Verifying data at the source (querying the database directly) that confirms the dashboard is showing what's actually being collected.

## 22. Possible Future Enhancements

- Add **threshold-based alerts**, notifying someone automatically if CPU, memory, or disk usage crosses a defined limit.
- Extend monitoring to **multiple machines**, rather than a single system, for organization-wide visibility.
- Add **historical trend analysis**, highlighting patterns over days or weeks rather than just the current moment.
- Optimize the data collection interval and storage approach for **longer-term, larger-scale** deployment.
- Add **data retention and archiving rules**, so the performance history doesn't grow indefinitely.
- Package the Python script as a **background service**, so it starts automatically and runs reliably without manual intervention.
