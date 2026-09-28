# Customer Message Triage with a Local LLM

An automation that reads an incoming customer message and instantly analyzes it using a locally hosted AI model, identifying the customer's sentiment, what they actually want, how urgent it is, and even drafting a suggested reply, all without sending any customer data to an external cloud AI service.

## 1. Project Overview

This project automates the first, most time-consuming part of handling customer messages: figuring out what a message is really about and how urgently it needs attention. A Power Automate Desktop flow sends an incoming customer message to a locally running AI model, Llama 3.2, served through Ollama, which analyzes it and returns a structured breakdown of sentiment, intent, urgency, and a ready-to-use draft reply, all in a matter of seconds.

## 2. Business Problem & Objectives

**The problem:** Customer support teams receive a constant stream of messages that vary widely in tone and urgency, from a simple question to a glowing compliment to an urgent complaint about a delayed order. Before a message can be properly handled, someone has to read it, judge how serious it is, and decide what kind of response is needed. Doing this consistently, especially at volume, takes real time and attention. Urgent messages can get buried if nothing distinguishes them from routine ones, and judging tone and urgency is inherently subjective, varying from person to person and hour to hour. Drafting a first response from scratch for every message also takes time, even when the right tone and approach are fairly predictable. On top of all this, sending customer messages to a cloud AI service may not be acceptable for organizations with strict data privacy requirements.

**The objectives:**
- Automatically analyze incoming customer messages for sentiment, intent, and urgency.
- Generate a short, appropriate draft reply automatically, saving time on first-response drafting.
- Perform this analysis using a locally hosted AI model, keeping customer data on premises.
- Present the results clearly and immediately, ready for a person to review and act on.
- Handle potential AI service issues, such as connection problems, gracefully.

## 3. Solution

A Power Automate Desktop flow, "Customer Message Triage (Local LLM)," uses Power Automate's built-in "Invoke Local LLM" action to connect to a locally hosted AI model, Llama 3.2, served through Ollama at `http://localhost:11434/v1`. No cloud AI service is involved at any point. A system prompt instructs the model to act as a customer support triage assistant that analyzes incoming messages concisely and always follows the exact requested output format. A user prompt feeds in the actual customer message and asks the model to respond in a precise, structured format covering sentiment, intent, urgency, and a suggested reply.

### What the Video Demonstrates

Running the flow against a real customer complaint about a delayed order, the model correctly identifies the message as Sentiment: Negative, Intent: Complaint, Urgency: High, and drafts a suggested reply acknowledging the frustration, referencing the customer's upcoming weekend trip, and confirming the team is looking into it immediately. The result is displayed to the user in a popup notification, ready for immediate review. The action itself is shown configured with error handling and retry settings, including a fixed retry policy of 2 to 5 attempts at 3-second intervals, covering specific failure scenarios such as connection errors, the model not being found, request timeouts, and invalid responses.

### End-to-End Workflow, Step by Step

1. **Receive the customer message.** The message text is made available to the flow as a variable.
2. **Send it to the local AI model.** The flow calls the locally hosted Llama 3.2 model, combining the customer message with a structured analysis prompt.
3. **Analyze the message.** The model determines the sentiment, intent, and urgency, and drafts a suggested reply.
4. **Handle any issues.** If the AI call fails, due to a connection issue, timeout, or similar, the flow's configured retry policy attempts the call again before giving up.
5. **Display the results.** The structured analysis and suggested reply are shown to the user in a clear notification popup.
6. **The user reviews and acts.** A person can use the analysis to prioritize the message and quickly adapt the suggested reply before sending it.

## 4. Solution Architecture & Technologies

- **Ollama**, hosting the local AI model that performs the analysis.
- **Power Automate Desktop**, running the automation and displaying results.
- **Power Automate Desktop's "Invoke Local LLM" action**, a built-in feature for connecting directly to a locally hosted AI model.
- **Llama 3.2**, the open-source AI model used for the analysis, served locally via Ollama.
- **Structured prompting**, using a system prompt and a precisely formatted user prompt to get consistent, structured output.
- **Built-in retry and error handling configuration**, for managing AI service reliability issues.

The flow relies on precise prompting to get consistent, structured results from the AI model. The system prompt establishes the model's role and instructs it to strictly follow the requested format, while the user prompt spells out exactly what fields are needed, and in what order. Because the output format is so tightly specified, the result can be reliably read and displayed without needing complex parsing.
