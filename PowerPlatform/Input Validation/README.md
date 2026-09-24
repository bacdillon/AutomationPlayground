# Input Validation Before Submission

A demonstration of a core automation engineering practice: checking data for correctness before using it, rather than assuming it's good and finding out the hard way. This project reads a list of new customer records, validates each one's name, zip code, and email address against clear rules, and only submits genuinely valid records into an external Microsoft Form, recording a specific, human-readable reason for every record that fails.

## 1. Project Overview

This project automates the process of registering new customers through a Microsoft Form, but its real focus is on doing that safely. Before any customer's details are ever typed into the form, the automation checks their name, zip code, and email address against a defined set of rules. Records that pass are submitted automatically. Records that fail are never submitted at all. Instead, the exact reason for the failure is written back into the source spreadsheet, so a person can see precisely what needs fixing.

## 2. Business Problem & Objectives

**The problem:** Any process that takes data from one place, such as a spreadsheet, a database export, or a customer-provided form, and feeds it into another system depends on that data actually being usable. Real-world data is rarely perfectly clean. People mistype emails, leave off spaces in names, or enter "I don't know" in a field that expects a number. Feeding unchecked data into a downstream system creates predictable problems: bad data can cause a submission to fail outright, especially when the receiving system enforces its own rules; a failed submission with no clear reason wastes time, since someone has to go back and guess what was wrong; processing a whole batch without checking data first risks wasted effort on records that were always going to be rejected; and without a specific, recorded reason for each failure, there is no efficient way to know which records need correcting or how.

**The objectives:**
- Check every customer record against clear validation rules before using it.
- Catch specific, common data problems: invalid zip codes, malformed email addresses, and improperly formatted names.
- Only submit records that pass validation into the external form.
- Record a precise, understandable reason for every record that fails validation.
- Process the full batch without letting one bad record stop or corrupt the run.

## 3. Solution

A Power Automate Desktop flow, "Input Validation," processes a list of new customer records from an Excel file. For each record, the flow calls dedicated validation subflows, `Validation_Name`, `Validation_ZipCode`, and `Validation_Email`, each checking that specific field against its own rules. Records that pass all three checks are automatically entered into a live Microsoft Form ("Create new customer"). Records that fail validation are never submitted to the form at all. Instead, the flow writes the exact reason for the failure directly into a Status column in the same spreadsheet.

### What the Video Demonstrates

The source spreadsheet (`NewCustomers.xlsx`) contains customer names, zip codes, and email addresses, several of which are deliberately invalid, covering a range of realistic data problems: a zip code entered as the text "Don't know my zip code," a zip code starting with a leading zero, a zip code with only three digits, an email containing two `@` symbols, an email missing the `.` after the `@`, and a name with no space between first and last name. Records that pass validation have their full name, zip code, and email address typed in and the form submitted, with a "Your response was submitted" confirmation shown. Records that fail are recorded with a specific reason, for example "The zip code was not in a numeric format," "The email address contained more than one '@'," or "The name did not contain any space characters." The flow also includes retry logic for reliably reaching the target form, checking whether the correct browser window is already open, and if not, launching and navigating to it, retrying up to three times with a short wait between attempts if the page hasn't loaded yet. The final spreadsheet, reviewed at the end, shows every one of the ten records with a clear outcome: either "Okay" or a specific, readable explanation of what was wrong.

### End-to-End Workflow, Step by Step

1. **Load the customer data.** The flow reads all customer records from the source Excel spreadsheet.
2. **Prepare the target form.** The flow ensures the Microsoft Form is open and ready, retrying if needed before proceeding.
3. **Process each customer record in turn.** For every record, the flow extracts the name, zip code, and email address, then validates the name (checking that it contains a space separating first and last name), the zip code (checking that it's numeric, doesn't start with zero, and has the correct number of digits), and the email address (checking that it contains exactly one `@` and a `.` in the correct place afterward).
4. **Branch based on the validation result.** If every check passes, the flow fills in and submits the customer's details on the Microsoft Form. If any check fails, it skips the submission and records the specific reason in the spreadsheet's Status column instead.
5. **Repeat for every record.** This continues automatically until all ten customers have been processed.
6. **Review the results.** The completed spreadsheet shows, for every customer, either a successful outcome or an exact explanation of what needs to be corrected.

## 4. Solution Architecture & Technologies

- **Microsoft Excel**, the source of customer records and the destination for validation results.
- **Microsoft Forms**, the external system customer details are submitted into once validated.
- **Microsoft Edge**, the browser used to interact with the Microsoft Form.
- **Power Automate Desktop**, for building the main flow and its dedicated validation subflows.
- **Excel automation activities**, for reading customer data and writing back validation results.
- **Custom validation logic**, implemented as separate, reusable subflows for name, zip code, and email checks.
- **Browser automation activities**, for reliably opening, detecting, and interacting with the target Microsoft Form.
- **Conditional (If/Else) and retry logic**, for handling both data validation outcomes and page-load reliability.

Every customer record follows the same clear path: check the name, check the zip code, check the email, and only if all three pass, proceed to submit the record. Each of these checks lives in its own dedicated subflow, meaning the validation rules for a name, a zip code, and an email are each self-contained and easy to test, understand, or update independently. This "validate first, act second" order is what separates a defensive, production-ready automation from one that simply hopes the data is clean.

## 5. Controls & Validation

- Every field is checked against specific, well-defined rules. This project's error handling is its core purpose, not an afterthought.
- Each failure is captured with a precise, human-readable message, rather than a generic "invalid data" flag, telling the reviewer exactly what's wrong and, implicitly, how to fix it.
- Because validation happens before the form submission step, invalid data never reaches the external system at all, avoiding failed or rejected submissions there.
- The flow also handles a separate, technical kind of reliability issue, making sure the target web page has actually loaded, using a retry loop with a defined limit, rather than assuming the page will always be ready immediately.
- A record must pass all validation checks before it can be submitted to the external form, and every record, whether it passes or fails, must have its outcome recorded in the spreadsheet.

## 6. Business Value

- **Prevents wasted effort.** Invalid records are never submitted, avoiding failed attempts against the external system.
- **Makes fixing bad data fast and easy.** Specific error messages mean no one has to investigate or guess what went wrong.
- **Protects data quality downstream.** Only properly formatted, valid customer records make it into the target system.
- **Builds trust in the automation.** A process that clearly explains its own failures is far easier to trust and maintain than one that fails silently or vaguely.
- **Scales safely.** The same validate-then-act pattern works whether there are ten records or ten thousand.

## 7. Skills Demonstrated

- Designing and implementing field-level data validation logic.
- Structuring validation rules as clean, reusable subflows.
- Building conditional automation logic that only acts on verified-good data.
- Writing specific, actionable error messages back to a source system.
- Implementing reliable web automation with retry logic for page-load timing.
- Applying a defensive, "validate before you act" design philosophy to RPA.

## 8. Enterprise Use Cases

This validate-before-submit pattern applies to virtually any process that feeds data into another system, including:

- **Customer or lead data entry**, as demonstrated here.
- **Financial transaction processing**, where invalid account numbers or amounts must be caught before submission.
- **HR or employee onboarding data**, validating details before they're entered into a core HR system.
- **E-commerce order processing**, checking shipping addresses or payment details before an order proceeds.
- **Any data migration or integration task**, where the source data can't be fully trusted and needs to be checked before it reaches its destination.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Validating data before acting on it, rather than acting first and handling failure after, prevents wasted effort and produces much clearer, more useful results.
- Specific, descriptive error messages are far more valuable than a generic "invalid" flag. They turn a failure into something a person can immediately act on.
- Breaking validation logic into separate subflows per field keeps each rule focused, easy to understand, and easy to update independently.
- Real-world test data with intentionally varied, realistic mistakes, rather than only obviously broken examples, is what actually proves a validation system works.
- Even simple, deterministic rule-checking, done thoroughly and communicated clearly, is one of the most valuable things a good automation can do.

**Future enhancements:**
- Add automatic correction suggestions for common mistakes, such as detecting and fixing a missing `.` in an email domain.
- Extend validation to include duplicate detection, catching customers who may already exist in the system.
- Add a summary report showing how many records passed, failed, and why, across all validation rules.
- Allow corrected records to be automatically re-validated and resubmitted after a person fixes the flagged issue.
- Expand the rule set to cover additional fields, such as phone numbers or addresses, as the form grows.
- Package the validation subflows as a shareable component, so the same name, zip, and email checks can be reused in other automation projects.