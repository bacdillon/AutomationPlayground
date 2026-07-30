# Common Basic Test Automation: CRM Login Validation with SAP CX

**Automation Playground Portfolio Project**

An automated test suite, built on UiPath Test Suite, that validates the login experience of a SAP CX–style CRM application. The project checks that the right users can log in, catches failures cleanly if something breaks, reports results automatically, and is tracked in source control and monitored through an enterprise orchestration platform.

## 1. Project Overview

This project is a working example of **automated software testing**, applied to the login screen of a CRM application built in the style of SAP Customer Experience (SAP CX). Instead of a QA tester manually opening the app, typing credentials, and checking the result every time a change is made, this suite does it automatically logging in, verifying the outcome, and reporting back, every time it runs.

The suite is built using **UiPath Test Suite** (Studio, Test Manager, and Orchestrator), includes reusable test components, an object repository for UI elements, and automatic email reporting, and is version-controlled in GitHub.

## 2. Business Context

Login is the front door to almost every business application, including CRM platforms. If login breaks, even for a small reason like a UI change or a slow server which it can block an entire sales or service team from doing their job. Teams that release updates to their CRM regularly need a fast, repeatable way to check that login still works correctly after every change, without relying on someone manually testing it each time.

## 3. Business Problem

Manually testing a login flow, over and over, has real costs:

- It's repetitive and easy to get wrong, a tired or rushed tester can miss a real bug.
- It doesn't scale, as an application grows, there are more scenarios to check (valid login, invalid login, logout, different user roles) and less time to check them all by hand.
- It's slow to report by the time a manual tester finds and writes up an issue, time has already been lost.
- It's not repeatable in the same way every time, which makes it hard to trust the results when comparing one test run to the next.

The goal was to remove this manual burden for a core, high-impact flow login while keeping the same, or better, quality of testing.

## 4. Project Objectives

- Automatically verify that a user can log in to the CRM with valid credentials.
- Automatically verify that the system correctly rejects invalid credentials.
- Automatically verify that a user can log out successfully.
- Build the tests so they're reusable, maintainable, and not tied to one specific screen layout.
- Handle unexpected failures gracefully, instead of letting the test just crash with no explanation.
- Report results automatically, so the team knows the outcome without having to check manually.
- Track everything in source control and run it through an enterprise test/orchestration platform, the way a real QA pipeline would.

## 5. What the Video Demonstrates

The video walks through a real UiPath Studio project called **CRM**, built for testing a SAP CX style CRM application:

- The project structure, including three test cases: **"User can login with valid credentials,"** **"User login fails with invalid credentials,"** and **"User can logout,"** plus a data-driven test folder ("Testing with Excel Data Variation") for running the same test with multiple sets of input data.
- A shared reusable workflow, **"Loginsteps,"** that performs the actual login actions (entering the email, entering the password, clicking Logon, and checking the result) used by the test cases rather than duplicating that logic everywhere.
- A live run of the valid-login test: the automation opens the CRM application, logs in as user **Marcus Vance**, confirms the message **"Logon successful. Identity Verified: Marcus Vance,"** and lands on the CRM dashboard ("Global Sales Operations").
- A **deliberately simulated failure**: the CRM application becomes unavailable (an HTTP 404 error), which causes the automation to fail to find the expected login field. The video shows how the workflow catches this cleanly with a **Try/Catch** block, logs the error, and displays a clear troubleshooting message instead of crashing silently.
- An automatic **email report** sent after each run (e.g., "Executed: User can login with valid credentials"), clearly stating whether an error occurred (`Error Occurred: True` or `False`).
- The same test running successfully in **UiPath Orchestrator** (the enterprise execution and monitoring platform), including job logs and a monitoring dashboard showing job success rate.
- The project's **object repository**, which stores reusable definitions of UI elements (like the login and password fields) separately from the test logic.
- The project's history in **GitHub**, including commits, file changes, and branches, showing that the automation is developed and maintained the same way professional software is.

## 6. End-to-End Workflow, Step by Step

1. **Open the CRM application.** The test navigates to the CRM login page.
2. **Enter login details.** The shared "Loginsteps" workflow types in the user's email and password.
3. **Submit and check the result.** The workflow clicks "Logon" and checks whether login succeeded or failed.
4. **Confirm the outcome.** For a valid login, the test verifies the success message and that the correct user's dashboard loads. For an invalid login, the test verifies that access is correctly denied. For logout, the test verifies the user is properly signed out.
5. **Handle anything unexpected.** If something goes wrong during the test (for example, the application is down or a screen element can't be found), the workflow catches the error instead of failing silently, logs what happened, and shows a clear message.
6. **Send a report.** An email is automatically sent summarizing what was tested and whether an error occurred.
7. **Log and monitor centrally.** When run through Orchestrator, the same execution details are captured centrally, so the whole team can see test history and success rates in one place.

## 7. Systems and Applications Involved

- **SAP CX–style CRM application** (the system under test) — a web-based CRM login and dashboard experience
- **UiPath Studio** — where the test cases and shared workflows are built
- **UiPath Test Manager** — for organizing test cases into test sets
- **UiPath Orchestrator** — for running and monitoring test executions centrally
- **Gmail** — for automated email reporting of test results
- **GitHub** — for source control and change tracking
- **Internet Information Services (IIS)** — hosting the CRM application locally for testing

## 8. Technologies Used

- **UiPath Testing Activities** — purpose-built activities for structuring automated test cases
- **UiPath UI Automation Activities** — for interacting with the CRM's web interface (typing, clicking, verifying)
- **UiPath Object Repository** — for storing and reusing UI element definitions across tests
- **Excel-based data variation** — for running the same test with multiple sets of input data
- **UiPath Mail Activities** — for sending automated email reports
- **UiPath Orchestrator** — for centralized scheduling, execution, and monitoring
- **Git / GitHub** — for version control of the automation project

## 9. Automation Logic

Each test case follows the same reliable pattern: perform the login action, check the actual result against the expected result, and clearly report success or failure — with no ambiguous outcomes. The login steps themselves live in one shared, reusable workflow rather than being copied into every test case, so a change to the login process only needs to be made in one place. The whole thing is wrapped in error handling: if anything unexpected happens, the workflow doesn't just stop, it records what went wrong, flags it clearly, and still sends a report, so nothing fails silently.

## 10. AI Capabilities

This project is a traditional (non-AI) test automation solution. It doesn't use AI decision-making. The intelligence here comes from good test design: reusable components, a proper object repository, and structured, data-driven test cases, rather than from an AI model. 

## 11. User Interactions

- The automation itself runs unattended — no one needs to sit and watch it.
- A team member's main interaction is reading the **automated email report** after each run, which tells them clearly whether the test passed or failed.
- If deeper investigation is needed, the team can review the detailed run logs in **UiPath Studio** or **Orchestrator**, or check the version history in **GitHub**.

## 12. Inputs and Outputs

**Inputs:**
- Login credentials (including different sets of data when using the Excel data-variation test)
- The URL of the CRM application under test

**Outputs:**
- A clear pass/fail result for each test case
- A detailed run log (each action taken and its result, with timestamps)
- An automatic email report summarizing the test run and whether an error occurred
- Central execution history and monitoring data in Orchestrator

## 13. Error Handling and Validation

- Every login attempt is wrapped in a **Try/Catch** block, so unexpected issues (like a missing UI element or an unavailable application) are caught instead of crashing the test outright.
- When an error is caught, the workflow **logs the specific error message**, sets a clear error flag, and shows a descriptive message explaining what might have gone wrong and how to fix it.
- The test still completes and **reports its outcome by email**, even when something fails.
- The video shows this in action: when the CRM application was temporarily unavailable, the test correctly detected the problem, reported `Error Occurred: True`, and gave a clear explanation rather than leaving the team guessing.

## 14. Business Rules

- A login attempt with valid, correct credentials must succeed and load the correct user's dashboard.
- A login attempt with invalid credentials must be correctly rejected.
- A completed session must be able to log out cleanly.
- Every test run must produce a clear, reportable outcome as success, failure, or a clearly explained error.

## 15. Key Features Demonstrated

- A structured suite of test cases covering valid login, invalid login, and logout
- A shared, reusable login workflow instead of duplicated logic
- An object repository for maintainable UI element references
- Data-driven testing using Excel input variations
- Robust error handling with clear logging and messaging
- Automatic email reporting after every run
- Centralized execution and monitoring through UiPath Orchestrator
- Full version control and change history through GitHub

## 16. Business Value and Benefits

- **Confidence after every change.** Login can be re-verified automatically any time the application changes, instead of relying on someone remembering to check.
- **Faster feedback.** Automated email reports mean the team knows the result of a test run within minutes, not whenever a person gets around to checking.
- **Fewer missed issues.** Automation checks the same steps the same way every time, reducing the risk of a tired or rushed manual check missing a real problem.
- **Clear accountability and history.** GitHub tracks every change to the test suite itself, and Orchestrator tracks every execution, so there's a full, auditable trail.
- **Reusable foundation.** The object repository and shared login workflow make it easy to build more tests on top of this one without starting from scratch.

## 17. Productivity Improvements

- Removes the need for a person to manually repeat the same login checks after every application update.
- Cuts the time between "a change was made" and "we know if login still works" from however long a manual tester takes down to minutes.
- Makes it easy to test multiple scenarios (valid login, invalid login, different users) without needing a separate manual pass for each one.

## 18. Time or Cost Savings (If Evident)

The video shows individual test runs completing in about 20 to 40 seconds, including login and verification. It doesn't show large-scale numbers, so no specific dollar or hour savings figure is claimed here. A login check that used to require a person, now running unattended in under a minute with automatic reporting, a reliable source of time savings anywhere it's applied regularly, especially in teams that release frequently.

## 19. Skills Demonstrated

- Designing and building automated UI test cases with UiPath Test Suite
- Structuring reusable, maintainable automation using shared workflows and an object repository
- Building data-driven tests using Excel input variation
- Implementing proper error handling and logging in an automation solution
- Setting up automated email reporting for test outcomes
- Deploying and monitoring automated tests through UiPath Orchestrator
- Managing an automation project with Git and GitHub, including commit history and branching

## 20. Real-World Enterprise Use Cases

This same approach applies well beyond CRM login testing, including:

- **Regression testing** — automatically re-checking core application flows after every release
- **Multi-application login testing** — verifying single sign-on or login across several connected systems
- **Form and workflow validation** — checking that key business forms (orders, tickets, applications) behave correctly
- **Release readiness checks** — running a suite of critical tests before a deployment goes live
- **Data-driven quality assurance** — testing the same flow against many different user roles, accounts, or input combinations
- **Continuous testing in CI/CD pipelines** — running these kinds of checks automatically as part of a software delivery pipeline

## 21. Lessons Learned

- Keeping shared logic (like the login steps) in one reusable workflow, instead of copying it into every test, makes the whole suite much easier to maintain.
- An object repository is worth the setup time. It keeps UI element references organized and makes tests far less fragile when the application's interface changes.
- Good error handling isn't optional in test automation. A test that crashes without explanation is almost as unhelpful as no test at all. Catching failures and reporting them clearly is what makes automation trustworthy.
- Automatic reporting (like the email summaries shown here) closes the loop. Automation that runs but doesn't tell anyone the result doesn't actually save time.
- Treating a test automation project like real software with source control, commit history, and a clear project structure, pays off as the suite grows.

## 22. Possible Future Enhancements

- Expand the suite to cover more CRM flows beyond login and logout, such as creating records, managing customer data, or working with sales pipelines.
- Add **scheduled runs** in Orchestrator so the suite executes automatically on a regular basis, not just on demand.
- Integrate results into a **team chat tool** (like Slack or Teams) in addition to email, for faster visibility.
- Expand the **data-driven testing** to cover a wider range of user roles and edge cases.
- Add a **dashboard** summarizing pass/fail trends over time, to help spot patterns (such as a screen that fails more often after certain changes).
- Connect the suite into a **CI/CD pipeline**, so tests run automatically whenever the application is updated.
