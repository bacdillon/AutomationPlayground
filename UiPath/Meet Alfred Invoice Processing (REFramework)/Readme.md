# Alfred: Intelligent Invoice Processing Automation (REFramework)

A production-grade, end-to-end invoice processing automation built on UiPath's REFramework, the industry-standard template for robust, enterprise-ready RPA. "Alfred" monitors an inbox for invoices, reads and understands them using AI-powered document processing, enters valid ones into a business system, flags invalid ones with a clear reason, and reports the results back to the team automatically.

## 1. Project Overview

This project automates the full lifecycle of processing incoming invoices, from the moment an email with invoice attachments arrives, through reading and understanding each invoice, entering its details into a business system, and reporting the outcome. It is built using UiPath's REFramework, a proven design pattern for automations that need to run reliably, handle errors gracefully, and behave predictably in a real production environment, not just in a demo.

## 2. Business Problem & Objectives

**The problem:** Businesses that receive invoices by email, from vendors, partners, or internal teams, typically need someone to open each attachment, read the details, and manually key them into an order entry or accounting system. This is repetitive, time-consuming work that also needs to be done carefully, since manual data entry is where costly mistakes tend to happen. As invoice volume grows, this becomes a real drag on a team's time and a real source of risk. Manually processing invoices is slow, since someone has to check the inbox, open each file, read it, and type the details into another system. It is error-prone, since manually retyping numbers, dates, and amounts is an easy place for mistakes to creep in, and it does not scale well, since more invoices simply means more hours spent on the same repetitive task. Bad data also causes bigger problems downstream, since an invoice missing a number or a customer address might get entered incorrectly instead of being caught and flagged, and there is often no clear record of what was processed, what wasn't, and why, until someone goes looking for it.

**The objectives:**
- Automatically detect and retrieve invoices arriving by email.
- Use AI-powered document understanding to read and extract data from each invoice, regardless of format (PDF or image).
- Validate the extracted data against business rules before doing anything with it.
- Automatically enter valid invoices into the business's order entry system.
- Clearly flag and report invoices that fail validation, along with the specific reason.
- Generate a consolidated summary report and email it to the team, with no manual reporting required.
- Build the automation on a resilient, production-ready framework rather than a fragile, one-off script.

## 3. Solution

"Alfred, Intelligent Invoice Processing Automation" (version 1.7) is a UiPath REFramework project made up of three coordinated stages: Intelligent Document Processing, Execute Order Entry Form, and Consolidate and Export Invoices. An Outlook inbox receives an email titled "Invoice Entry Request for Processing" with several invoice files attached, including PDFs and a JPG. The robot digitizes, classifies, and extracts data from each invoice using UiPath Document Understanding, then validates the extracted data before deciding whether to process it or flag it. Validated invoice data is entered into "Alfred Supermart," a custom Order Entry CRM application built with Python and Streamlit, running locally at `localhost:8501`.

### What the Video Demonstrates

Extracted invoice data with a missing invoice number, or missing customer and billing details, is correctly identified as a business rule exception rather than being processed incorrectly. Valid invoices are automatically entered into "Alfred Supermart," the Streamlit-based Order Entry CRM application, including customer details, invoice number, dates, line items, and totals, before being submitted. Automatic email notifications are sent for each invoice that fails validation, explaining exactly what was wrong, for example "Invoice Number is empty for: ABC Company." A consolidated Summary Report in Excel is generated at the end of the run, listing every invoice processed, its status, and, for failures, the specific reason, which is then emailed to the team. The automation also correctly handles a scenario where no new invoice email has arrived, sending a clear notification instead of failing or doing nothing silently.

### End-to-End Workflow, Step by Step

1. **Check for new invoices.** The robot monitors the Outlook inbox for a new "Invoice Entry Request" email with invoice attachments.
2. **Retrieve and store attachments.** Invoice files (PDF or image) are downloaded and saved for processing.
3. **Read and understand each invoice.** Using Document Understanding, each file is digitized, classified by document type, and its key data (customer, invoice number, dates, line items, totals) is extracted.
4. **Validate the data.** Each extracted invoice is checked against business rules, for example that the invoice number and customer billing details are not missing.
5. **Route based on validation result.** If valid, the invoice data is used to automatically fill out and submit the Order Entry Form in the business system. If invalid, the invoice is marked as a business rule exception, and an email is sent explaining exactly what is missing.
6. **Consolidate results.** Every invoice's outcome, success or exception, with details, is written to a summary spreadsheet.
7. **Report back to the team.** The summary report is emailed out automatically once processing is complete.
8. **Handle the no-data case.** If no new invoice email has arrived, the robot sends a clear notification instead of running unnecessarily or failing silently.

## 4. Solution Architecture & Technologies

- **Microsoft Outlook**, the inbox used to receive invoices and send notifications and reports.
- **UiPath Document Understanding**, for digitizing, classifying, and extracting data from invoice documents.
- **"Alfred Supermart"**, a custom Order Entry CRM application where validated invoice data is entered and submitted.
- **Python**, the language used to build the "Alfred Supermart" application.
- **Streamlit**, the Python framework powering the "Alfred Supermart" web interface, running locally at `localhost:8501`.
- **Microsoft Excel**, used for the consolidated summary report and per-invoice exported data.
- **UiPath REFramework**, the underlying design pattern providing structured initialization, transaction processing, and clean shutdown.
- **UiPath Mail Activities**, for monitoring the inbox and sending automated notifications and reports.
- **UiPath Excel Activities**, for exporting and consolidating extracted invoice data.
- **UiPath UI Automation Activities**, for interacting with the web-based Order Entry Form.
- **UiPath PDF Activities**, for working with PDF invoice files.

The automation follows the REFramework's proven structure. It starts by initializing everything it needs, settings, connections, applications, then works through invoices one at a time as individual transactions, and finishes with a clean shutdown regardless of what happened along the way. Each transaction has one of three possible outcomes: Success, where the invoice was valid and entered correctly; Business Exception, where the invoice itself has a data problem, like a missing invoice number, not a system failure; or System Exception, where something went wrong with the automation itself, like an unexpected application error. Separating these two exception types matters. A bad invoice and a broken robot are very different problems, and this framework treats them that way. A business exception gets flagged and reported, while a system exception can be retried automatically. Nothing is processed unless it passes validation, which keeps bad data out of the business system entirely.

**AI capabilities:** the automation does not just extract raw text. It classifies each document by type and pulls out specific, structured fields, such as customer name, invoice number, dates, line items, and totals, regardless of the invoice's layout. The same process handles both PDF invoices and image-based (JPG) invoices without separate logic for each, and the AI-extracted data is what the business rules validate against, so the quality of the AI extraction directly determines whether an invoice is processed correctly or correctly flagged as incomplete.

