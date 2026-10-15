# ServiceNow REST API Integration: Automated Attachment Upload

**Automation Playground Portfolio Project**

A Power Automate Desktop flow that uploads a file as an attachment to a ServiceNow incident record by calling ServiceNow's Attachment REST API directly, without opening the ServiceNow user interface to do it.

## 1. Project Overview

This project automates the attachment of a file to a ServiceNow incident (INC0008111) using ServiceNow's Attachment API. The video first shows the API being tested manually through ServiceNow's built in REST API Explorer, confirming the correct endpoint, parameters, and headers needed to upload a file. It then shows a Power Automate Desktop flow, named "ServiceNow Upload Attachment," that calls the same endpoint programmatically through an Invoke Web Service action, uploading a local file and receiving a successful response from ServiceNow in return.

## 2. Business Problem & Objectives

**The problem:** Attaching supporting files to a ServiceNow record, such as a log file, a test report, or supporting documentation, is normally a manual task: someone opens the record, finds the attachment option, browses for the file, and uploads it. When this needs to happen repeatedly, for example whenever a related process generates a new log or output file, manual attachment does not scale and is easy to forget or delay.

**The objectives:**
- Confirm ServiceNow's Attachment API accepts an uploaded file against a specific table and record, using the correct parameters and authentication.
- Build an automated flow that uploads a file to a ServiceNow incident without any manual interaction with the ServiceNow interface.
- Verify that an automated upload produces the same result, a visible attachment on the incident record, as a manual one.

## 3. Solution

The solution uses ServiceNow's REST Attachment API (`/api/now/attachment/file`) as the integration point. A POST request to this endpoint, with the target table name, the record's `sys_id`, and the desired file name passed as query parameters, uploads a file and attaches it to that record. The API call requires a `multipart/form-data` content type and an authenticated user token.

### What the Video Demonstrates

The video opens in ServiceNow's REST API Explorer, showing the Attachment API's documentation and its "Upload an attachment from a binary request" operation. The request is configured with `table_name=incident`, `table_sys_id=a83820b58f723300e7e16c7827bdeed2`, and a `file_name` value, then a file is attached to the request body and sent. The response returns a 201 Created status with the uploaded file's metadata in the body. The incident record (INC0008111) is then opened directly to confirm the attachment appears under its "Manage Attachments" list, along with a timestamped activity log entry showing the upload.

The video then switches to Power Automate Desktop, where a flow called "ServiceNow Upload Attachment" is shown open in the editor. This flow uses an "Invoke Web Service" action configured with the same endpoint URL, the same `table_name` and `table_sys_id` parameters, a POST method, and the attachment upload option enabled with a local file (`ServiceNow Upload Test Log.txt`) selected as the attachment. The flow is run, and the action's output shows a `StatusCode` of 201, along with the raw web service response. The incident record is then refreshed in the browser, showing the new attachment ("ServiceNow Upload Test Log.txt," 644 bytes) now listed alongside the earlier manual uploads, with a matching activity log entry timestamped at the moment the flow ran.

### End-to-End Workflow, Step by Step

1. **Confirm the API manually.** The Attachment API's upload operation is tested in ServiceNow's REST API Explorer, setting the target table, record ID, and file name, then sending a file in the request.
2. **Verify the manual result.** The incident record is opened to confirm the test attachment appears in its attachment list and activity log.
3. **Configure the automated flow.** In Power Automate Desktop, an Invoke Web Service action is set up with the same endpoint, parameters, and POST method, with file upload enabled and a local file selected as the attachment.
4. **Run the flow.** The flow executes the web service call and returns a status code and response body confirming the outcome.
5. **Verify the automated result.** The incident record is refreshed to confirm the flow's uploaded file now appears in the attachment list, with its own timestamped activity log entry, matching the behavior of the manual test.

## 4. Solution Architecture & Technologies

- **ServiceNow REST API Explorer**, used to inspect and manually test the Attachment API before automating it.
- **ServiceNow Attachment API** (`/api/now/attachment/file`), the integration point that accepts a file upload against a specified table and record.
- **ServiceNow Incident module**, the target record (INC0008111) that the attachment is uploaded to and verified against.
- **Microsoft Power Automate Desktop**, used to build and run the automated upload flow.
- **Invoke Web Service action**, configured with the endpoint URL, query parameters, POST method, multipart file upload, and an authenticated user token, used to call the API without a browser.

Testing the API manually first, before automating it, is what makes this a reliable integration rather than a guess at how the endpoint behaves. The manual pass in the REST API Explorer confirms the exact parameters, headers, and response shape needed, and that same configuration is then carried directly into the Invoke Web Service action. Verifying the result in the incident record after each run, manual and automated, confirms the integration actually produces the expected outcome in ServiceNow rather than just a successful looking API response.
