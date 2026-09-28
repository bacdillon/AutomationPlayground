# Holland America Deck Plans (AI Agent)

A conversational AI agent, built on Microsoft Copilot Studio, that answers detailed questions about Holland America cruise ship layouts, where things are, how to get between them, and whether a specific cabin meets a guest's needs, all grounded in the cruise line's actual deck plan documentation.

## 1. Project Overview

This project is a working AI assistant for cruise ship navigation and cabin selection. Rather than guests scrolling through static deck plan PDFs or maps, they can simply ask the agent a question, "Which deck is the casino on?", "How do I get from there to the sport court?", "Is cabin VC6154 wheelchair accessible?", and get a clear, accurate answer sourced directly from the ship's official deck plan documentation.

## 2. Business Problem & Objectives

**The problem:** Cruise ships are large, complex vessels with dozens of decks, hundreds of cabins, and a wide range of dining, entertainment, and recreation venues. Guests booking a cruise, or already onboard, often need quick answers about where things are, how to get between them, or whether a specific cabin suits their needs, location preference, accessibility, proximity to elevators, and so on. Traditionally, this means digging through a static deck plan PDF or asking staff directly. Static plans require manual interpretation, since a guest has to visually scan a deck-by-deck diagram to find a specific venue or work out how two locations relate to each other. Cabin-specific questions are hard to self-serve, since knowing whether a specific cabin number is accessible, quiet, or well-located isn't obvious from a deck map alone. Wayfinding between venues isn't provided at all. A deck plan shows what's where, but not how to actually walk from one place to another. Staff time is also spent on repetitive, answerable questions that a well-informed assistant could handle directly.

**The objectives:**
- Let guests ask natural-language questions about ship layouts and get accurate, specific answers.
- Ground every answer in the cruise line's actual deck plan documentation, not general assumptions.
- Provide practical wayfinding guidance between venues, not just static location facts.
- Support specific cabin-level questions, including accessibility.
- Help guests choose the right stateroom based on their personal preferences.

## 3. Solution

The "Holland America Deck Plans" agent, built in Microsoft Copilot Studio, is described in its own configuration as a tool to help guests choose ideal staterooms, locate key amenities, and navigate the ship easily. The agent is configured to answer questions about deck layouts, explain cabin types (Oceanview, Verandah, Suites), guide stateroom selection based on preferences, detail public spaces by deck, differentiate between ship classes, and offer cabin-selection and motion-sensitivity tips, grounded in official Holland America documentation for the ship Rotterdam.

### What the Video Demonstrates

A direct location question, "Which deck is the casino on the Rotterdam?", is answered with the specific deck, along with other venues sharing that deck. A multi-step navigation request, "How do I get to the sport court from there?", has the agent work out the route between two different decks and provide clear, step-by-step directions, including practical tips about elevators and stairwells. A "nearest venue" query, "What is the closest bar to the sea view pool?", is answered with the specific bar, its deck, and a short description. A specific cabin accessibility check, "Is room VC6154 a handicap accessible room?", has the agent correctly identify the cabin type and deck, confirm it is not listed as an accessible stateroom according to the official deck plan legend, and offer to provide a list of cabins that are. Each answer is clearly grounded in named source references, specific deck plan documents, which are cited alongside the response.

### End-to-End Workflow, Step by Step

1. **Ask a question.** The guest asks about a venue, deck, cabin, or how to get somewhere on the ship.
2. **Retrieve the relevant information.** The agent searches its grounded knowledge sources, the ship's official deck plan documentation, for the relevant details.
3. **Reason through the answer.** For simple lookups, the agent returns the specific fact directly. For more complex requests, like directions between two venues, it works out the relevant decks and route.
4. **Respond clearly.** The agent presents the answer in plain language, citing the specific source documents it drew from.
5. **Offer relevant next steps.** The agent proactively offers to help further, for example suggesting a list of accessible cabins after confirming one specific cabin isn't accessible.

## 4. Solution Architecture & Technologies

- **Microsoft Copilot Studio**, the platform used to build and run the AI agent.
- **Holland America's official deck plan documentation**, the grounded knowledge source the agent draws its answers from.
- **A large language model (GPT-4.1)**, powering the agent's understanding and reasoning.
- **Knowledge grounding and retrieval**, connecting the agent to specific, official deck plan source documents, with citations returned alongside answers.

The agent's core logic is retrieval-grounded reasoning: rather than generating answers from general knowledge, it searches its connected deck plan documentation for the relevant facts, then reasons over them to answer the actual question asked. This distinction matters for the multi-step navigation question, where the agent doesn't just report where two venues are located. It works out a sensible route between them, via elevators or stairwells, and explains it step by step. Similarly, for the cabin accessibility question, it doesn't just describe the cabin. It specifically checks whether that cabin number appears in the deck plan's accessible-cabin listing before answering. Its AI capabilities include grounded knowledge retrieval, with every factual answer sourced from actual documentation and citations returned for verification, multi-step reasoning for navigation, synthesizing a practical route between two locations across different decks, precise specific lookups down to an individual cabin number, and proactive follow-up suggestions after answering a specific question.
