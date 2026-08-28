# Customer Message Triage (Local LLM)

## 1. Project Overview

**Customer Message Triage (Local LLM)** is a low-code RPA automation built in **Microsoft Power Automate Desktop** that reads an incoming customer message and uses a **locally hosted Large Language Model (LLM)** to automatically classify and respond to it. In a single automated step, the flow determines the customer's **sentiment**, **intent**, **urgency level**, and generates a **ready to use draft reply**, without sending any customer data to an external cloud AI service.

The flow calls a local LLM server (Ollama, model `llama3.2:latest`) running on `http://localhost:11434`, the entire happens **on premises**, making it ideal for organizations with strict data privacy or compliance requirements.

## 2. Business Context

Customer support teams, whether in retail, e-commerce, SaaS, banking, or telecom, receive a constant stream of messages through email, chat, web forms, and social media. Before an agent can respond effectively, someone (or something) needs to:

- Read the message
- Judge how the customer feels
- Understand what they actually want
- Decide how urgently it needs a response
- Draft a suitable reply

Doing this manually for every incoming message is slow and inconsistent, especially during high volume periods. This project demonstrates how RPA and a local AI model can automate that first triage step, giving agents an instant head start.

## 3. Business Problem

- Support agents spend significant time simply **reading and categorizing** messages before they can act on them.
- Urgent or negative messages (e.g., complaints, refund requests) are sometimes **not prioritized fast enough**, risking customer churn.
- Manual triage is **inconsistent**, different agents may judge tone, urgency, or intent differently.
- Many businesses cannot send customer data to third party cloud AI APIs due to **privacy, security, or compliance** policies (GDPR, internal data governance, etc.).
- Drafting a first response from scratch for every message is **repetitive and time-consuming**.

## 4. Project Objectives

- Automatically **analyze the sentiment, intent, and urgency** of any incoming customer message.
- Automatically **generate a short, empathetic draft reply** an agent can review and send.
- Keep all data processing **local and private** by using a self-hosted LLM instead of a cloud AI API.
- Build the entire solution using **low-code RPA tooling** (Power Automate Desktop) rather than custom-coded software.
- Demonstrate a **reusable, structured output pattern** so the AI's response can be parsed reliably by downstream steps (e.g., routing tickets, updating a CRM).
- Include **built-in error handling and retry logic** so the automation is resilient to LLM downtime or bad responses.

## 5. What the Video Demonstrates

The demonstration video walks through a working Power Automate Desktop flow called **"Customer Message Triage (Local LLM)"**. It shows:

- The two core steps of the flow: **Invoke Local LLM** and **Display message**.
- The full configuration of the **Invoke Local LLM** action, including the server URL, model name, user prompt template, and advanced settings (system prompt, temperature, token limits, timeout).
- The **error-handling and retry configuration** attached to the LLM call.
- A **live run** of the flow, showing the automation calling the local model, receiving a structured response, and displaying it in a pop-up window.
- The final AI-generated output: a sentiment/intent/urgency classification plus a drafted customer reply.

## 6. End-to-End Workflow Explained Step-by-Step

1. **Flow trigger / input**. The flow accepts a customer message as an **input parameter** (visible as `Input: 1` in the Variables pane), allowing it to be triggered manually, from a parent flow, or from another system (e.g., an inbox-monitoring flow) that passes in the raw message text.
2. **Prompt construction**. The flow inserts the customer's message into a pre-built prompt template using the `%customer_message%` placeholder.
3. **Invoke Local LLM**. The flow sends the constructed prompt to a local LLM server (Ollama) running the `llama3.2:latest` model, along with a system prompt that instructs the model to act as a "customer support triage assistant."
4. **Structured response generation**. The model returns a response formatted in four required fields: Sentiment, Intent, Urgency, and Suggested reply.
5. **Token/telemetry capture**. The flow captures `PromptTokens` and `CompletionTokens` as flow variables for monitoring model usage and performance.
6. **Display result**. The flow shows the model's full response in a pop-up notification window titled **"Reply: Customer Message Triage (Local LLM)"**, so the operator can review the classification and draft reply immediately.
7. **User acknowledgment**. The operator clicks **OK** (or **Cancel**), and the button choice is captured in the `ButtonPressed2` variable, which could be used to drive further logic (e.g., auto-send the reply vs. escalate for manual editing).

## 7. Systems and Applications Involved

| System | Role |
|---|---|
| **Power Automate Desktop** | RPA orchestration engine that builds and runs the automation |
| **Ollama (local LLM server)** | Hosts and serves the `llama3.2:latest` model via an OpenAI-compatible local API (`http://localhost:11434/v1`) |
| **Windows Desktop notification popups** | Used to display the AI-generated triage result to the operator |

## 8. Technologies Used

- **Microsoft Power Automate Desktop** (RPA / low-code automation platform)
- **Ollama** — local LLM inference server
- **Meta Llama 3.2** (`llama3.2:latest`), open-source large language model, run entirely offline
- **OpenAI-compatible REST API** (`/v1` endpoint), the protocol used to communicate between Power Automate and the local model
- **Prompt engineering**, a structured system + user prompt design to force consistent, parsable output

## 9. AI Capabilities

This project showcases several practical generative AI capabilities, run entirely locally:

- **Sentiment analysis**, classifies the message as Positive, Negative, or Neutral.
- **Intent classification**, categorizes the message as a Complaint, Question, Praise, Refund Request, or Other.
- **Urgency scoring**, flags the message as Low, Medium, or High priority.
- **Automated draft reply generation**, produces a short, empathetic, human-like response tailored to the specific message.
- **Configurable model behavior**, temperature, system prompt, and max tokens are all exposed as adjustable parameters, letting the developer tune creativity vs. consistency.
- **On-device inference**, no data leaves the local machine/network, since the model runs through Ollama rather than a cloud API.

## 10. User Interactions

- The operator (or a triggering system) provides the raw customer message as flow input.
- The operator **runs the flow** (manually, in this demo) and watches it execute step by step in the Power Automate Desktop designer.
- Once complete, a **pop-up notification** displays the analysis and the drafted reply.
- The operator reviews the output and clicks **OK** to acknowledge (or **Cancel**), with that choice captured for potential future branching logic (e.g., "OK = send reply", "Cancel = escalate to human agent").

## 11. Inputs and Outputs

**Input:**
- A single text string containing the raw customer message (e.g., a complaint about a delayed order).

**Outputs (Response variable, structured text):**
- `Sentiment` e.g., Negative
- `Intent` e.g., Complaint
- `Urgency` e.g., High
- `Suggested reply` a 2–3 sentence draft response

**Additional flow variables produced:**
- `PromptTokens`, number of tokens sent to the model (194 in the demo run)
- `CompletionTokens`, number of tokens generated by the model (67–72 in the demo runs)
- `ButtonPressed2`, captures which button the operator clicked on the results popup

## 12. Error Handling and Validation

The **Invoke Local LLM** action includes a dedicated error-handling configuration to make the automation resilient to failure conditions:

- **Retry policy:** Fixed retry strategy, retries the call **2 times** with a **3-second interval** between attempts before failing.
- **Handled error conditions:**
  - **Connection error**, the local LLM server is unreachable (e.g., Ollama isn't running).
  - **Model not found**, the specified model isn't installed/loaded on the server.
  - **Request timed out**, the model takes too long to respond (a 300-second timeout is configured).
  - **Invalid response**, the model output doesn't come back in a usable format.

This layered approach (timeout + retries + specific error branches) ensures the flow can recover from transient issues (like a slow first model load) instead of failing outright, and gives developers a clear place to add fallback logic (e.g., notify IT, log the failure, or route the message for manual handling).

## 13. Business Rules

- Every customer message must be run through the **exact same prompt template**, ensuring consistent evaluation criteria across all messages.
- The model's response must strictly follow the **four-field format** (Sentiment / Intent / Urgency / Suggested reply) so that it can be reliably parsed by later steps.
- The **system prompt** enforces the assistant's role and tone ("customer support triage assistant… respond concisely… follow the exact output format").
- **Temperature is set to 0.8**, allowing some natural variation in the drafted reply while the classification fields remain structured and predictable.
- A **maximum of 2048 tokens** and a **300-second timeout** cap how much the model can generate and how long the flow will wait, keeping runtime and cost/resource usage predictable.

## 14. Key Features

- Calling a **local, self-hosted LLM** directly from a no-code/low-code RPA tool.
- Using **prompt engineering** to force structured, parsable output from a generative model.
- Exposing and adjusting **advanced model parameters** (system prompt, temperature, max tokens, timeout, response format) inside a visual designer.
- Capturing **usage telemetry** (prompt/completion tokens) as native flow variables.
- Implementing **enterprise-grade error handling** (retry policy + specific failure-type handling) around an AI service call.
- Presenting AI output to a human operator through a simple, native **desktop notification**.

## 15. Business Value and Benefits

- **Faster first response:** Messages are classified and drafted in seconds rather than minutes.
- **Consistent triage quality:** Every message is judged against the same criteria, reducing agent-to-agent variability.
- **Improved prioritization:** High-urgency complaints are immediately flagged, so they can be escalated before they affect customer satisfaction.
- **Data privacy by design:** Because the LLM runs locally, no customer message content is transmitted to a third-party AI provider — a major advantage for regulated industries.
- **Lower AI operating cost:** Using an open-source local model avoids per-call API fees associated with commercial cloud LLMs.
- **Scalable foundation:** The same pattern can be extended to auto-tag tickets, populate a CRM, or route messages to the right team automatically.

## 16. Productivity Improvements

- Removes the manual step of an agent reading and categorizing every message before responding.
- Provides a **ready-made draft reply**, cutting down the time an agent spends composing a first response from scratch.
- Frees up human agents to focus on **judgment-based work** (handling exceptions, sensitive cases, and complex resolutions) rather than repetitive triage.
- Enables **24/7 initial triage**, since the automation doesn't require an available human agent to begin analyzing incoming messages.

## 17. Real-World Enterprise Use Cases

- **Customer support inbox triage**, auto-classify and draft replies for emails, web-form submissions, or live chat transcripts before they reach an agent's queue.
- **Social media / review monitoring**, flag negative or urgent brand mentions for immediate attention.
- **Helpdesk / IT ticketing**, automatically tag incoming tickets with urgency and category to support smarter routing and SLAs.
- **Regulated industries (finance, healthcare, government)**, apply generative AI to sensitive communications without sending data to external cloud services.
- **Multichannel customer engagement platforms**, standardize how messages from different channels (email, chat, forms) are triaged before being merged into a single agent workspace.

## 18. Lessons Learned

- **Prompt design directly determines automation reliability.** Requiring an exact output format (four labeled fields) made it possible to treat a generative AI response like structured data inside an RPA flow.
- **Local LLMs are a viable option for RPA-integrated AI features**, especially where data privacy is a priority, though they require the additional step of hosting/maintaining the model server (Ollama) locally.
- **Error handling is essential** when calling any external or local AI service, model servers can be slow to respond (especially on first load) or unavailable, so retry logic and timeouts are not optional extras but core requirements.
- **Temperature and token limits matter**, tuning these settings balances response creativity against consistency and keeps runtime/costs predictable.

## 19. Possible Future Enhancements

- **Parse the structured Response variable** into separate fields (Sentiment, Intent, Urgency, Suggested reply) using text-parsing actions, so each value can be used independently (e.g., stored in a spreadsheet or CRM field).
- **Auto-route messages** based on urgency and intent (e.g., send High-urgency Complaints directly to a supervisor's queue).
- **Connect to a live inbox** (Outlook, Teams, or a support ticketing system) to trigger the flow automatically on new incoming messages, instead of running it manually.
- **Log every triage result** to Excel, SharePoint, or a database for reporting and quality auditing.
- **Add human-in-the-loop approval** before automatically sending the AI-drafted reply to the customer.
- **A/B test model parameters** (temperature, prompt wording) to improve reply quality and classification accuracy over time.
- **Support multiple languages** by adjusting the prompt to detect and respond in the customer's original language.
