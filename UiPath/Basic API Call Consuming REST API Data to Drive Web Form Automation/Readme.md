# API Call: Consuming REST API Data to Drive Web Form Automation

A foundational RPA demonstration showing how to pull data from a REST API and use it to automatically fill out a web form, including a form specifically designed to test whether an automation can keep up when field positions change unpredictably. This project focuses on two core automation skills: calling and reading an API, and handling a dynamic, unpredictable web interface.

## 1. Project Overview

This project demonstrates a fundamental building block of modern automation: calling a REST API to retrieve data, and then using that data to complete a task in a separate application,filling out and submitting a web form. Rather than typing the test data by hand, the automation fetches a randomly generated user profile from a public API and feeds those details directly into the form fields, handling the fact that the form's layout shifts after every submission.

## 2. Business Context

Many real business processes involve pulling data from one system (often through an API) and using it to populate another system's interface. Customer details fetched from a CRM and entered into a portal, or product data pulled from an inventory API and entered into a supplier's web form. Being able to reliably call an API, understand its response, and use that data to drive a UI-based process is a core, widely applicable automation skill.

## 3. Business Problem

This project is a **skills demonstration** built around a well known RPA training exercise ("RPA Challenge"), rather than a specific live business system, but it's built to mirror a real and common automation challenge:

- **Manually re-entering data between systems is slow and error-prone.** Copying details from an API response or another data source into a web form by hand invites typos and inconsistencies.
- **Web forms aren't always static.** Some interfaces are intentionally or unintentionally unpredictable where fields can move, reload, or change order, which breaks automations that rely on fixed, hardcoded positions.
- **Automations need to be genuinely adaptive**, not just capable of clicking in the same spot every time.

The RPA Challenge site used in this demo is specifically designed to test that last point: it shuffles the form's field layout after every submission, forcing the automation to correctly identify each field by what it *is*, not where it happens to sit on the screen.

## 4. Project Objectives

- Demonstrate calling a public REST API and retrieving structured data from it.
- Demonstrate reading (deserializing) that data so it can be used elsewhere in the automation.
- Use the retrieved data to accurately complete a web form.
- Prove the automation can correctly fill the form even when field positions change between rounds.
- Build a clean, minimal example of the "API in, UI out" automation pattern.

## 5. What the Video Demonstrates

The video shows a UiPath project called **"Basic API Call,"** which:

- Makes an **HTTP GET request** to a public API (`randomuser.me/api/`) that returns a randomly generated user profile in JSON format, including name, email, phone number, address, and other details.
- **Deserializes** that JSON response so the individual data fields (like first name, last name, and email) can be used elsewhere in the workflow.
- Opens the **RPA Challenge** website, a widely used RPA practice site whose form intentionally rearranges its fields (First Name, Last Name, Company Name, Role in Company, Address, Email, Phone Number) after each submission, across multiple rounds.
- Automatically types the data retrieved from the API. For an example, "Mrs. Zoe Klyve," her generated email address, and phone number into the correct fields on the form, correctly matching each value to the right field regardless of its position on screen.

## 6. End-to-End Workflow, Step by Step

1. **Call the API.** The automation sends a request to a public REST API and receives a response containing a randomly generated user's details.
2. **Read the response.** The JSON response is deserialized, turning the raw data into values the automation can work with (name, email, phone, etc.).
3. **Open the target form.** The automation navigates to the web form that needs to be filled out.
4. **Identify each field.** Rather than relying on fixed screen positions, the automation identifies each form field by what it represents (e.g., "this is the First Name field"), regardless of where it currently sits on the page.
5. **Fill in the form.** Each piece of data from the API response is typed into its matching field.
6. **Submit and repeat.** The form is submitted, and the process can repeat across multiple rounds, even as the form's layout changes each time.

## 7. Systems and Applications Involved

- **A public REST API** (`randomuser.me`) used as the source of structured test data
- **RPA Challenge** — a web-based practice application designed to test dynamic form-filling automation

## 8. Technologies Used

- **UiPath Studio** — used to build the automation
- **UiPath Web API Activities (HTTP Request)** — for calling the REST API
- **JSON deserialization** — for reading the API's structured response
- **UiPath UI Automation Activities** — for interacting with and typing into the web form

## 9. User Interactions

- This automation runs unattended from start to finish. No user input is required once it's started.
- Its "interaction" is entirely with two systems: the API (to retrieve data) and the web form (to enter it). A good example of a fully self-contained, end-to-end automated task.

## 10. Inputs and Outputs

**Inputs:**
- A response from the REST API, containing a randomly generated user's details (name, email, phone, address, and more)

**Outputs:**
- A correctly completed and submitted web form, with each field filled using the matching data from the API response

## 11. Error Handling and Validation

- By identifying form fields based on what they represent rather than their fixed screen position, the automation is inherently more resilient to layout changes, the exact scenario this exercise is built to test.
- Reading the API response through proper JSON deserialization (rather than manually parsing text) reduces the risk of misreading or mismatching data fields.

## 12. Business Rules

- Each piece of retrieved data must be entered into its correctly corresponding form field where first name goes to First Name, email goes to Email, and so on, regardless of the field's position on screen.
- The automation must correctly complete the form across multiple rounds, even as the layout changes each time.

## 13. Business Value and Benefits

- **Removes manual data transfer** between an API-driven data source and a web-based system.
- **Builds more resilient automations** — ones that keep working even when a target interface's layout isn't perfectly predictable.
- **Establishes a reusable pattern** — this same API-to-form structure applies to many real business scenarios where data needs to move from a data source into a web application.

## 14. Productivity Improvements

- Eliminates manual copy and paste work between a data source and a web form.
- Removes the fragility of automations that break the moment a form's layout changes even slightly.

## 15. Real-World Enterprise Use Cases

This exact pattern to pull data from an API, then use it to complete a task in a separate interface which can applies to many real scenarios, including:

- **Populating a partner or vendor web portal** using data retrieved from an internal system's API
- **Filling out compliance or registration forms** with data sourced from an internal database via API
- **Testing or QA automation**, using API-generated sample data to exercise a form or application repeatedly
- **Any process where two systems don't share a native integration**, but one exposes an API and the other only offers a web interface
- **Automations that must remain functional despite UI changes**, a common real-world challenge with third-party or frequently updated web applications

## 16. Lessons Learned

- Reading data properly (through structured deserialization) rather than treating an API response as plain text makes downstream automation logic far more reliable.
- Automations that identify UI elements by what they are, rather than where they sit, are significantly more robust and this robustness matters even in "simple" automations, not just complex ones.
- A well-designed practice exercise (like the RPA Challenge site's shifting form) is a genuinely useful way to build and prove real automation skills, not just a novelty.
- Even a small, focused project is a good way to demonstrate a specific, transferable technical capability clearly.

## 17. Possible Future Enhancements

- Extend the automation to handle **multiple API records in sequence**, rather than a single retrieved profile.
- Add **error handling** for cases where the API call fails or returns unexpected data.
- Log each submission's data and outcome for later review or auditing.
- Adapt the same pattern to a **real business web portal**, rather than a training exercise, to demonstrate direct enterprise applicability.
- Combine this pattern with **data validation logic**, checking that retrieved data meets expected formats before it's entered into the form.

