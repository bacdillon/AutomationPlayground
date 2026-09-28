# Common Basic Test Automation: CRM Login Validation with SAP CX

An automated test suite, built on UiPath Test Suite, that validates the login experience of a SAP CX style CRM application. The project checks that the right users can log in, catches failures cleanly if something breaks, reports results automatically, and is tracked in source control and monitored through an enterprise orchestration platform.

## 1. Project Overview

This project is a working example of **automated software testing**, applied to the login screen of a CRM application built in the style of SAP Customer Experience (SAP CX). Instead of a QA tester manually opening the app, typing credentials, and checking the result every time a change is made, this suite does it automatically. It logs in, verifies the outcome, and reports back, every time it runs.

**A note on "SAP CX-style":** the application under test is a custom-built CRM, hosted locally through Internet Information Services (IIS) at `localhost/sap/default.html`, styled to look and behave like SAP Customer Experience, complete with a "Cloud Identity Services" login screen and a "Global Sales Operations" dashboard. It is not the licensed SAP CX product or SAP's actual cloud infrastructure. This is a common and reasonable approach for a training or portfolio project: it lets the automation be tested against realistic, SAP-style screens and terminology without requiring a live SAP environment or license.

The suite is built using **UiPath Test Suite** (Studio, Test Manager, and Orchestrator), includes reusable test components, an object repository for UI elements, and automatic email reporting, and is version controlled in GitHub.

## 2. Business Problem & Objectives

Login is the front door to almost every business application, including CRM platforms. If login breaks, even for a small reason like a UI change or a slow server, it can block an entire sales or service team from doing their job. Teams that release updates to their CRM regularly need a fast, repeatable way to check that login still works correctly after every change, without relying on someone manually testing it each time.

**The problem:** Manually testing a login flow, over and over, has real costs:

- It's repetitive and easy to get wrong. A tired or rushed tester can miss a real bug.
- It doesn't scale. As an application grows, there are more scenarios to check (valid login, invalid login, logout, different user roles) and less time to check them all by hand.
- It's slow to report. By the time a manual tester finds and writes up an issue, time has already been lost.
- It's not repeatable in the same way every time, which makes it hard to trust the results when comparing one test run to the next.

The goal was to remove this manual burden for a core, high-impact flow, login, while keeping the same, or better, quality of testing.

**The objectives:**

- Automatically verify that a user can log in to the CRM with valid credentials.
- Automatically verify that the system correctly rejects invalid credentials.
- Automatically verify that a user can log out successfully.
- Build the tests so they're reusable, maintainable, and not tied to one specific screen layout.
- Handle unexpected failures gracefully, instead of letting the test just crash with no explanation.
- Report results automatically, so the team knows the outcome without having to check manually.
- Track everything in source control and run it through an enterprise test and orchestration platform, the way a real QA pipeline would.

## 3. Solution

### What the Video Demonstrates

The video walks through a real UiPath Studio project called **CRM**, built for testing a SAP CX style CRM application:

- The project structure, including three test cases: **"User can login with valid credentials,"** **"User login fails with invalid credentials,"** and **"User can logout,"** plus a data-driven test folder ("Testing with Excel Data Variation") for running the same test with multiple sets of input data.
- A shared reusable workflow, **"Loginsteps,"** that performs the actual login actions (entering the email, entering the password, clicking Logon, and checking the result), used by the test cases rather than duplicating that logic everywhere.
- A live run of the valid-login test. The automation opens the CRM application, logs in as user **Marcus Vance**, confirms the message **"Logon successful. Identity Verified: Marcus Vance,"** and lands on the CRM dashboard ("Global Sales Operations").
- A **deliberately simulated failure**: the CRM application becomes unavailable (an HTTP 404 error), which causes the automation to fail to find the expected login field. The video shows how the workflow catches this cleanly with a **Try/Catch** block, logs the error, and displays a clear troubleshooting message instead of crashing silently.
- An automatic **email report** sent after each run (for example, "Executed: User can login with valid credentials"), clearly stating whether an error occurred (`Error Occurred: True` or `False`).
- The same test running successfully in **UiPath Orchestrator** (the enterprise execution and monitoring platform), including job logs and a monitoring dashboard showing job success rate.
- The project's **object repository**, which stores reusable definitions of UI elements (like the login and password fields) separately from the test logic.
- **A live commit and push to GitHub, demonstrated end to end (starting around the 11:08 mark).** From inside UiPath Studio's built-in source control panel, the developer reviews the modified files, types a commit message, and clicks **"Commit and Push."** Studio shows a **"Pushing changes..."** status while the push completes. A browser tab then switches to the live GitHub repository (`github.com/alfredbot01/CRM-SAP-Customer-Experience-CX`), confirming the change landed. The latest commit, **"Remove msg box,"** appears at the top of the file listing, the repository shows **17 total commits**, and the demonstration continues on to the repo's **Branches** page, showing `main` as the default branch, checked and up to date.

### End-to-End Workflow, Step by Step

1. **Open the CRM application.** The test navigates to the CRM login page.
2. **Enter login details.** The shared "Loginsteps" workflow types in the user's email and password.
3. **Submit and check the result.** The workflow clicks "Logon" and checks whether login succeeded or failed.
4. **Confirm the outcome.** For a valid login, the test verifies the success message and that the correct user's dashboard loads. For an invalid login, the test verifies that access is correctly denied. For logout, the test verifies the user is properly signed out.
5. **Handle anything unexpected.** If something goes wrong during the test, for example the application is down or a screen element can't be found, the workflow catches the error instead of failing silently, logs what happened, and shows a clear message.
6. **Send a report.** An email is automatically sent summarizing what was tested and whether an error occurred.
7. **Log and monitor centrally.** When run through Orchestrator, the same execution details are captured centrally, so the whole team can see test history and success rates in one place.

## 4. Solution Architecture & Technologies

- **A custom, SAP CX-styled CRM application** (the system under test), a locally hosted web application designed to look and behave like SAP Customer Experience, not the licensed SAP product itself.
- **UiPath Studio**, where the test cases and shared workflows are built.
- **UiPath Test Manager**, for organizing test cases into test sets.
- **UiPath Orchestrator**, for running and monitoring test executions centrally.
- **Gmail**, for automated email reporting of test results.
- **GitHub**, for source control and change tracking.
- **Internet Information Services (IIS)**, hosting the CRM application locally for testing.
- **UiPath Testing Activities**, purpose-built activities for structuring automated test cases.
- **UiPath UI Automation Activities**, for interacting with the CRM's web interface (typing, clicking, verifying).
- **UiPath Object Repository**, for storing and reusing UI element definitions across tests.
- **Excel-based data variation**, for running the same test with multiple sets of input data.
- **UiPath Mail Activities**, for sending automated email reports.
- **Git and GitHub**, for version control of the automation project, using UiPath Studio's built-in source control panel to commit and push changes directly, without leaving the IDE.

Each test case follows the same reliable pattern: perform the login action, check the actual result against the expected result, and clearly report success or failure, with no ambiguous outcomes. The login steps themselves live in one shared, reusable workflow rather than being copied into every test case, so a change to the login process only needs to be made in one place. The whole thing is wrapped in error handling. If anything unexpected happens, the workflow doesn't just stop. It records what went wrong, flags it clearly, and still sends a report, so nothing fails silently.
