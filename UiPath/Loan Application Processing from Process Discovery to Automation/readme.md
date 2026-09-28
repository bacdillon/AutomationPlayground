# UiBank Loan Application Processing

## 1. Project Overview

This project automates the process of submitting multiple loan applications to a bank's online application portal. Instead of manually typing each applicant's details into the web form one at a time, the automation reads a list of applicants and their loan details from an Excel spreadsheet, submits each one through the bank's actual web form, captures the outcome, approved or rejected, along with the resulting loan ID and interest rate, and writes that result straight back into the same spreadsheet.

## 2. Business Problem & Objectives

Banks and lenders process loan applications that typically start as structured data, an applicant's requested amount, term, income, and age. Getting that data from a source system (like a spreadsheet, a CRM, or an intake form) into the bank's actual application system, and then capturing the outcome, is a repetitive but essential step in loan processing. Any delay or manual error at this stage slows down the applicant's experience and adds unnecessary operational overhead.

**The problem:** Manually submitting a batch of loan applications creates familiar friction:

- **Manual data entry is slow and repetitive**, especially when the same set of fields needs to be filled in for every applicant.
- **Mistakes are easy to make** when re-typing amounts, terms, income figures, or ages by hand.
- **Capturing each application's outcome afterward**: the resulting loan ID, approval status, and rate, requires someone to go back and record it, which is easy to delay or forget.
- **Processing doesn't scale**: handling ten applications by hand takes noticeably longer than one, with proportionally more room for error.

**The objectives:**

- Automatically submit a batch of loan applications, sourced from a spreadsheet, into the bank's web-based application form.
- Correctly map each applicant's data to the right field on the form for every submission.
- Capture the outcome of each application, approval status, loan ID, and interest rate, directly from the system's response.
- Write those results back into the source spreadsheet, creating a single, complete record of what was submitted and what happened.
- Process the entire batch without manual intervention between applications.

## 3. Solution

### What the Video Demonstrates

The video shows a **Power Automate Desktop** flow, **"Robot 2 - Loan Application,"** processing a batch of loan applicants:

- The flow opens a web browser and navigates to the bank's loan application page, then opens an Excel file containing a list of applicants and their loan details (requester email, loan amount, loan term, yearly income, and age).
- For **each applicant in the spreadsheet**, the flow automatically fills in the web form, email, loan amount, loan term, income, and age, and submits the application.
- After each submission, the system returns a result: either an **approval**, showing a generated loan ID and an interest rate (APR), or a **rejection**, shown as "Not Approved."
- The flow captures this result and **writes it back into the Excel spreadsheet**, recording the loan status and loan ID against the correct applicant's row.
- The process repeats automatically for every applicant in the list, the video shows six different applicants processed in sequence, with four approved (at varying interest rates) and two rejected.
- Once the full batch is processed, the flow **saves and closes the Excel file** and closes the browser, leaving behind a spreadsheet that shows the original applicant data alongside the outcome of each submission.

### End-to-End Workflow, Step by Step

1. **Set up the target and starting point.** The flow defines the bank's application URL and sets a starting row counter for the spreadsheet.
2. **Open the required applications.** A web browser is launched to the loan application page, and the source Excel file is opened.
3. **Read the applicant data.** All rows of applicant information are read from the spreadsheet into memory.
4. **Loop through each applicant.** For every row of data:
   - The applicant's email, loan amount, loan term, income, and age are entered into the corresponding fields on the web form.
   - The application is submitted.
   - The result, approval status, loan ID, and interest rate, is read from the confirmation page.
   - That result is written back into the spreadsheet, in the row matching that applicant.
   - The form is reset for the next application.
5. **Repeat until the batch is complete.** This continues automatically for every applicant in the list.
6. **Finalize and clean up.** Once all applicants have been processed, the spreadsheet is saved and closed, and the browser session ends.

## 4. Solution Architecture & Technologies

- **UiBank**, the web-based loan application portal being automated
- **Microsoft Excel**, the source of applicant data and the destination for recorded results
- **A web browser (Firefox)**, used to interact with the loan application form
- **Power Automate Desktop**, for building and running the automation
- **Excel automation activities**, for reading applicant data and writing results back
- **Web/browser automation activities**, for filling in and submitting the loan application form
- **Loop (For Each) logic**, for processing every applicant in the spreadsheet automatically
- **Variables and flow control**, for tracking the current row and managing the process end-to-end

The flow is built around a simple, repeatable loop: for every row of applicant data, fill in the form, submit it, read the result, and record it, then move to the next row. A row counter keeps track of exactly where in the spreadsheet each result should be written, so outcomes are always recorded against the correct applicant. The automation itself doesn't decide who gets approved, that decision is made by the bank's own application system based on the submitted details (for example, in the demonstrated run, applicants requesting a loan amount disproportionate to their stated income were rejected). The automation's role is to reliably submit the data and faithfully capture whatever the system decides.

