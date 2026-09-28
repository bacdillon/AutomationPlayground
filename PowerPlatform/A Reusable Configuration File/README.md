# A Reusable Configuration File

A Power Automate Desktop configuration file holds configuration data used by a desktop flow. It allows settings to be stored separately from the automation logic itself. Configuration data remains constant throughout all flow runs, and if it becomes necessary to update the configuration, it can be done without changing the automation itself.

## 1. Project Overview

This project demonstrates how to build automations that are easy to maintain, move between environments, and hand off to someone else, by separating an automation's settings from its logic. Instead of folder paths and an email address being typed directly into the automation's steps, they are stored in an external Excel file that the automation reads at the start of every run, through one shared, reusable subflow. The pattern is proven out using a working example: an automation that sorts a folder of mixed files into the correct subfolders, using settings pulled entirely from configuration rather than hardcoded values.

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
