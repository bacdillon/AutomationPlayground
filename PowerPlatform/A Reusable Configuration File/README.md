# A Reusable Configuration File

A Power Automate Desktop configuration file holds configuration data used by a desktop flow. It allows settings to be stored separately from the automation logic itself. Configuration data remains constant throughout all flow runs, and if it becomes necessary to update the configuration, it can be done without changing the automation itself.

## 1. Project Overview

This project demonstrates how to build automation that are easy to maintain, move between environments, and hand off to someone else, by separating an automation's settings from its logic. Instead of folder paths and an email address being typed directly into the automation's steps, they are stored in an external Excel file that the automation reads at the start of every run, through one shared, reusable subflow. The pattern is proven out using a working example: an automation that sorts a folder of mixed files into the correct subfolders, using settings pulled entirely from configuration rather than hardcoded values.

## 2. Business Problem & Objectives

**The problem:** As automations move from a quick personal script to something a team relies on, a common problem emerges: settings like file paths, email addresses, or system URLs end up scattered directly inside each automation's steps. This works fine for a single automation running on one machine, but breaks down the moment there is more than one automation to maintain, or the same automation needs to run in a different environment, such as a test setup versus a live one. Moving an automation to a new environment then requires editing its internal logic, which is risky and easy to get wrong, and switching between a test setup and a live setup often means manually changing values buried inside the automation itself.

**The objectives:**
- Separate an automation's configurable settings from its core logic.
- Store configuration in a format that is easy to view and edit without touching the automation itself.
- Support switching between different environments, such as Development and Production, without modifying the automation's steps.
- Demonstrate the pattern with a concrete, working example: automatically organizing files by type.
- Provide a clear, reusable template for setting up configuration in future automations.

## 3. Solution

A Config folder contains an Excel file (`config.xlsx`) storing all of the automation's settings as simple key-value pairs: a project path, separate folder paths for documents, text files, and pictures, and an email address for notifications. The file has two tabs, "Production" and "Development," allowing the same automation to run against different settings depending on which environment is selected. A separate template file (`template.xlsx`) is included, providing a ready-made starting point for setting up configuration in a new automation project. The main flow sets which environment to use, then runs a dedicated "Config" subflow that reads the appropriate settings from the Excel file and returns them as a single, structured object the rest of the flow can reference.

### What the Video Demonstrates

Using the loaded configuration settings, the flow retrieves every file in the configured project folder and its subfolders, then loops through each one, checking its file extension and moving it into the correct destination folder: images into the Pictures folder, presentations into the Documents folder, and text files into the Text folder, all using paths pulled from the configuration, not hardcoded. Once every file has been sorted, the flow launches Outlook and sends a confirmation email, using the recipient address from the same configuration file, with the subject "File cleanup done" and a message confirming the folder has been cleaned up. The result is confirmed directly in the video: a "Files" project folder starting with unsorted documents, images, and text files (using famous paintings as example content, such as "Mona Lisa," "The Birth of Venus," and "Girl with a Pearl Earring") ends up correctly organized into `Development\Documents`, `Development\Pictures`, and `Development\Text` subfolders, with the confirmation email arriving in the inbox shortly after.

### End-to-End Workflow, Step by Step

1. **Set the target environment.** The flow specifies which configuration set to use, for example "Development."
2. **Load the configuration.** A dedicated subflow reads the corresponding settings from the external Excel configuration file.
3. **Retrieve the files to process.** Using the configured project path, the flow collects every file in that folder and its subfolders.
4. **Sort each file by type.** For every file, its extension determines which configured destination folder it belongs in.
5. **Move the file.** The file is moved into the correct folder, using a path read from configuration rather than typed directly into the automation.
6. **Repeat for every file.** This continues until all files have been sorted.
7. **Notify on completion.** The flow sends a confirmation email, again using a recipient address pulled from configuration, confirming the task is complete.

## 4. Solution Architecture & Technologies

- **Power Automate Desktop**, for building the main flow and the reusable configuration subflow.
- **Excel read activities**, for loading configuration values at runtime.
- **A dedicated, reusable subflow**, for centralizing configuration-loading logic in one place.
- **Switch/case logic**, for routing files to the correct folder based on file type.
- **File system move operations**, for organizing files into their destination folders.
- **Outlook automation**, for sending the completion notification.

The core idea is a clean separation between what the automation does and where or for whom it does it. The main flow's logic, read files, check their type, move them, notify someone, never changes. What changes is only the configuration, folder paths and an email address, both stored externally and loaded through a single, reusable subflow at the start of the run. Because the configuration file distinguishes between "Development" and "Production" settings, the exact same automation logic can be pointed at a safe test environment or the real, live environment simply by changing which environment is selected, with zero changes to the automation's actual steps.

## 5. Controls & Validation

- Centralizing configuration loading in a single, dedicated subflow means every part of the automation references the same, consistent settings, so there is no risk of one part of the flow using an outdated or mismatched path.
- Because file-type routing is handled through explicit switch/case logic, files that do not match a recognized type fall through to a defined default case, rather than causing an unhandled failure.
- Separating Development and Production settings reduces the risk of accidentally running a test automation against live, real-world folders or recipients.
- The video shows both the model configuration file being loaded correctly and its result being verified directly against the actual folder structure, confirming the settings were applied as intended, not just assumed to work.

## 6. Business Value

- **Easier maintenance.** Updating a folder path or recipient is a simple spreadsheet edit, not a change to the automation itself.
- **Safer environment switching.** Moving from testing to live operation is a configuration change, not a code change, reducing the risk of mistakes.
- **Faster onboarding for new automations.** The included template makes it quick to set up proper configuration for future projects from day one.
- **Better collaboration.** Non-technical stakeholders can review or update settings directly in Excel, without needing to open or understand the automation logic.
- **More resilient automations overall.** Centralizing configuration reduces the chance of inconsistent or forgotten hardcoded values scattered throughout a flow.

## 7. Skills Demonstrated

- Designing maintainable, configuration-driven automations.
- Structuring reusable subflows for shared logic, such as configuration loading.
- Managing environment-specific settings, including Development versus Production.
- Implementing file-type-based routing logic.
- Automating email notifications tied to configurable recipients.
- Applying software engineering best practices, such as separation of concerns and externalized configuration, within an RPA tool.

## 8. Enterprise Use Cases

This configuration pattern is broadly applicable to virtually any RPA or automation project, including:

- **Multi-environment deployments**, running the same automation safely across development, test, and production systems.
- **Multi-client or multi-site automations**, using different configuration sets for different customers or locations without duplicating logic.
- **Automations maintained by non-developers**, allowing settings updates without requiring changes to the underlying automation.
- **Automation governance and auditing**, having a single, reviewable file showing exactly what an automation is configured to do.
- **Any automation expected to scale or be reused**, where hardcoded values would otherwise become a growing maintenance burden.

## 9. Lessons Learned & Future Enhancements

**Lessons learned:**
- Separating configuration from logic is one of the simplest, highest-leverage practices in building maintainable automations. The effort to set it up is small compared to the problems it prevents later.
- A dedicated subflow for loading configuration keeps that logic in exactly one place, so there is never a risk of different parts of an automation reading settings inconsistently.
- Supporting multiple environments, such as Development and Production, from the start makes it far safer to test changes without risking live systems or data.
- Providing a reusable template lowers the barrier to applying this pattern consistently across future automation projects, rather than it being a one-off effort.
- Even a simple demonstration task, sorting files by type, is enough to clearly show the value of a good architectural pattern. The complexity does not need to be in the example, just in the design principle.

**Future enhancements:**
- Add validation of the configuration file at startup, confirming all required settings are present before the automation proceeds.
- Support additional environments beyond Development and Production, such as a dedicated Testing or Staging tab.
- Extend the configuration file to support more complex settings, such as lists or nested values, not just simple key-value pairs.
- Add logging of which configuration and environment were used for each run, supporting easier troubleshooting and auditing.
- Build a simple validation or preview tool, letting someone check their configuration changes before running the automation live.
- Package the configuration-loading subflow as a standalone, shareable component for use across multiple automation projects.
