# Common Basic Test Automation: CRM Login Validation with SAP CX Style

## 1. Project Overview

This project is an automated test suite, built with UiPath Test Suite, that validates the login flow of a custom CRM application styled to look and behave like SAP Customer Experience (SAP CX). The application under test is a locally hosted web app, served through Internet Information Services (IIS), designed with SAP-style branding and terminology. It is not the licensed SAP CX product itself. The suite goes beyond simply confirming that login works. It is specifically built to prove it behaves reliably when things go wrong, and it is developed and version controlled the same way professional software would be, using Git and GitHub directly from within UiPath Studio.

## 2. Business Problem & Objectives

**The problem:** Login is the entry point to almost every business application. If it breaks, even briefly, an entire team can be locked out of their tools. Teams that update their CRM regularly need a fast, repeatable way to confirm login still works after every change. Just as important, they need confidence that if something genuinely does break, the test will catch it clearly rather than passing quietly or crashing without explanation. And like any piece of software that will be maintained over time, the automation itself needs proper version control, not just a working script on one machine.

**The objectives:**
- Automatically verify that a user can log in to the CRM with valid credentials.
- Confirm the test correctly and visibly fails when the underlying application is unavailable, rather than giving a false pass.
- Report the outcome of every run automatically, including whether an error occurred.
- Track every execution centrally, so results are visible without needing to check the automation tool directly.
- Maintain the automation project under proper source control, with a full, traceable commit history.

## 3. Solution

A UiPath test project, structured around a reusable "Loginsteps" workflow, performs the actual login action: typing the email, typing the password, clicking Logon, and checking the result. The project uses an Object Repository, visible as a dedicated "Objects" folder in the project structure, to store reusable definitions of the CRM's UI elements separately from the test logic itself. A dedicated test case, "User can login with valid credentials," calls the shared login workflow and reports its outcome by email after every run. To prove the test's reliability, the project includes a deliberate failure scenario, where the CRM application's web server is stopped through IIS Manager and the test is run again while the application is offline. The whole project is version controlled in GitHub, with commits made and pushed directly from inside UiPath Studio.

**A note on test coverage:** the project's file structure includes three test cases: "User can login with valid credentials," "User login fails with invalid credentials," and "User can logout." Across both recordings, only the valid-login test case is shown actually executing, including its failure-mode variant with the CRM application taken offline. The invalid-login and logout test cases exist as files in the project but are not demonstrated running in either video, so their behavior is not documented here.

### What the Video Demonstrates

**A successful run.** The test opens the CRM application, logs in as user Marcus Vance, confirms the message "Logon successful. Identity Verified: Marcus Vance," and lands on the CRM dashboard ("Global Sales Operations"). An automated email arrives immediately afterward: "Executed: User can login with valid credentials... Error Occurred: False."

**A deliberately induced failure.** Using Internet Information Services (IIS) Manager, the CRM application's web server is stopped, taking the site offline, confirmed by an HTTP 404 "Not Found" error when visiting the site directly. The same test is run again. Because the login page's expected element is now unavailable, the test correctly fails with a clear error: "Type Into 'User ID / Business Email': Could not find the user-interface (UI) element for this action." The automated email report reflects this accurately: "Executed: User can login with valid credentials... Error Occurred: True." Three separate confirmation emails appear in the inbox across the demonstrations, one for each test execution, giving a clear, timestamped record of what happened and when.

**Centralized monitoring.** UiPath Orchestrator's Processes, Jobs, Agents, and Monitoring views are shown throughout, including the same "CRM" test process visible in the process list, a live jobs dashboard tracking success rate and average processing time, and the agent running the automation.

**A live commit and push to GitHub, demonstrated end to end (starting around the 11:08 mark of the longer recording).** From inside UiPath Studio's built-in source control panel, the developer reviews the modified files, types a commit message, and clicks "Commit and Push." Studio shows a "Pushing changes..." status while the push completes. A browser tab then switches to the live GitHub repository (`github.com/alfredbot01/CRM-SAP-Customer-Experience-CX`), confirming the change landed. The latest commit, "Remove msg box," appears at the top of the file listing, the repository shows 17 total commits, and the demonstration continues on to the repo's Branches page, showing `main` as the default branch, checked and up to date.

### End-to-End Workflow, Step by Step

1. **Open the CRM application.** The test navigates to the CRM login page.
2. **Enter login details.** The shared Loginsteps workflow types in the email and password.
3. **Submit and check the result.** The workflow clicks Logon and checks whether login succeeded or failed.
4. **Report the outcome by email.** An automated message is sent summarizing the run, including whether an error occurred.
5. **Simulate an outage.** The CRM application's web server is intentionally stopped through IIS Manager.
6. **Re-run the same test.** The test attempts the same login steps against the now-unavailable application.
7. **Detect and report the failure clearly.** The test correctly identifies that the expected page element cannot be found, fails the run, and sends an email explicitly reporting that an error occurred.
8. **Review centrally.** The outcome of every run can be confirmed through UiPath Orchestrator's job history and monitoring views.
9. **Commit and push changes.** Once a code change is made in the project, such as adjusting how errors are handled, the developer commits the change and pushes it directly from UiPath Studio to the project's GitHub repository.
10. **Verify on GitHub.** The commit is confirmed live on the GitHub repository page, including its commit message, position in the commit history, and branch status.

## 4. Solution Architecture & Technologies

- **UiPath Testing Activities**, used to structure the automated test case.
- **UiPath UI Automation Activities**, used to interact with the CRM's web interface.
- **A UiPath Object Repository**, storing reusable UI element definitions for the CRM application separately from the test logic, visible as a dedicated "Objects" folder in the project structure.
- **A shared reusable workflow ("Loginsteps")**, containing the core login logic used by the test case.
- **UiPath Mail Activities**, used to send an automated email report after every run.
- **UiPath Orchestrator**, used for centralized job execution, agent and machine monitoring, and process tracking.
- **A custom, SAP CX-styled CRM application**, hosted locally through Internet Information Services (IIS), designed to look and behave like SAP Customer Experience without being the licensed SAP product. IIS Manager is also used to intentionally take the application offline for failure testing.
- **Git and GitHub**, for version control of the automation project, using UiPath Studio's built-in source control panel to commit and push changes directly, without leaving the IDE.

## 5. Controls & Validation

- **Every run produces an explicit, accurate outcome.** The email report always states whether an error occurred, so a failure is never silent.
- **The failure scenario is a genuine test of error handling, not a scripted pass.** The application was actually taken offline through IIS, and the test's failure is a real, correctly detected result, not a simulated message.
- **The specific error is captured and reported**, naming exactly which UI element could not be found, which gives a clear starting point for troubleshooting rather than a vague failure.
- **Every execution is tracked in UiPath Orchestrator**, providing a central, auditable record of test runs beyond just the local email inbox.
- **Every code change is committed and pushed to GitHub**, confirmed live on the remote repository, giving the automation project the same traceable, professional change history as any properly maintained codebase.

## 6. Business Value

- **Confidence after every change.** Login can be re-verified automatically any time the CRM is updated.
- **Trustworthy failure detection.** A team can rely on the test to correctly flag a real problem rather than silently passing when something is actually broken.
- **Fast, clear reporting.** Automated email reports mean the team knows the result of a test run within moments, without needing to check the automation tool.
- **Centralized visibility.** Orchestrator gives a shared, trackable history of every run, useful for both day-to-day monitoring and later review.
- **Clear accountability and history.** GitHub tracks every change to the test suite itself, with 17 commits and counting on the main branch at the time of the demo, giving the project the same auditable trail a professionally maintained codebase would have.

## 7. Skills Demonstrated

- Designing automated UI test cases with UiPath Test Suite.
- Structuring reusable, maintainable automation using a shared login workflow and an Object Repository.
- Deliberately testing failure scenarios to validate an automation's error handling, not just its happy path.
- Configuring automated email reporting tied to test outcomes.
- Using IIS Manager to control a web application's availability for test purposes.
- Monitoring and reviewing automated test execution through UiPath Orchestrator.
- Managing an automation project with Git and GitHub, including committing and pushing changes directly from the development environment and verifying them on the remote repository.

## 8. Enterprise Use Cases

- **Regression testing**, automatically re-checking core application flows after every release.
- **Resilience and failure-mode testing**, confirming an automation correctly detects and reports outages or unavailable systems.
- **Release readiness checks**, running critical tests before a deployment goes live.
- **Continuous testing in CI/CD pipelines**, running these kinds of checks automatically as part of a software delivery process.
- **Automation project governance**, maintaining test automation under the same version control discipline as any other software project.
- **Any automated test suite** where knowing that a failure will be caught and reported is as important as confirming the happy path works.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- A test suite is only as trustworthy as its failure handling. Proving that a test correctly catches a real outage is just as important as proving it passes under normal conditions.
- Deliberately inducing a failure, rather than only testing the ideal case, is what actually validates an automation's error handling in practice.
- Automated email reporting closes the loop. A test that runs but does not clearly report its result to someone does not save real time.
- Centralizing execution in Orchestrator, rather than relying on local runs and inbox checks alone, makes test results visible and auditable across a team.
- Treating a test automation project like real software, with source control, commit history, and a clear project structure, pays off as the suite grows.

**Future enhancements:**
- Add automatic retries for transient failures, distinguishing them from genuine, persistent outages.
- Extend the same deliberate failure-testing approach to the other test cases in the suite, such as invalid login and logout.
- Add a dashboard summarizing pass and fail trends over time, not just individual email reports.
- Integrate alerts into a team chat tool, such as Slack or Teams, alongside email.
- Schedule the test suite to run automatically at set intervals through Orchestrator, rather than only on demand.
- Adopt branching and pull request reviews for future changes, rather than committing directly to the main branch.
