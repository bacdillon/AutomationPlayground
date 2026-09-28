# Intelligent IT Helpdesk Support (AI Agent)

A conversational AI agent, built on Microsoft Copilot Studio, that lets employees check the status of their IT helpdesk tickets and get answers to IT and HR policy questions, simply by chatting naturally, in their own language, with no forms, ticket numbers to hunt for, or portal navigation required.

## 1. Project Overview

This project is a working AI-powered helpdesk assistant. Employees can ask it, in plain language, about the status of an IT support ticket, company IT or HR policies, or general IT issues, and it responds conversationally, pulling live ticket details from ServiceNow when needed. It automatically detects and responds in whatever language the user writes in, remembers context across a conversation so a user doesn't have to repeat themselves, and is built with usage analytics baked in from day one.

## 2. Business Problem & Objectives

**The problem:** Every organization with an IT helpdesk deals with a steady stream of simple, repetitive questions: "What's the status of my ticket?", "What department am I in?", "What's our policy on X?" These questions don't need a human's judgment. They need fast access to information that already exists in systems like ServiceNow or a company knowledge base. Handling them through a live chat agent frees up IT staff for the issues that actually require a person, while giving employees a faster answer than waiting in a support queue. Simple status checks consume real staff time, even though the answer is just a lookup away. Employees often don't know their own ticket number or how to navigate a ticketing portal, creating friction before they even get an answer. Support is typically limited to one language, which can slow things down or exclude non-native speakers in a global organization, and basic policy questions get repeated constantly, taking time away from genuinely complex support issues.

**The objectives:**
- Let employees check their IT ticket status through natural conversation, not a portal.
- Automatically detect and respond in the user's own language.
- Pull live, accurate ticket data directly from ServiceNow rather than static or outdated information.
- Answer common IT and HR policy questions using the organization's own knowledge base.
- Maintain context across a conversation, so users can ask natural follow-up questions.
- Track the agent's usage and performance through built-in analytics.

## 3. Solution

An AI agent called "Intelligent IT Helpdesk Support," built in Microsoft Copilot Studio, greets employees and asks for their registered email address to identify them before sharing any personalized information. From there, the agent uses a large language model to understand what the user is asking, decide what information it needs, and choose the right action, querying ServiceNow, consulting the knowledge base, or asking a clarifying question.

### What the Video Demonstrates

The agent confirms the identified user by name, "Thanks for that, David Miller," then demonstrates automatic language detection: the user switches to writing in German partway through the conversation, and the agent seamlessly continues the entire rest of the conversation in German, with no manual language setting required. When the user asks about their ticket status, the agent asks for the specific ServiceNow incident number, in the correct `INC` plus seven-digit format, before looking it up, then retrieves and clearly presents live ticket details from ServiceNow, status, priority, the dates the ticket was opened and last updated, and the original issue description. A natural follow-up question, "What category does this ticket belong to?", is answered correctly without the user needing to repeat the ticket number, showing the agent retains context from earlier in the conversation. A completely different type of question, "What department am I in, according to my user profile?", is answered correctly too, showing the agent can also draw on user profile and HR information, not just ticket data. A built-in Analytics panel tracks conversation sessions, engagement, and satisfaction score for the agent.

### End-to-End Workflow, Step by Step

1. **Start the conversation.** The user opens a chat with the agent, which introduces itself and explains what it can help with.
2. **Identify the user.** The agent asks for the user's registered email address and confirms their identity.
3. **Understand the request.** The user asks a question in natural language, for example about a ticket status, a policy, or their own profile information.
4. **Retrieve the needed information.** For ticket-related questions, the agent requests the relevant ticket number and looks it up directly in ServiceNow. For policy or profile questions, it draws on connected knowledge sources.
5. **Respond clearly.** The agent presents the answer in plain, readable language, not raw system data.
6. **Handle follow-up questions.** If the user asks something related to the same topic, like a ticket's category, the agent uses the context already established, without asking the user to repeat information.
7. **Continue in the user's language.** Throughout, the agent responds in whatever language the user is writing in, switching automatically if the user changes language mid-conversation.

## 4. Solution Architecture & Technologies

- **Microsoft Copilot Studio**, the platform used to build, test, and publish the AI agent.
- **ServiceNow**, the IT service management platform the agent queries for live ticket data.
- **A connected knowledge base**, supplying information on company IT and HR policies.
- **A large language model (GPT-4.1)**, powering the agent's natural language understanding and response generation.
- **Tool and API integration with ServiceNow**, for retrieving live incident (ticket) data.
- **Knowledge grounding**, connecting the agent to company policy and HR documentation.
- **Automatic language detection**, enabling multilingual conversations without manual configuration.
- **Built-in analytics**, tracking conversation sessions, engagement, and satisfaction.

Rather than following a rigid, scripted decision tree, the agent uses a large language model to understand what the user is actually asking and choose the right action. Context from earlier in the conversation is retained, so a follow-up question naturally connects back to what was already discussed, rather than treating every message as a fresh, disconnected request. This is what allows the agent to feel like a genuine conversation rather than a form-filling exercise. Its AI capabilities include natural language understanding across multiple languages, automatic language detection and response, contextual memory, grounded tool-based responses that pull real, current data rather than guessing, and built-in evaluation and analytics providing direct visibility into how the agent is performing.
