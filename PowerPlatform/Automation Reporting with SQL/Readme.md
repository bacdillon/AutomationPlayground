# Automation Reporting with SQL

An automation that reports on the health of other automation. It queries a SQL database where automated processes log their outcomes, calculates a success rate, and emails a clear performance summary, turning raw process logs into a report a manager can read in seconds, with no manual digging required.

## 1. Project Overview

This project automates the reporting side of running robots in production. It connects to a SQL Server database where an automated process has been logging the outcome of every case it handles, summarizes how many cases succeeded versus failed and why, calculates an overall success rate, and emails that summary to a stakeholder automatically. It is the natural companion to a "validation and logging" automation elsewhere in this portfolio. That automation does the logging; this one does the reporting.

## 2. Business Problem & Objectives

**The problem:** Once a business has automation running regularly, a new question comes up: how do you know how well they are actually performing? Logs and databases full of individual case records are useful for troubleshooting, but they are not something a manager wants to read line by line. Teams need a simple, regular answer to "how did the robot do?" ideally delivered to them, rather than requiring someone to go looking for it. Without a dedicated reporting layer, monitoring automation performance tends to fall into one of two bad patterns. No one checks at all, so problems like a rising failure rate can go unnoticed until they cause a real business impact, or someone has to manually query logs or a database every time they want a performance snapshot, which is slow and easy to skip when things get busy. Raw data is not the same as insight. A table full of individual case outcomes does not tell you, at a glance, whether the automation is healthy.

**The objectives:**
- Automatically summarize the outcomes of processed cases stored in a database.
- Calculate a clear, overall success rate for the automation being monitored.
- Deliver this summary automatically, without requiring anyone to run a report manually.
- Make automation performance visible on a regular basis, not just when someone remembers to check.

## 3. Solution

A Power Automate Desktop flow, referred to as "Management Reporting," connects to a SQL Server database, "ProcessedCaseDB," which stores a record of every case handled by an automated process, including its result and timestamp. A SQL query groups and counts cases by outcome, for example how many were successfully processed versus how many failed due to invalid data, and a second query calculates the overall success rate as a percentage. The results are assembled into a plain-language email summary and sent automatically through Outlook.

### What the Video Demonstrates

The email summary reads "Here is your report for the robot's performance," followed by the outcome breakdown and success rate, and is sent with the subject "Robot Performance Report." The Outlook inbox shows a history of these reports sent over several days, allowing performance to be tracked and compared over time, alongside related automated alerts, such as individual case failure notifications, from the same monitored process. SQL Server Management Studio is also used directly to inspect the underlying data, confirming the case-level records, case ID, which automation or flow it belonged to, its result, and when it was processed, that the report is built from.

### End-to-End Workflow, Step by Step

1. **Connect to the database.** The flow opens a connection to the SQL Server database storing processed case records.
2. **Summarize outcomes.** A query groups all recorded cases by their result (successful, or a specific type of failure) and counts each group.
3. **Calculate the success rate.** A second query works out what percentage of all cases were successful.
4. **Close the database connection.** Once the data has been retrieved, the connection is cleanly closed.
5. **Build the report.** The outcome breakdown and success rate are assembled into a clear, readable email message.
6. **Send the report.** The email is sent automatically through Outlook to the relevant recipient.
7. **Repeat on a regular basis.** Run repeatedly over time, this produces a running history of performance reports that can be compared against each other.

## 4. Solution Architecture & Technologies

- **Microsoft SQL Server**, storing the case-level outcome data this report is built from.
- **SQL Server Management Studio**, used to directly inspect and verify the underlying data.
- **Microsoft Outlook**, used to deliver the performance report by email.
- **Power Automate Desktop**, for building the reporting automation.
- **SQL query execution (Execute SQL statement)**, for summarizing and calculating performance data directly in the database.
- **SQL aggregate functions (COUNT, CASE, ROUND)**, for grouping outcomes and calculating a success percentage.
- **Outlook automation**, for composing and sending the report by email.

Rather than pulling raw data out of the database and processing it elsewhere, the heavy lifting is done directly in SQL. One query groups and counts cases by outcome, and a second calculates the success percentage using conditional counting, counting only the "successful" cases and dividing by the total. This keeps the automation itself simple. It retrieves already-summarized results, builds a short message around them, and sends it. The result is a lightweight, reliable reporting layer that can run on a schedule without needing to reprocess large amounts of raw data every time. This project doesn't use AI. It's a straightforward, SQL-driven reporting automation, and its value is in making existing data useful: turning a database table that only a technical person could interpret into a plain-language summary that anyone can read and act on.

## 5. Controls & Validation

- Because the summary is calculated directly from the same database the underlying automation logs to, the report reflects the actual, complete history of processed cases rather than a partial or manually assembled view.
- Using SQL's own counting and calculation logic, rather than manual tallying, reduces the risk of an incorrect summary.
- The database connection is explicitly opened and closed as part of the flow, keeping the automation's interaction with the database clean and self-contained.
- Every case recorded in the database must be included in the outcome summary, none should be silently excluded, and the success rate must be calculated as the percentage of all cases specifically marked as successful.

## 6. Business Value

- **Effortless visibility.** Stakeholders receive a clear performance summary without having to ask for one or dig through data themselves.
- **Faster identification of issues.** A visible success rate and outcome breakdown makes it easy to notice if performance is slipping.
- **Reduced reporting overhead.** No one needs to manually query a database or compile a report by hand.
- **Trustworthy reporting.** Because the summary is generated directly from the same data the automation logs, there's no risk of a manually compiled report drifting from reality.
- **A foundation for broader monitoring.** The same pattern can be extended to report on any automation that logs its outcomes to a database.

## 7. Skills Demonstrated

- Writing and executing SQL queries for aggregation and calculation (COUNT, CASE, ROUND).
- Connecting an automation to a SQL Server database.
- Building a lightweight, database-driven reporting automation.
- Composing and sending automated email reports.
- Verifying automated report output against the underlying source data.
- Designing a reporting layer that complements a separate data-logging automation.

## 8. Enterprise Use Cases

This reporting pattern applies to a wide range of operational monitoring needs, including:

- **RPA and automation health monitoring**, tracking success and failure rates across any bot or automated process.
- **Batch job reporting**, summarizing the outcome of scheduled data processing jobs.
- **Customer service or helpdesk metrics**, reporting on ticket resolution rates from a database.
- **Quality assurance reporting**, summarizing test pass and fail rates from a results database.
- **Any recurring "how did it go?" reporting need**, where data already exists in a database but isn't visible to the people who need it.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Doing summarization and calculation directly in SQL, rather than in the automation itself, keeps the automation simple and leverages the database's own strengths.
- A short, plain-language email is often more useful to a stakeholder than access to the raw underlying data. The value is in the summary, not just the numbers.
- Pairing a data-logging automation with a separate reporting automation is a clean, maintainable pattern. Each piece has a single, clear responsibility.
- Verifying automated reports against the underlying data, as shown using SQL Server Management Studio, builds justified confidence that the report is accurate.
- Recurring automated reporting turns monitoring from an occasional, manual chore into a continuous, low-effort habit.

**Future enhancements:**
- Add trend comparisons, showing how the current success rate compares to previous reporting periods.
- Include visual charts in the email report, rather than plain text, for faster interpretation.
- Add threshold-based alerting, flagging the report differently or notifying additional people if the success rate drops below an acceptable level.
- Extend reporting to cover multiple automation in a single consolidated report.
- Schedule the report to run automatically on a fixed cadence, daily or weekly, via an orchestration platform.
- Add a dashboard view alongside the email report, for anyone who wants to explore the underlying data interactively.
