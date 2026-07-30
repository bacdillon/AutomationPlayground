# BMI Queue Automation: Dispatcher & Performer Pattern

**Automation Playground Portfolio Project**

A demonstration of one of the most fundamental design patterns in RPA — splitting an automation into a **Dispatcher** (which loads the work) and a **Performer** (which does the work), connected through a managed queue in UiPath Orchestrator. The example use case is calculating Body Mass Index (BMI) for a list of people, but the pattern itself is the real point: it's the same structure used for high-volume, production-grade automations of almost any kind.

---

## 1. Project Overview

This project automates the calculation of Body Mass Index (BMI) for a batch of people, using a two-part automation design: one component loads the data to be processed into a queue, and a separate component picks up each item from that queue, processes it, and reports the result. Behind a simple example (BMI calculation), this project is really a demonstration of a **scalable, production-ready automation architecture** — the same pattern used in real enterprise RPA solutions to process thousands of records reliably.

## 2. Business Context

Many business processes involve working through a list of records one at a time — invoices to check, applications to review, records to update, or in this case, people whose BMI needs to be calculated from height and weight data. When the volume is small, doing this by hand or with a simple script is fine. But as volume grows, or as the process needs to run reliably, be monitored, and recover from failures, a more structured approach is needed — one where the workload is clearly separated from the work itself.

## 3. Business Problem

Simple, single-file automations that both **load data** and **process it** in the same place run into problems as they scale:

- If the automation crashes partway through, it's often unclear which records were completed and which weren't.
- There's no easy way to track progress, retry failed items, or see the status of the batch while it's running.
- A single monolithic script is harder to scale — you can't easily split the work across more than one robot.
- Mixing "get the data" logic with "do the work" logic makes the automation harder to maintain and reuse.

The business need is a repeatable, trackable, and scalable way to process a list of items — with clear visibility into what's done, what's pending, and what failed.

## 4. Project Objectives

- Separate the automation into two clear responsibilities: loading data (Dispatcher) and processing data (Performer).
- Use a managed queue to track the status of every item, from start to finish.
- Automatically calculate BMI for each person using their height and weight.
- Give the business a clear, real-time view of processing status through Orchestrator.
- Demonstrate a pattern that can scale from a handful of records to large volumes without redesigning the automation.

## 5. What the Video Demonstrates

The video walks through a UiPath project called **BMI_Automation**, which includes two main workflows:

- **AddItemsToQueue** (the Dispatcher) — reads a list of people's height, weight, and status from an Excel file, and adds each row as an item to a queue in UiPath Orchestrator called **BMIQueue**.
- **GetQueueItemAndProcess** (the Performer) — picks up an item from the queue, opens a web-based BMI calculator, enters the person's height and weight, retrieves the calculated BMI result, and completes the transaction.

The video shows the queue in **UiPath Orchestrator** with four items loaded from the Excel source — two marked "Ready to process" and two marked "Not ready to process." As the Performer runs, it picks up and successfully completes the items marked "Ready to process," while the "Not ready to process" items are correctly left untouched. Each completed transaction is shown moving from "New" to **"Successful"** status in Orchestrator, along with its processing time and the underlying data (height, weight, status) attached to that transaction.

## 6. End-to-End Workflow, Step by Step

1. **Load the source data.** The Dispatcher reads a table of people's data (height, weight, and a status flag) from an Excel file.
2. **Add each item to the queue.** For every row, the Dispatcher creates a queue item in Orchestrator, carrying that person's data along with it.
3. **Items sit in the queue.** Orchestrator now holds a trackable list of work items, each with its own status.
4. **The Performer picks up an item.** It retrieves the next item from the queue, along with the data attached to it.
5. **The Performer calculates BMI.** It opens a BMI calculator web application, enters the person's height and weight, and retrieves the calculated BMI result.
6. **The transaction is completed.** The Performer reports the outcome back to Orchestrator, and the item's status updates to "Successful."
7. **Progress is visible throughout.** At any point, the current status of every item — pending, in progress, or completed — can be seen directly in Orchestrator.

## 7. Systems and Applications Involved

- **Microsoft Excel** — the source file containing the list of people and their height/weight data
- **UiPath Orchestrator** — hosts the queue, tracks every item's status, and provides monitoring
- **Web-based BMI calculators** — used to perform the actual BMI calculation, accessed through a browser

## 8. Technologies Used

- **UiPath Studio** — used to build the Dispatcher and Performer workflows
- **UiPath Excel Activities** — for reading the source data table
- **UiPath Orchestrator Queues** — for adding, tracking, and managing work items
- **UiPath UI Automation Activities** — for entering data into the web-based BMI calculator and reading back the result
- **Web browser automation (Chrome)** — used to interact with the BMI calculator application

## 9. Automation Logic

The core idea is a clean split of responsibility. The **Dispatcher** only cares about getting data ready — it doesn't calculate anything itself. It reads each row from the source file and adds it to the queue as a self-contained work item, carrying all the data the Performer will need. The **Performer** only cares about doing the work — it doesn't know or care where the data originally came from; it simply asks the queue for the next item, processes it, and reports back whether it succeeded. This separation means either part can be changed, scaled, or reused independently — for example, running several Performers at once to work through the queue faster, without touching the Dispatcher at all.

## 10. AI Capabilities

This project doesn't use AI decision-making — it's a classic, rules-based automation pattern. Its value doesn't come from intelligent judgment calls, but from **solid architecture**: reliable data handling, clear separation of concerns, and full trackability. It's a good demonstration that not every automation needs AI to be valuable — sometimes the right structural pattern is what makes an automation dependable at scale.

## 11. User Interactions

- This automation is designed to run **unattended** — no one needs to interact with it while it runs.
- A business user's main interaction is with **UiPath Orchestrator**, where they can see the queue, check how many items are pending or completed, and review the data and outcome for any individual item.
- If needed, a user can review each transaction's attached data (like height, weight, and status) directly from the transaction details in Orchestrator.

## 12. Inputs and Outputs

**Inputs:**
- An Excel file containing rows of people's data: height, weight, and a status flag
- Each queue item's attached data (height, weight, status), used by the Performer

**Outputs:**
- A calculated BMI result for each processed person
- An updated transaction status in Orchestrator (e.g., "Successful") for every completed item
- A clear, queryable record of which items were processed and which were not

## 13. Error Handling and Validation

- Because the work is managed through a **queue**, every item has a trackable status at all times — nothing is silently lost or skipped without a record of it.
- The video shows the automation correctly distinguishing between items that are **"Ready to process"** and items that are **"Not ready to process"** — only the ready items are picked up and completed, showing that the automation respects the state of the data rather than blindly processing everything.
- Because Dispatcher and Performer are separate, a failure in processing one item doesn't affect the loading of the rest of the batch, and doesn't require re-loading data that's already in the queue.

## 14. Business Rules

- Only records marked **"Ready to process"** should be picked up and completed by the Performer.
- Records marked **"Not ready to process"** must remain untouched in the queue until they're ready.
- Every record from the source file must be tracked as an individual queue item, with its own status, from the moment it's loaded.
- A completed calculation must be recorded back against its original transaction, so results can always be traced to their source data.

## 15. Key Features Demonstrated

- The classic **Dispatcher/Performer** automation pattern
- Queue-based work management using UiPath Orchestrator
- Status-based processing logic (only handling "ready" records)
- Automated web-based data entry and result retrieval
- Real-time visibility into batch processing status
- Clear separation between data loading and data processing logic

## 16. Business Value and Benefits

- **Reliability at scale.** Work is tracked item by item, so nothing gets lost, even if something goes wrong mid-batch.
- **Full visibility.** Anyone can check Orchestrator at any time to see exactly how a batch is progressing.
- **Reusability.** The Dispatcher and Performer can each be reused or modified independently — for example, swapping in a different data source without touching the processing logic.
- **Scalability.** Because the work sits in a queue, more than one robot could pick up items from the same queue to process a large batch faster.
- **Respect for data state.** The automation only processes records that are actually ready, avoiding wasted effort or incorrect processing.

## 17. Productivity Improvements

- Removes the need for someone to manually calculate BMI (or process any similar per-record task) one at a time.
- Makes it possible to track a batch's progress without asking anyone to check in manually — the status is always visible in Orchestrator.
- Sets up a reusable foundation that can process much larger batches without any redesign.

## 18. Time or Cost Savings (If Evident)

The video shows individual transactions completing in around 20 to 25 seconds each, including opening the calculator, entering data, and retrieving the result. With only four sample records, the video doesn't demonstrate large-scale savings directly, so no specific cost or time figure is claimed here. That said, the queue-based pattern shown is specifically designed for scale — the same setup that processes 4 records in this demo is built to handle thousands without any change in design, which is where the real time and cost savings would come from in a production setting.

## 19. Skills Demonstrated

- Designing automations using the Dispatcher/Performer (producer/consumer) pattern
- Working with UiPath Orchestrator queues, including adding, tracking, and monitoring items
- Reading and processing structured data from Excel
- Automating data entry and result extraction from a web application
- Applying business rules to control which records get processed
- Building automations with reusable, cleanly separated components

## 20. Real-World Enterprise Use Cases

This exact pattern is used across countless enterprise automation scenarios, including:

- **Invoice or claims processing** — loading a batch of documents into a queue, then processing each one individually
- **Data migration or record updates** — moving or updating large volumes of records reliably, with full tracking
- **Customer onboarding** — processing a batch of new applications or accounts one at a time, with clear status tracking
- **Bulk report generation** — generating a report or output for each item in a list, at scale
- **Any high-volume, per-record task** — where reliability, visibility, and scalability matter more than the specific task itself

## 21. Lessons Learned

- Separating "getting the work" from "doing the work" makes automations far easier to scale, maintain, and troubleshoot.
- A managed queue turns a batch of work into something trackable and recoverable, instead of a black box that either finishes or doesn't.
- Respecting the state of the data (like only processing "ready" records) is a simple but important business rule that prevents automations from doing the wrong thing at the wrong time.
- Even a simple example, like calculating BMI, is a great way to demonstrate a pattern that scales to far more complex, high-volume enterprise processes.
- Good automation architecture pays off long before an automation becomes complex — building it the right way from the start makes future growth much easier.

## 22. Possible Future Enhancements

- Add **automatic retries** for any item that fails during processing, instead of requiring manual follow-up.
- Introduce **multiple Performers** running at the same time, to process large batches faster.
- Add **validation rules** to catch bad input data (like an unrealistic height or weight) before it's processed.
- Store **calculated results** back into a central system or report, rather than just marking the transaction complete.
- Add **email or dashboard reporting** summarizing batch results once all items are processed.
- Extend the pattern to handle **other per-record business processes** beyond BMI calculation, reusing the same Dispatcher/Performer structure.

---

*This project is part of an Automation Playground portfolio, built to demonstrate a foundational, production-grade RPA design pattern — one that scales from a handful of records to enterprise-level volumes without changing its core structure.*
