# Input Validation

## 1. Project Overview

This project automates the process of registering new customers through a Microsoft Form, but its real focus is on doing that safely. Before any customer's details are ever typed into the form, the automation checks their name, zip code, and email address against a defined set of rules. Records that pass are submitted automatically. Records that fail are never submitted at all — instead, the exact reason for the failure is written back into the source spreadsheet, so a person can see precisely what needs fixing.

## 2. Business Context

Any process that takes data from one place (like a spreadsheet, a database export, or a customer-provided form) and feeds it into another system depends on that data actually being usable. Real-world data is rarely perfectly clean — people mistype emails, leave off spaces in names, or enter "I don't know" in a field that expects a number. A business collecting new customer records, and needing to register each one somewhere else, has to deal with exactly this kind of messiness.

## 3. Business Problem

Feeding unchecked data into a downstream system creates predictable problems:

- **Bad data can cause a submission to fail outright**, especially when the receiving system (like a web form) enforces its own rules, such as requiring a zip code to be numeric.
- **A failed submission with no clear reason wastes time**, since someone has to go back, guess what was wrong, and try to fix it.
- **Processing a whole batch without checking data first risks wasted effort** — attempting to submit obviously bad records, only to have them rejected one at a time.
- **Without a specific, recorded reason for each failure**, there's no efficient way to know which records need correcting or how.

## 4. Project Objectives

- Check every customer record against clear validation rules before using it.
- Catch specific, common data problems: invalid zip codes, malformed email addresses, and improperly formatted names.
- Only submit records that pass validation into the external form.
- Record a precise, understandable reason for every record that fails validation.
- Process the full batch without letting one bad record stop or corrupt the run.

## 5. What the Video Demonstrates

The video shows a Power Automate Desktop flow, **"Input Validation,"** processing a list of ten new customer records from an Excel file:

- The source spreadsheet (`NewCustomers.xlsx`) contains customer names, zip codes, and email addresses — several of which are **deliberately invalid**, covering a range of realistic data problems: a zip code entered as the text "Don't know my zip code," a zip code starting with a leading zero, a zip code with only three digits, an email containing two `@` symbols, an email missing the `.` after the `@`, and a name with no space between first and last name.
- For each record, the flow calls **dedicated validation subflows** — `Validation_Name`, `Validation_ZipCode`, and `Validation_Email` — each checking that specific field against its own rules.
- Records that **pass all three checks** are automatically entered into a live Microsoft Form ("Create new customer") — full name, zip code, and email address are typed in and the form is submitted, with a "Your response was submitted" confirmation shown.
- Records that **fail validation** are never submitted to the form at all. Instead, the flow writes the exact reason for the failure directly into a **Status** column in the same spreadsheet — for example, *"The zip code was not in a numeric format,"* *"The email address contained more than one '@',"* or *"The name did not contain any space characters."*
- The flow also includes **retry logic** for reliably reaching the target form: it checks whether the correct browser window is already open, and if not, launches and navigates to it, retrying up to three times with a short wait between attempts if the page hasn't loaded yet.
- The final spreadsheet, reviewed at the end, shows every one of the ten records with a clear outcome: either **"Okay"** or a specific, readable explanation of what was wrong.

## 6. End-to-End Workflow, Step by Step

1. **Load the customer data.** The flow reads all customer records from the source Excel spreadsheet.
2. **Prepare the target form.** The flow ensures the Microsoft Form is open and ready, retrying if needed before proceeding.
3. **Process each customer record in turn:**
   - Extract the name, zip code, and email address for that record.
   - Validate the **name** (checking, for example, that it contains a space separating first and last name).
   - Validate the **zip code** (checking that it's numeric, doesn't start with zero, and has the correct number of digits).
   - Validate the **email address** (checking that it contains exactly one `@` and a `.` in the correct place afterward).
4. **Branch based on the validation result:**
   - If every check passes, fill in and submit the customer's details on the Microsoft Form.
   - If any check fails, skip the submission and record the specific reason in the spreadsheet's Status column instead.
5. **Repeat for every record.** This continues automatically until all ten customers have been processed.
6. **Review the results.** The completed spreadsheet shows, for every customer, either a successful outcome or an exact explanation of what needs to be corrected.

## 7. Systems and Applications Involved

- **Microsoft Excel** — the source of customer records and the destination for validation results
- **Microsoft Forms** — the external system customer details are submitted into once validated
- **Microsoft Edge** — the browser used to interact with the Microsoft Form

## 8. Technologies Used

- **Power Automate Desktop** — for building the main flow and its dedicated validation subflows
- **Excel automation activities** — for reading customer data and writing back validation results
- **Custom validation logic** — implemented as separate, reusable subflows for name, zip code, and email checks
- **Browser automation activities** — for reliably opening, detecting, and interacting with the target Microsoft Form
- **Conditional (If/Else) and retry logic** — for handling both data validation outcomes and page-load reliability

## 9. Automation Logic

Every customer record follows the same clear path: check the name, check the zip code, check the email, and only if all three pass, proceed to submit the record. Each of these checks lives in its own dedicated subflow, meaning the validation rules for a name, a zip code, and an email are each self-contained and easy to test, understand, or update independently. When a record fails any check, the automation stops that record's progress *before* it ever reaches the external form — avoiding a wasted, likely-to-fail submission — and instead writes back a specific, human-readable explanation. This "validate first, act second" order is what separates a defensive, production-ready automation from one that simply hopes the data is clean.

## 10. AI Capabilities

This project doesn't use AI — it's a rules-based validation system, and that's the right choice here: the validation rules (is this numeric, does this contain a space, how many `@` symbols are there) are precise and well-defined, exactly the kind of check that deterministic logic handles reliably and transparently.

## 11. User Interactions

- This automation runs unattended, processing the full batch of customer records without needing anyone to intervene.
- A person's main interaction is **reviewing the completed spreadsheet** afterward, where every record's outcome — success or a specific failure reason — is clearly recorded.
- Because failure reasons are specific and written in plain language, a person can act on them directly (for example, correcting a customer's zip code) without needing to investigate what went wrong.

## 12. Inputs and Outputs

**Inputs:**
- A spreadsheet of new customer records, each with a name, zip code, and email address

**Outputs:**
- Successfully validated customer records submitted into the Microsoft Form
- An updated spreadsheet showing, for every record, either "Okay" or a specific validation failure reason

## 13. Error Handling and Validation

- Every field is checked against **specific, well-defined rules** — this project's error handling *is* its core purpose, not an afterthought.
- Each failure is captured with a **precise, human-readable message**, rather than a generic "invalid data" flag — telling the reviewer exactly what's wrong and, implicitly, how to fix it.
- Because validation happens **before** the form submission step, invalid data never reaches the external system at all, avoiding failed or rejected submissions there.
- The flow also handles a separate, technical kind of reliability issue — making sure the target web page has actually loaded — using a retry loop with a defined limit, rather than assuming the page will always be ready immediately.

## 14. Business Rules

- A zip code must be in numeric format, must not start with zero, and must be exactly four characters long.
- An email address must contain exactly one `@` symbol and a `.` appearing after it.
- A name must contain a space character, separating a first and last name.
- A record must pass **all** validation checks before it can be submitted to the external form.
- Every record — whether it passes or fails — must have its outcome recorded in the spreadsheet.

## 15. Key Features Demonstrated

- Field-level input validation using dedicated, reusable subflows
- Clear branching logic: validate first, then act only on valid data
- Specific, human-readable error messages for every type of validation failure
- Reliable web form interaction, including retry logic for page loading
- A complete, reviewable audit trail of every record's validation outcome

## 16. Business Value and Benefits

- **Prevents wasted effort.** Invalid records are never submitted, avoiding failed attempts against the external system.
- **Makes fixing bad data fast and easy.** Specific error messages mean no one has to investigate or guess what went wrong.
- **Protects data quality downstream.** Only properly formatted, valid customer records make it into the target system.
- **Builds trust in the automation.** A process that clearly explains its own failures is far easier to trust and maintain than one that fails silently or vaguely.
- **Scales safely.** The same validate-then-act pattern works whether there are ten records or ten thousand.

## 17. Productivity Improvements

- Removes the need for someone to manually check customer data for obvious problems before submission.
- Eliminates wasted time re-attempting form submissions that were always going to fail due to bad data.
- Speeds up data correction, since the exact issue is already identified and recorded for every failed record.

## 18. Time or Cost Savings (If Evident)

The video shows ten customer records validated and processed — six failing for six different, specific reasons, and four passing and being successfully submitted — in a single automated run lasting a few minutes. It doesn't demonstrate large-scale production volumes or a formal cost comparison against manual data checking, so no specific dollar or hour savings figure is claimed here. That said, catching bad data before it reaches a downstream system — rather than after a failed submission — is a well-established way to save meaningful time and rework, especially as data volume grows.

## 19. Skills Demonstrated

- Designing and implementing field-level data validation logic
- Structuring validation rules as clean, reusable subflows
- Building conditional automation logic that only acts on verified-good data
- Writing specific, actionable error messages back to a source system
- Implementing reliable web automation with retry logic for page-load timing
- Applying a defensive, "validate before you act" design philosophy to RPA

## 20. Real-World Enterprise Use Cases

This validate-before-submit pattern applies to virtually any process that feeds data into another system, including:

- **Customer or lead data entry**, as demonstrated here
- **Financial transaction processing**, where invalid account numbers or amounts must be caught before submission
- **HR or employee onboarding data**, validating details before they're entered into a core HR system
- **E-commerce order processing**, checking shipping addresses or payment details before an order proceeds
- **Any data migration or integration task** — where the source data can't be fully trusted and needs to be checked before it reaches its destination

## 21. Lessons Learned

- Validating data before acting on it — rather than acting first and handling failure after — prevents wasted effort and produces much clearer, more useful results.
- Specific, descriptive error messages are far more valuable than a generic "invalid" flag; they turn a failure into something a person can immediately act on.
- Breaking validation logic into separate subflows per field keeps each rule focused, easy to understand, and easy to update independently.
- Real-world test data with intentionally varied, realistic mistakes (rather than only obviously broken examples) is what actually proves a validation system works.
- Even simple, deterministic rule-checking — done thoroughly and communicated clearly — is one of the most valuable things a good automation can do.

## 22. Possible Future Enhancements

- Add **automatic correction suggestions** for common mistakes, such as detecting and fixing a missing `.` in an email domain.
- Extend validation to include **duplicate detection**, catching customers who may already exist in the system.
- Add a **summary report** showing how many records passed, failed, and why, across all validation rules.
- Allow **corrected records to be automatically re-validated and resubmitted** after a person fixes the flagged issue.
- Expand the rule set to cover **additional fields**, such as phone numbers or addresses, as the form grows.
- Package the validation subflows as a **shareable component**, so the same name/zip/email checks can be reused in other automation projects.

---

*This project is part of an Automation Playground portfolio, built to demonstrate a foundational best practice — validating data thoroughly before acting on it — that makes automations safer, clearer, and easier to trust.*
