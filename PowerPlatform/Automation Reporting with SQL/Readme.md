# Automation Reporting with SQL

**Automation Playground Portfolio Project**

An automation that reports on the health of other automations. It queries a SQL database where automated processes log their outcomes, calculates a success rate, and emails a performance summary. Turning raw process logs into a report, where a stakeholder can read with no manual required.

## 1. Project Overview

This project automates the reporting side of running robot. It connects to a SQL Server database where an automated process has been logging the outcome of every case it handles, summarizes how many cases succeeded versus failed (and why), calculates an overall success rate, and emails that summary to a stakeholder automatically.

## 2. Business Context

Once a business has automations running regularly, we will know how well the bots are actually performing. Logs and databases full of individual case records are useful for troubleshooting.

## 3. Business Problem

Without a dedicated reporting, monitoring automation performance tends to fall into:

- **No one checks at all**, so problems can go unnoticed until they cause a real business impact.
- **Someone has to manually query logs or a database** every time they want a performance snapshot, which is slow and easy to skip when things get busy.
- **Raw data isn't the same as insight** a table full of individual case outcomes doesn't tell you, at a glance, whether the automation is healthy.

## 4. Project Objectives

- Automatically summarize the outcomes of processed cases stored in a database.
- Calculate a clear, overall success rate for the automation being monitored.
- Deliver this summary automatically, without requiring anyone to run a report manually.
- Make automation performance visible on a regular basis, not just when someone remembers to check.

## 5. What the Video Demonstrates

The video walks through a Power Automate Desktop flow:

- A connection to a **SQL Server database** ("ProcessedCaseDB"), which stores a record of every case handled by an automated process, including its result and timestamp.
- A SQL query that **groups and counts cases by outcome** (for example, how many were successfully processed versus how many failed due to invalid data).
- A second SQL query that **calculates the overall success rate** as a percentage.
- The results being assembled into a plain language **email summary** a report for the robot's performance, followed by the outcome breakdown and success rate.
- The email being sent automatically through **Outlook**, with the subject **"Robot Performance Report."**
- The Outlook inbox showing a **history of these reports sent over several days**, allowing performance to be tracked and compared over time, alongside related automated alerts (such as individual case failure notifications) from the same monitored process.
- **SQL Server Management Studio** being used directly to inspect the underlying data, confirming the case level records (case ID, which automation/flow it belonged to, its result, and when it was processed).

## 6. End-to-End Workflow, Step by Step

1. **Connect to the database.** The flow opens a connection to the SQL Server database storing processed case records.
2. **Summarize outcomes.** A query groups all recorded cases by their result (e.g., successful, or a specific type of failure) and counts each group.
3. **Calculate the success rate.** A second query works out what percentage of all cases were successful.
4. **Close the database connection.** Once the data has been retrieved, the connection is closed.
5. **Build the report.** The outcome breakdown and success rate are assembled into a readable email message.
6. **Send the report.** The email is sent automatically through Outlook to the relevant recipient.
7. **Repeat on a regular basis.** Run repeatedly over time, this produces a running history of performance reports that can be compared against each other.

## 7. Systems and Applications Involved

- **Microsoft SQL Server** — storing the case-level outcome data this report is built from
- **SQL Server Management Studio** — used to directly inspect and verify the underlying data
- **Microsoft Outlook** — used to deliver the performance report by email

## 8. Technologies Used

- **Power Automate Desktop** — for building the reporting automation
- **SQL query execution (Execute SQL statement)** — for summarizing and calculating performance data directly in the database
- **SQL aggregate functions (COUNT, CASE, ROUND)** — for grouping outcomes and calculating a success percentage
- **Outlook automation** — for composing and sending the report by email

## 9. Automation Logic

Rather than pulling raw data out of the database and processing it elsewhere, the heavy lifting is done directly in SQL: one query groups and counts cases by outcome, and a 2nd calculates the success percentage using conditional counting (counting only the "successful" cases and dividing by the total). This keeps the automation itself simple. It retrieves the summarized results, builds a short message around them, and sends it. The result is a lightweight, reliable reporting layer that can run on a schedule without needing to reprocess large amounts of raw data every time.

## 10. AI Capabilities

This project doesn't use AI. It is a SQL-driven reporting automation. Its value is in **making existing data useful**: turning a database table that only a technical person could interpret into a plain language summary that anyone can read and act on.

## 11. User Interactions

- This automation can runs unattended where no user interaction is required for it to generate and send its report.
- The primary interaction for a business stakeholder is simply **reading the email** that arrives in their inbox, with no need to log into a database or ask someone else for a status update.
- A technical user can independently verify the report's accuracy at any time by querying the same database directly.

## 12. Inputs and Outputs

**Inputs:**
- Case-level outcome records stored in a SQL Server database, each showing the result of a processed case and when it occurred

**Outputs:**
- A summarized breakdown of case outcomes (e.g., how many succeeded, how many failed and why)
- An overall success rate percentage
- An automatically delivered email report summarizing this information

## 13. Error Handling and Validation

- Because the summary is calculated directly from the same database the underlying automation logs to, the report reflects the actual, complete history of processed cases rather than a partial or manually assembled view.
- Using SQL's own counting and calculation logic (rather than manual tallying) reduces the risk of an incorrect summary.
- The database connection is explicitly opened and closed as part of the flow, keeping the automation's interaction with the database.

## 14. Business Rules

- Every case recorded in the database must be included in the outcome summary.
- The success rate must be calculated as the percentage of all cases that were specifically marked as successful.
- A report must be generated and delivered without requiring manual intervention.

## 15. Key Features Demonstrated

- Direct SQL-based summarization and calculation of process performance data
- Automatic composition of a plain-language performance report
- Automated email delivery of that report
- A verifiable link between the report and the underlying source data
- A reusable reporting that can run on a recurring basis

## 16. Business Value and Benefits

- **Effortless visibility.** Stakeholders receive a performance summary without having to ask for one or dig through data themselves.
- **Faster identification of issues.** A visible success rate and outcome breakdown makes it easy to notice if performance is slipping.
- **Reduced reporting overhead.** No one needs to manually query a database or compile a report by hand.
- **Trustworthy reporting.** Because the summary is generated directly from the same data the automation logs, there's no risk of a manually compiled report drifting from reality.
- **A foundation for broader monitoring.** The same way of doing can be extended to report on any automation that logs its outcomes to a database.

## 17. Productivity Improvements

- Removes the need for a person to manually query a database and compile a performance summary.
- Makes automation performance visible on a recurring basis without ongoing manual effort.
- Frees up technical staff from repeatedly answering "how is the robot doing?" by having the answer delivered automatically.

## 18. Time or Cost Savings (If Evident)

The video shows a performance report, covering the grouped outcome of many processed cases and an overall success rate was generated and emailed within seconds of the flow running. It doesn't demonstrate a direct time comparison against a manual reporting process, so no specific savings figure is claimed here. This was automatically generating and delivering a status report that would otherwise require someone to manually query a database and compile results is a reliable, low-effort way to save recurring reporting time.

## 19. Skills Demonstrated

- Writing and executing SQL queries for aggregation and calculation (COUNT, CASE, ROUND)
- Connecting an automation to a SQL Server database
- Building a lightweight, database-driven reporting automation
- Composing and sending automated email reports
- Verifying automated report output against the underlying source data
- Designing a reporting layer that complements a separate data-logging automation

## 20. Real-World Enterprise Use Cases

This reporting pattern applies to a wide range of operational monitoring needs, including:

- **RPA/automation health monitoring** — tracking success and failure rates across any bot or automated process
- **Batch job reporting** — summarizing the outcome of scheduled data processing jobs
- **Customer service or helpdesk metrics** — reporting on ticket resolution rates from a database
- **Quality assurance reporting** — summarizing test pass/fail rates from a results database
- **Any recurring "how did it go?" reporting need** — where data already exists in a database but isn't visible to the people who need it

## 21. Lessons Learned

- Doing summarization and calculation directly in SQL, rather than in the automation itself, keeps the automation simple and leverages the database's own strengths.
- A short email is often more useful to a stakeholder than access to the raw underlying data the value is in the summary, not just the numbers.
- Pairing a data-logging automation with a separate reporting automation is maintainable.
- Verifying automated reports against the underlying data (as shown using SQL Server Management Studio) builds justified confidence that the report is accurate.
- Recurring automated reporting turns monitoring from an occasional, manual chore into a continuous, low-effort habit.

## 22. Possible Future Enhancements

- Add **trend comparisons**, showing how the current success rate compares to previous reporting periods.
- Include **visual charts** in the email report, rather than plain text, for faster interpretation.
- Add **threshold-based alerting**, flagging the report differently (or notifying additional people) if the success rate drops below an acceptable level.
- Extend reporting to cover **multiple automations** in a single consolidated report.
- Schedule the report to run **automatically on a fixed cadence** (daily or weekly) via an orchestration platform.
- Add a **dashboard view** alongside the email report, for anyone who wants to explore the underlying data interactively.
