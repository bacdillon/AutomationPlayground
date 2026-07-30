# Basic API Integration: Extracting Data from a REST API into Excel

**Automation Playground Portfolio Project**

A foundational RPA demonstration showing how to pull multiple records from a REST API, in bulk, and save them into a clean, structured Excel spreadsheet with the number of records to retrieve configurable at run time. This project focuses on a core automation skill: turning repeated API calls into a usable, structured dataset.

## 1. Project Overview

This project automates the process of calling a REST API multiple times, collecting the data returned each time, and compiling all of it into a single Excel spreadsheet. Rather than manually calling an API and copying results one at a time, the automation asks how many records are needed, then loops through that many API calls automatically, building a clean table of results as it goes.

## 2. Business Context

Many business and technical processes need data pulled from an external system that only offers an API for supplier catalogs, market data, contact directories, and public data sources are common examples. Once retrieved, that data is often needed in a familiar, easy-to-use format like Excel, so it can be reviewed, shared, filtered, or fed into another process. Being able to reliably call an API repeatedly and consolidate the results into a spreadsheet is a common, practical automation need.

## 3. Business Problem

This project is a **testing demonstration** using a public test API (`randomuser.me`), rather than a specific business system, but it mirrors a genuinely common automation challenge:

- **Manually calling an API multiple times and copying the results is slow and tedious**, especially when many records are needed.
- **Raw API responses (JSON) aren't business-friendly** most business users want data in a spreadsheet, not a block of code-like text.
- **The number of records needed often varies** from one situation to the next, so a rigid, one-size script isn't as useful as one that can be told how much data to pull.

## 4. Project Objectives

- Automate repeated calls to a REST API to retrieve multiple records.
- Let the user specify how many records should be retrieved.
- Convert each API response from raw JSON into clean, usable data fields.
- Compile all retrieved records into a single, well-structured Excel file.
- Demonstrate a clean, reusable pattern for "API in, spreadsheet out" automation.

## 5. What the Video Demonstrates

The video shows a UiPath project called **"Basic API Extract data from API and save in Excel,"** which:

- Prompts the user with an **input dialog** asking, "How many data do you need to extract?" — allowing the number of records to be set at run time rather than being fixed in the automation.
- Repeatedly calls the **`randomuser.me` REST API**, once for each record requested, retrieving a randomly generated user profile in JSON format each time.
- **Deserializes** each JSON response and extracts the relevant fields with first name, last name, and email address.
- Adds each extracted record as a new row to a data table, building up the full result set as the loop runs.
- Writes the completed data table out to an **Excel file**, producing a clean spreadsheet with columns for First Name, Last Name, and Email, and one row per record retrieved (the video shows 15 such records successfully extracted and saved).

## 6. End-to-End Workflow, Step by Step

1. **Ask how many records are needed.** The automation prompts the user to specify the number of records to extract.
2. **Call the API.** For each record needed, the automation sends a request to the REST API and receives a response.
3. **Read the response.** Each JSON response is deserialized so its data (name, email, and other details) can be used.
4. **Extract the relevant fields.** The specific fields needed are first name, last name, email — are pulled out of each response.
5. **Add the record to the dataset.** Each extracted record is added as a new row to a running data table.
6. **Repeat until complete.** Steps 2–5 repeat until the requested number of records has been collected.
7. **Save to Excel.** Once all records are collected, the complete data table is written out to an Excel file.

## 7. Systems and Applications Involved

- **A public REST API** (`randomuser.me`) — used as the source of structured data
- **Microsoft Excel** — the output format where the extracted data is saved

## 8. Technologies Used

- **UiPath Studio** — used to build the automation
- **UiPath Web API Activities (HTTP Request)** — for calling the REST API repeatedly
- **JSON deserialization** — for reading each API response
- **UiPath Excel Activities** — for building and saving the resulting data table
- **Input Dialog** — for capturing the desired number of records at run time
- **A loop with a counter** — to control how many times the API is called

## 9. Automation Logic

The automation is built around a simple, reusable loop: ask how many records are needed, then repeat the "call API → read response → extract fields → add row" sequence exactly that many times, using a counter to track progress. Each pass through the loop is independent and self-contained, which makes the whole process easy to follow and easy to extend — for example, adding more fields to extract, or writing to a different output format, without changing the overall structure. Making the record count a run-time input, rather than a fixed number, means the same automation can be used for a quick 5-record test or a much larger batch without any changes to the workflow itself.

## 10. AI Capabilities

This project doesn't use AI. It is just a demonstration of core, deterministic RPA and data-handling skills: calling an API repeatedly, parsing structured responses, and compiling results into a usable format. It's an example of how much practical value can come from foundational automation engineering, without needing AI involved.

## 11. User Interactions

- The only interaction required is at the start: the user is asked how many records to extract, through a simple input prompt.
- After that, the automation runs entirely unattended, looping through the API calls and building the spreadsheet without further input.
- The end result with a ready to use Excel file — is what the user interacts with afterward.

## 12. Inputs and Outputs

**Inputs:**
- The number of records to extract, provided by the user at the start of the run
- Repeated responses from the REST API, one per record requested

**Outputs:**
- A single Excel file containing one row per extracted record, with columns for First Name, Last Name, and Email

## 13. Error Handling and Validation

- Because each record is retrieved and processed in its own loop iteration, an issue with a single API call is contained to that iteration rather than affecting records already successfully retrieved.
- Reading each response through proper JSON deserialization, rather than manually parsing raw text, reduces the risk of incorrectly reading or mismatching data fields.
- Using a counter-driven loop tied directly to the user-specified record count ensures the automation retrieves exactly as many records as requested.

## 14. Business Rules

- The number of records extracted must match what the user specifies at the start of the run.
- Each record retrieved from the API must be represented as its own row in the output spreadsheet.
- Every record must include the same set of fields (First Name, Last Name, Email), keeping the output consistently structured.

## 15. Key Features Demonstrated

- Repeated, loop-driven REST API calls
- Run-time configurable record count via a simple input prompt
- Structured extraction of specific fields from JSON responses
- Automatic construction of a data table from repeated API results
- Clean, ready-to-use Excel output

## 16. Business Value and Benefits

- **Removes manual, repetitive API calls and data copying.**
- **Produces business-friendly output** (Excel) from a technical data source (a JSON API), without requiring the end user to understand JSON at all.
- **Scales to different needs** the same automation can pull a handful of records or a much larger batch, just by changing the number entered at the start.
- **Establishes a reusable pattern** for any scenario where bulk data needs to move from an API into a spreadsheet.

## 17. Productivity Improvements

- Eliminates the need to manually call an API multiple times and transcribe each result.
- Removes the manual step of converting raw JSON data into a usable spreadsheet format.
- Lets a user request exactly the amount of data they need, without any automation redevelopment.

## 18. Time or Cost Savings (If Evident)

The video shows 15 records being retrieved from the API and compiled into Excel in well under a minute of runtime. Because this is a training/demonstration exercise using a public test API rather than a live production data source, no real-world volume or cost savings figures apply here. The underlying capability is turning repeated API calls into a clean spreadsheet automatically, it is a common source of real time savings anywhere a business needs bulk data pulled from an API on a regular basis.

## 19. Skills Demonstrated

- Making repeated REST API calls within a controlled loop
- Deserializing and extracting specific fields from JSON responses
- Building a data table incrementally from repeated automation steps
- Capturing user input to control automation behavior at run time
- Producing clean, structured Excel output from an external data source

## 20. Real-World Enterprise Use Cases

This cause the loop through an API, extract fields, compile into a spreadsheet that can applies to many real business scenarios, including:

- **Pulling contact or customer lists** from a CRM or marketing platform's API into a report
- **Extracting product or pricing data** from a supplier's API for internal review
- **Compiling market or financial data** from a public or subscription API into an analysis-ready spreadsheet
- **Gathering survey or form response data** from a platform's API for reporting
- **Any scenario where data lives behind an API** but needs to be reviewed, shared, or analyzed in a spreadsheet

## 21. Lessons Learned

- A simple loop-and-counter structure is often all that's needed to turn a single API call into a robust, repeatable bulk-extraction process.
- Letting the user specify how much data to pull (rather than hardcoding a fixed number) makes an automation far more flexible and reusable.
- Converting technical API responses into a clean, familiar format like Excel is often what makes a technical capability actually usable by a business audience.
- Even a small, focused project is a good way to demonstrate a specific, transferable data-handling capability clearly.

## 22. Possible Future Enhancements

- Add **error handling** for individual failed API calls, so one failure doesn't stop the rest of the batch.
- Extract **additional fields** from each API response (such as phone number, address, or date of birth) for richer output.
- Add **duplicate checking**, in case the same record is retrieved more than once.
- Allow the output format to be chosen at run time (Excel, CSV, or a database table).
- Adapt the same pattern to a **real business API**, rather than a public test API, to demonstrate direct enterprise applicability.