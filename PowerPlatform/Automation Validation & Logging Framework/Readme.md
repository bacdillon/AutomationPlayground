# Automation Validation & Logging Framework

A demonstration of automation engineering practices in Microsoft Power Automate Desktop. Structured logging, per-record data validation, and error handling to built around a simple example task (adding pairs of numbers) so the underlying engineering pattern is easy to see clearly.

## 1. Project Overview

This project automates a simple task by reading pairs of numbers from a spreadsheet, adding them together, and recording the result but the real focus is on *how* it's built. The automation validates every input before using it, handles bad data gracefully instead of crashing, keeps a detailed, timestamped log of everything it does, and records the outcome of every single record it processes. The simple "add two numbers" task is really a stand-in for any repetitive business calculation or data-processing step; what this project demonstrates is the engineering discipline needed to make that kind of automation trustworthy at scale.

## 2. Business Context

Any automation that processes a batch of records such as invoices, orders, calculations, transactions, will eventually run into bad data: a missing value, a typo, a number entered as text. How an automation handles that moment determines whether it is production ready or just a fragile script that works until it doesn't. Businesses relying on automation need confidence that problems will be caught, logged clearly, and reported, not ignored or allowed to crash the entire batch.

## 3. Business Problem

Automations that skip proper validation and logging tend to fail in predictable, costly ways:

- **Bad input data can crash an entire batch**, rather than being handled gracefully as an isolated issue.
- **Without detailed logs, it's hard to know what actually happened** during a run, especially after the fact, when something needs to be investigated.
- **A single failure can go unnoticed** if there's no clear, per-record record of success or failure.
- **Troubleshooting becomes guesswork** without a timestamped trail showing exactly what the automation did, step by step.

## 4. Project Objectives

- Process a batch of records reliably, one at a time, without letting one bad record stop the whole batch.
- Validate every piece of input data before using it in a calculation.
- Handle invalid data gracefully, recording a clear reason rather than failing.
- Maintain a detailed, timestamped log of every action the automation takes.
- Record the outcome of every individual record, not just the batch as a whole.
- Demonstrate a reusable pattern for validation and logging that can be applied to any similar automation.

## 5. What the Video Demonstrates

The video walks through a Power Automate Desktop flow called **"Calculations with Logging,"** showing:

- A **Main flow** that reads a list of number pairs from an Excel file, then processes each row in turn.
- **Input validation** on every row for each number is explicitly converted to a numeric type before use, so a stray text value (like the word "Nine" typed into a number field) or a blank cell is caught immediately rather than miscalculated.
- The actual calculation being performed using a **real, external application**, the Windows Calculator for an example, automated to click the correct number and operator buttons and read back the result, showing UI automation working in concert with the data validation logic.
- **Error handling** built around each calculation: if a row's data is invalid, the flow catches the issue, records a specific status message (e.g., "The number B has an invalid value"), and moves on to the next row without stopping the batch.
- The final result being written back into the source spreadsheet, with a **Result** and **Status** column for every row to clearly showing which rows calculated successfully ("Valid") and which didn't, with a clear reason.
- A **detailed, timestamped CSV log file**, recording every step the automation took when workflow started, subflow started and end, each row being processed, and every validation error encountered along with references to the same information being recorded in a database.
- The completed results file being saved with a **timestamped filename**, so multiple runs can be kept and compared without overwriting previous results.

## 6. End-to-End Workflow, Step by Step

1. **Start the workflow and begin logging.** The flow records that it has started, along with a timestamp.
2. **Read the input data.** A list of number pairs is loaded from an Excel file.
3. **Process each row in turn.** For every row, the flow logs that it's processing that specific row.
4. **Validate the data.** Each number is converted to a proper numeric value; anything that fails this conversion is caught immediately.
5. **Perform the calculation.** For valid rows, the 2 numbers are added together using the Windows Calculator, automated through the UI.
6. **Handle any errors.** If a row's data was invalid, the flow records exactly what went wrong instead of stopping the process.
7. **Record the outcome.** Each row's result and status (Valid or a specific error reason) is written back to the spreadsheet.
8. **Log the outcome centrally.** The row's outcome is also recorded to a database, alongside the ongoing CSV log file.
9. **Repeat until complete.** The process continues through every row in the input file.
10. **Save the final results.** The completed spreadsheet is saved with a timestamped filename once all rows are processed.

## 7. Systems and Applications Involved

- **Microsoft Excel** — both the source of input data and the destination for results
- **Windows Calculator** — automated as the tool that actually performs each calculation
- **A database** — used to log workflow executions and individual record outcomes
- **A CSV log file** — recording a detailed, timestamped trail of every automation action

## 8. Technologies Used

- **Power Automate Desktop** — for building the automation
- **Power Automate Desktop subflows** — used to structure the automation into clear, reusable components (Main, Log_WriteTo, Get_Time, Read_Excel, Launch Calculator and Logon, Calculator_Add, ErrorHandling)
- **UI automation activities** — for interacting with the Windows Calculator application
- **Excel automation activities** — for reading input data and writing results
- **Error handling blocks** ("On block error") — for catching and responding to issues without stopping the whole process
- **CSV file writing** — for structured, ongoing logging
- **Database logging actions** — for recording workflow and per-record outcomes centrally

## 9. User Interactions

- This automation runs unattended from start to finish. No user interaction is required once it begins.
- After a run, a person can review the **results spreadsheet** to see the outcome of every record, or the **CSV log file** for a detailed, step-by-step account of what happened.
- Windows notifications confirm when a run has finished and where the results file was saved.

## 10. Inputs and Outputs

**Inputs:**
- A spreadsheet containing pairs of numbers to be processed

**Outputs:**
- An updated spreadsheet showing the result and status (Valid or a specific error reason)
- A timestamped results file, preserved separately from the original input
- A detailed CSV log file recording every step of the automation's execution
- Corresponding records logged to a database, tracking both the overall run and each individual row's outcome

## 11. Error Handling and Validation

- Every input value is explicitly validated (converted to a proper number) before being used where invalid data is caught immediately rather than causing a miscalculation or a crash.
- Errors are handled at the level of the individual row, bad record doesn't stop the rest of the batch from being processed.
- A dedicated error handling, the subflow captures the specific error that occurred, rather than a generic failure message.
- Every outcome success or failure, is explicitly recorded.

## 12. Business Rules

- Every number used in a calculation must be successfully validated as numeric before processing continues.
- A row with invalid data must be recorded with a specific, descriptive error rather than being skipped.
- Every row must have a final outcome recorded. Valid or a specific reason for failure with no row left unaccounted for.
- Every workflow run must produce a complete, timestamped log and a preserved results file.

## 13. Business Value and Benefits

- **Higher reliability.** Bad data doesn't derail the whole process, it is being recorded, and the batch continues.
- **Full traceability.** A detailed log means any run can be reviewed.
- **Faster troubleshooting.** Specific, descriptive error messages make it immediately clear what went wrong and where.
- **Confidence at scale.** The same validation and logging pattern that handles a handful of records works just as well for a much larger batch.
- **Reusable engineering pattern.** The subflow structure (logging, error handling, timestamps) can be reused across many other automations.

## 14. Productivity Improvements

- Removes the need for someone to manually check a batch of calculations for errors, since invalid data is automatically caught and reported.
- Reduces time spent troubleshooting automation issues, log in detailed, timestamped logs.
- Eliminates lost work from a single bad record crashing an entire batch process.

## 15. Real-World Enterprise Use Cases

The validation-and-logging pattern shown here applies to virtually any batch automation, including:

- **Financial calculations and reconciliations** — where bad input data must be caught, not silently miscalculated
- **Order or invoice processing** — validating each record before it's acted on
- **Data migration projects** — logging exactly what succeeded, what failed, and why, row by row
- **Any scheduled batch job** — where reliability and after the fact traceability matter
- **Automation frameworks and templates** — reusable logging and error handling patterns that other automations can be built on top of it

## 16. Lessons Learned

- Validating data, rather than assuming it's correct, is one of the simplest and most effective ways to prevent an automation from doing the wrong thing.
- Handling errors at the level of the individual record but not the whole batch. 1 bad entry doesn't cost the entire run.
- Detailed, timestamped logging turns "something went wrong" into "exactly what went wrong, when, and why," which makes troubleshooting dramatically faster.
- Structuring an automation into small, purpose-built subflows (logging, timestamps, error handling) makes it easier to build, test, and reuse than one long, monolithic flow.
- Even a simple example task can be a powerful way to demonstrate serious automation engineering discipline.

## 17. Possible Future Enhancements

- Extend the validation logic to catch additional types of bad data, such as out-of-range values.
- Add **automatic retries** for transient errors, separate from genuine data validation failures.
- Build a **summary dashboard** showing success/failure rates across multiple runs over time.
- Add **alerting**, notifying a team automatically if a run's failure rate crosses a certain threshold.
- Replace the Windows Calculator step with a direct calculation, and compare performance and reliability against the UI-automated approach.
- Package the logging and error-handling subflows as a **reusable template** for other automations to adopt directly.