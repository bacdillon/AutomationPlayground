# System Performance Monitoring with Python, SQL Server & Power BI

A real-time system monitoring solution that continuously collects a computer's performance data, stores it in a proper database, and visualizes it live on a Power BI dashboard. This project shows a complete, small-scale data pipeline, from data collection, through storage, to live reporting, built entirely from foundational tools.

## 1. Project Overview

This project continuously monitors a computer's performance, including CPU usage, memory usage, disk usage, and network activity, and streams that data into a live Power BI dashboard. A Python script collects system metrics in a constant loop and writes them into a SQL Server database, while Power BI connects directly to that database and updates its visuals in near real time. The result is a live, at-a-glance view of system health, built without any specialized monitoring software.

## 2. Business Problem & Objectives

**The problem:** Organizations rely on servers, workstations, and other systems staying healthy. Running out of memory, disk space, or network capacity can quietly degrade performance long before anything fails outright. Without a structured monitoring setup, these issues are easy to miss. Performance problems often build up gradually, so a slow memory leak or rising disk usage is not obvious without ongoing tracking. Raw system data is not useful on its own, since a stream of numbers from an operating system's performance counters means little without context or visualization. Manual checking does not scale, since no one can watch a system's live stats around the clock. Off-the-shelf monitoring tools are not always available or practical for every environment.

**The objectives:**
- Continuously collect key system performance metrics from a running computer.
- Store that data reliably in a structured, queryable database.
- Build a live dashboard that visualizes system health as it changes.
- Demonstrate a complete, working data pipeline, collection, storage, and visualization, using accessible, widely used tools.

## 3. Solution

A Python script (`performance.py`) runs continuously, using the `psutil` library to read live system metrics, including CPU usage, memory usage, CPU interrupts and calls, memory used and free, bytes sent and received over the network, and disk usage, and inserts a new record into a SQL Server database every second. Power BI then connects directly to that same database in DirectQuery mode, so the dashboard always reflects the latest data rather than a static snapshot.

### What the Video Demonstrates

SQL Server Management Studio is used to directly query the resulting `Performance` table, confirming that new rows of timestamped performance data are being reliably written in real time as the Python script runs. A Power BI dashboard, "System Information and Performance Monitoring," connected live to the same SQL Server database, shows CPU, disk, and memory usage as gauges, along with time-series charts for network activity and CPU activity, all refreshing automatically as new data streams in.

### End-to-End Workflow, Step by Step

1. **Collect system metrics.** The Python script continuously reads live performance data from the operating system: CPU, memory, disk, and network statistics.
2. **Write to the database.** On each loop cycle, the script inserts a new, timestamped record into a SQL Server table.
3. **Store a continuous history.** Over time, the database builds up a detailed, timestamped log of the system's performance.
4. **Connect a live dashboard.** Power BI connects directly to the SQL Server table using DirectQuery, rather than a static import, so it always reflects the latest data.
5. **Visualize in real time.** The dashboard's gauges and charts automatically refresh, showing current CPU, memory, and disk usage, along with trends in network and CPU activity over time.

## 4. Solution Architecture & Technologies

- **Microsoft SQL Server**, the database storing the collected performance data.
- **SQL Server Management Studio**, used to inspect and verify the stored data directly.
- **Microsoft Power BI**, the live dashboard visualizing the data.
- **Python**, running via Visual Studio Code, for writing the data collection script.
- **psutil**, a Python library for reading system performance metrics.
- **pyodbc**, a Python library for connecting to and writing into SQL Server.
- **DirectQuery**, Power BI's live-connection mode, used here so the dashboard reflects new data without manual refreshes or re-imports.

The core of the system is a simple but effective loop: read the current system metrics, write them to the database, and repeat continuously, with each cycle capturing a fresh timestamped snapshot of system health. Because the data is written directly into a proper database rather than a log file, it becomes immediately queryable and reportable. Connecting Power BI in DirectQuery mode, rather than importing a static snapshot of the data, is what turns this from a one-time report into a genuinely live monitoring dashboard. Every time the script writes a new row, the dashboard's next refresh reflects it.
