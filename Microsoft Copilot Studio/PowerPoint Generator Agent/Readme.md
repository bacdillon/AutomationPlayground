# PowerPoint Generator Agent

An AI agent, built on Microsoft Copilot Studio, that generates PowerPoint documents, certificates, reports, and proposals, from a simple chat request. Ask it in plain language, or hand it a spreadsheet of names, and it produces a properly formatted PowerPoint file for each one, ready to download, with no manual copy-pasting into a template required.

## 1. Project Overview

This project is a working AI agent that turns a natural-language request into a finished PowerPoint document. In the demonstration, it's used to generate certificates of completion. The user simply describes who the certificate is for, and the agent fills in a template, saves the finished file, and hands back a download link. It also handles bulk generation: given a spreadsheet listing multiple people, it produces an individual, correctly personalized PowerPoint file for every row, automatically.

## 2. Business Problem & Objectives

**The problem:** Many businesses regularly need to produce personalized documents from a template, training certificates, client proposals, status reports, where the layout stays the same but the details change each time, a name, a course, a date, a set of figures. Doing this by hand means opening a template, manually typing in the right details, saving it under the right name, and repeating that for every person or every report. It's simple work, but it adds up quickly when there are many to produce. Repetitive manual editing, copying a template and retyping the same few fields over and over, is one recurring friction. So is the risk of small mistakes, since a misspelled name or wrong course title is an easy slip when doing this manually at volume. There's no simple way to batch-produce documents either. Generating one certificate is easy enough by hand; generating fifty at once, correctly and consistently, is not. Document generation is also disconnected from where the request originates, since someone has to translate "please create a certificate for these five people" into actual file-by-file work themselves.

**The objectives:**
- Let a user request a finished PowerPoint document simply by describing what they need in plain language.
- Automatically fill a PowerPoint template with the correct, specific details for each request.
- Save the finished file to a shared, accessible location and return a usable link.
- Support bulk generation from a spreadsheet, producing one correctly personalized file per row.
- Remove manual document editing from a repetitive, template-based task entirely.

## 3. Solution

The "PowerPoint Generator Agent," built in Microsoft Copilot Studio, is described as an automated document generation Copilot agent that creates PowerPoint presentations such as certificates, reports, and proposals, using templates and structured data. Its core capability is a single, reusable tool, "Generate New Certificate," that takes three pieces of information, student name, course name, instructor name, and produces one finished PowerPoint file.

### What the Video Demonstrates

For single document generation, the user types a natural-language request, "Create a new certificate for Nellie Nam's successful completion of AB-730 Microsoft 365 for Business Users instructed by Dr. Julien Bashir." The agent runs its "Generate New Certificate" tool, correctly extracting the student name, course name, and instructor name from the sentence, generates the certificate, and replies with a summary and a working download link. The resulting PowerPoint file is opened directly to confirm the certificate was generated correctly, with the right name merged into the template. For bulk document generation, the user asks the agent to "create a new certificate for the students" and uploads a spreadsheet, "Students.xlsx," listing multiple students for the same course and instructor. The agent reads the spreadsheet and automatically runs the certificate-generation tool once for each student listed, the video shows it processing Ethan Tan, Chloe Lim, Daniel Wong, Sophia Lee, and Ryan Koh, producing a separate, correctly personalized PowerPoint certificate for every person, each one verified afterward by opening the generated file.

### End-to-End Workflow, Step by Step

1. **Make a request.** The user describes what document they need in plain language, or uploads a spreadsheet listing multiple people who need the same type of document.
2. **The agent interprets the request.** It identifies the relevant details, such as student name, course, and instructor, either from the sentence itself or from each row of an uploaded spreadsheet.
3. **The document is generated.** For each request, or each row in a bulk scenario, the agent runs a dedicated generation tool that merges the specific details into a PowerPoint template.
4. **The file is saved.** The completed PowerPoint file is saved to a shared location (SharePoint), rather than staying local to the conversation.
5. **A link is returned.** The agent responds with a summary of what was generated and a direct download link for each file.
6. **The user retrieves the result.** The finished PowerPoint document can be downloaded and opened immediately, fully personalized and ready to use.

## 4. Solution Architecture & Technologies

- **Microsoft Copilot Studio**, the platform used to build and run the AI agent.
- **Microsoft PowerPoint**, the format of the generated documents, and used to verify the output.
- **SharePoint and OneDrive**, where generated files are saved and made available for download.
- **Microsoft Excel**, the format used for bulk input, a spreadsheet listing multiple people or requests.
- **Claude Sonnet**, the large language model powering the agent's understanding of natural-language requests and its responses.
- **An agent flow (Power Automate)**, the underlying automation that retrieves the PowerPoint template, merges in the provided data via a prompt action, saves the result to SharePoint, and returns the file path.
- **Structured data extraction**, pulling specific fields (name, course, instructor) out of both natural-language sentences and spreadsheet rows.

For a single request, the agent extracts the three required details directly from the user's sentence and calls the generation tool once. For a bulk request, the agent instead reads an uploaded spreadsheet and calls the exact same tool once per row, reusing the same template-filling logic without needing any different setup. This means the underlying generation logic doesn't need to know or care whether it's handling one request or fifty. That distinction is handled entirely by how the agent chooses to call the tool. Its AI capabilities include natural language understanding, correctly extracting specific structured fields from a single, ordinary sentence, document understanding for bulk input, correctly identifying each spreadsheet row as a separate request, tool orchestration, knowing when and how to invoke its document-generation tool, and clear, grounded responses that restate the specific details used and provide a direct, working link to the actual generated file.
