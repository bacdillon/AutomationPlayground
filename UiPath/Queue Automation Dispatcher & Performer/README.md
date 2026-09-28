# Queue Automation: Dispatcher & Performer Pattern

A demonstration of one of the most fundamental design patterns in RPA: splitting an automation into a Dispatcher, which loads the work, and a Performer, which does the work, connected through a managed queue in UiPath Orchestrator. The example use case is calculating Body Mass Index (BMI) for a list of people, but the pattern itself is the real point. It is the same structure used for high-volume, production-grade automations of almost any kind.

## 1. Project Overview

This project automates the calculation of Body Mass Index (BMI) for a batch of people, using a two-part automation design: one component loads the data to be processed into a queue, and a separate component picks up each item from that queue, processes it, and reports the result. Behind a simple example, BMI calculation, this project is really a demonstration of a scalable, production-ready automation architecture, the same pattern used in real enterprise RPA solutions to process thousands of records reliably.

## 2. Business Problem & Objectives

**The problem:** Many business processes involve working through a list of records one at a time, whether that is invoices to check, applications to review, records to update, or in this case, people whose BMI needs to be calculated from height and weight data. When the volume is small, doing this by hand or with a simple script is fine. But as volume grows, or as the process needs to run reliably, be monitored, and recover from failures, a more structured approach is needed, one where the workload is clearly separated from the work itself. Simple, single-file automations that both load data and process it in the same place run into problems as they scale. If the automation crashes partway through, it is often unclear which records were completed and which weren't. There is no easy way to track progress, retry failed items, or see the status of the batch while it is running. A single monolithic script is harder to scale, since the work cannot easily be split across more than one robot, and mixing "get the data" logic with "do the work" logic makes the automation harder to maintain and reuse.

**The objectives:**
- Separate the automation into two clear responsibilities: loading data (Dispatcher) and processing data (Performer).
- Use a managed queue to track the status of every item, from start to finish.
- Automatically calculate BMI for each person using their height and weight.
- Give the business a clear, real-time view of processing status through Orchestrator.
- Demonstrate a pattern that can scale from a handful of records to large volumes without redesigning the automation.

## 3. Solution

A UiPath project, "BMI_Automation," splits the work into two workflows. AddItemsToQueue, the Dispatcher, reads a list of people's height, weight, and status from an Excel file, and adds each row as an item to a queue in UiPath Orchestrator called BMIQueue. GetQueueItemAndProcess, the Performer, picks up an item from the queue, opens a web-based BMI calculator, enters the person's height and weight, retrieves the calculated BMI result, and completes the transaction.

### What the Video Demonstrates

The queue in UiPath Orchestrator holds four items loaded from the Excel source, two marked "Ready to process" and two marked "Not ready to process." As the Performer runs, it picks up and successfully completes the items marked "Ready to process," while the "Not ready to process" items are correctly left untouched. Each completed transaction is shown moving from "New" to "Successful" status in Orchestrator, along with its processing time and the underlying data, height, weight, and status, attached to that transaction.

### End-to-End Workflow, Step by Step

1. **Load the source data.** The Dispatcher reads a table of people's data (height, weight, and a status flag) from an Excel file.
2. **Add each item to the queue.** For every row, the Dispatcher creates a queue item in Orchestrator, carrying that person's data along with it.
3. **Items sit in the queue.** Orchestrator now holds a trackable list of work items, each with its own status.
4. **The Performer picks up an item.** It retrieves the next item from the queue, along with the data attached to it.
5. **The Performer calculates BMI.** It opens a BMI calculator web application, enters the person's height and weight, and retrieves the calculated BMI result.
6. **The transaction is completed.** The Performer reports the outcome back to Orchestrator, and the item's status updates to "Successful."
7. **Progress is visible throughout.** At any point, the current status of every item, pending, in progress, or completed, can be seen directly in Orchestrator.

## 4. Solution Architecture & Technologies

- **Microsoft Excel**, the source file containing the list of people and their height and weight data.
- **UiPath Orchestrator**, hosting the queue, tracking every item's status, and providing monitoring.
- **Web-based BMI calculators**, used to perform the actual BMI calculation, accessed through a browser.
- **UiPath Studio**, used to build the Dispatcher and Performer workflows.
- **UiPath Excel Activities**, for reading the source data table.
- **UiPath Orchestrator Queues**, for adding, tracking, and managing work items.
- **UiPath UI Automation Activities**, for entering data into the web-based BMI calculator and reading back the result.
- **Web browser automation (Chrome)**, used to interact with the BMI calculator application.

The core idea is a clean split of responsibility. The Dispatcher only cares about getting data ready. It does not calculate anything itself. It reads each row from the source file and adds it to the queue as a self-contained work item, carrying all the data the Performer will need. The Performer only cares about doing the work. It does not know or care where the data originally came from. It simply asks the queue for the next item, processes it, and reports back whether it succeeded. This separation means either part can be changed, scaled, or reused independently, for example running several Performers at once to work through the queue faster, without touching the Dispatcher at all.
