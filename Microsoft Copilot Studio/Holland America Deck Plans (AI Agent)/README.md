# Holland America Deck Plans Agent

A conversational AI agent, built on Microsoft Copilot Studio, that answers detailed questions about Holland America cruise ship layouts — where things are, how to get between them, and whether a specific cabin meets a guest's needs — all grounded in the cruise line's actual deck plan documentation.

## 1. Project Overview

This project is a working AI assistant for cruise ship navigation and cabin selection. Rather than guests scrolling through static deck plan PDFs or maps, they can simply ask the agent a question — "Which deck is the casino on?", "How do I get from there to the sport court?", "Is cabin VC6154 wheelchair accessible?" — and get a clear, accurate answer sourced directly from the ship's official deck plan documentation.

## 2. Business Context

Cruise ships are large, complex vessels with dozens of decks, hundreds of cabins, and a wide range of dining, entertainment, and recreation venues. Guests booking a cruise, or already onboard, often need quick answers about where things are, how to get between them, or whether a specific cabin suits their needs (location preference, accessibility, proximity to elevators, and so on). Traditionally, this means digging through a static deck plan PDF or asking staff directly.

## 3. Business Problem

Deck plans are information-dense but not easy to use in the moment:

- **Static plans require manual interpretation.** A guest has to visually scan a deck-by-deck diagram to find a specific venue or work out how two locations relate to each other.
- **Cabin-specific questions are hard to self-serve.** Knowing whether a specific cabin number is accessible, quiet, or well-located isn't obvious from a deck map alone.
- **Wayfinding between venues isn't provided at all** — a deck plan shows what's where, but not how to actually walk from one place to another.
- **Staff time is spent on repetitive, answerable questions** that a well-informed assistant could handle directly.

## 4. Project Objectives

- Let guests ask natural-language questions about ship layouts and get accurate, specific answers.
- Ground every answer in the cruise line's actual deck plan documentation, not general assumptions.
- Provide practical wayfinding guidance between venues, not just static location facts.
- Support specific cabin-level questions, including accessibility.
- Help guests choose the right stateroom based on their personal preferences.

## 5. What the Video Demonstrates

The video shows the **"Holland America Deck Plans"** agent, built in Microsoft Copilot Studio, described in its own configuration as a tool to help guests *"choose ideal staterooms, locate key amenities, and navigate the ship easily."* The agent is configured to answer questions about deck layouts, explain cabin types (Oceanview, Verandah, Suites), guide stateroom selection based on preferences, detail public spaces by deck, differentiate between ship classes, and offer cabin-selection and motion-sensitivity tips. The demonstration shows the agent, grounded in official Holland America documentation for the ship *Rotterdam*, handling:

- A direct location question — **"Which deck is the casino on the Rotterdam?"** — answered with the specific deck, along with other venues sharing that deck.
- A **multi-step navigation request** — "How do I get to the sport court from there?" — where the agent works out the route between two different decks and provides clear, step-by-step directions, including practical tips about elevators and stairwells.
- A **"nearest venue" query** — "What is the closest bar to the sea view pool?" — answered with the specific bar, its deck, and a short description.
- A **specific cabin accessibility check** — "Is room VC6154 a handicap accessible room?" — where the agent correctly identifies the cabin type and deck, confirms it is *not* listed as an accessible stateroom according to the official deck plan legend, and offers to provide a list of cabins that are.

Each answer is clearly grounded in named source references (specific deck plan documents), which are cited alongside the response.

## 6. End-to-End Workflow, Step by Step

1. **Ask a question.** The guest asks about a venue, deck, cabin, or how to get somewhere on the ship.
2. **Retrieve the relevant information.** The agent searches its grounded knowledge sources — the ship's official deck plan documentation — for the relevant details.
3. **Reason through the answer.** For simple lookups, the agent returns the specific fact directly. For more complex requests (like directions between two venues), it works out the relevant decks and route.
4. **Respond clearly.** The agent presents the answer in plain language, citing the specific source document(s) it drew from.
5. **Offer relevant next steps.** The agent proactively offers to help further — for example, suggesting a list of accessible cabins after confirming one specific cabin isn't accessible.

## 7. Systems and Applications Involved

- **Microsoft Copilot Studio** — the platform used to build and run the AI agent
- **Holland America's official deck plan documentation** — the grounded knowledge source the agent draws its answers from

## 8. Technologies Used

- **Microsoft Copilot Studio** — for building the agent's conversation flow and knowledge grounding
- **A large language model (GPT-4.1)** — powering the agent's understanding and reasoning
- **Knowledge grounding / retrieval** — connecting the agent to specific, official deck plan source documents, with citations returned alongside answers

## 9. Automation Logic

The agent's core logic is retrieval-grounded reasoning: rather than generating answers from general knowledge, it searches its connected deck plan documentation for the relevant facts, then reasons over them to answer the actual question asked. This distinction matters for a request like the multi-step navigation question — the agent doesn't just report where two venues are located; it works out a sensible route between them (via elevators or stairwells) and explains it step by step. Similarly, for the cabin accessibility question, it doesn't just describe the cabin — it specifically checks whether that cabin number appears in the deck plan's accessible-cabin listing before answering.

## 10. AI Capabilities

- **Grounded knowledge retrieval**: every factual answer is sourced from actual deck plan documentation, with citations returned so the source can be verified.
- **Multi-step reasoning for navigation**: the agent doesn't just state facts — it synthesizes a practical route between two locations across different decks.
- **Precise, specific lookups**: the agent can answer questions down to the level of an individual cabin number, correctly distinguishing it from similar-sounding cabin categories.
- **Proactive follow-up suggestions**: after answering a specific question, the agent offers a relevant next step (like a list of accessible cabins) rather than ending the interaction abruptly.

## 11. User Interactions

- Guests interact with the agent entirely through natural conversation, asking questions the way they would to ship staff or a knowledgeable travel agent.
- The agent responds with clear, structured answers and offers relevant follow-up help without requiring the user to know what to ask next.
- No account setup or navigation of a separate deck plan document is required — the agent handles the lookup and interpretation directly.

## 12. Inputs and Outputs

**Inputs:**
- Natural-language questions about ship venues, decks, navigation, or specific cabins

**Outputs:**
- Clear, specific answers about deck locations and venues
- Step-by-step navigation directions between two points on the ship
- Cabin-specific details, including accessibility status
- Cited references to the specific source documentation used

## 13. Error Handling and Validation

- By grounding answers in official deck plan documentation rather than general assumptions, the agent reduces the risk of giving inaccurate location or accessibility information — a category of question where accuracy genuinely matters for guests with specific needs.
- The agent explicitly checks a specific cabin against the accessible-cabin listing, rather than guessing based on cabin category alone, before answering an accessibility question.
- Citing source references alongside each answer gives the user a way to verify the information independently.

## 14. Business Rules

- Answers about ship layout, venues, and cabins must be grounded in the official deck plan documentation, not general assumptions.
- Accessibility questions must be answered by checking the specific cabin against the documented accessible-cabin listing, not inferred from the cabin's general category.
- Navigation guidance must account for the actual layout of the ship (deck numbers, elevator/stairwell locations), not just list the two locations involved.

## 15. Key Features Demonstrated

- Grounded, citation-backed answers to ship layout questions
- Multi-step wayfinding/navigation guidance between venues
- "Nearest venue" style lookups
- Precise, cabin-specific accessibility verification
- Proactive, relevant follow-up suggestions

## 16. Business Value and Benefits

- **Faster, self-service answers** for guests, without needing to interpret a static deck plan or wait on staff availability.
- **More accurate cabin guidance**, particularly for accessibility needs, where getting the answer wrong has real consequences for a guest's experience.
- **Reduced staff workload** for routine, repetitive wayfinding and cabin questions.
- **A more confident booking and onboard experience**, since guests can get specific answers before making decisions rather than guessing from a static map.

## 17. Productivity Improvements

- Removes the need for guests to manually interpret complex deck plan diagrams.
- Reduces repetitive staff inquiries about common wayfinding and cabin questions.
- Speeds up decision-making during cabin selection by providing specific, relevant answers on demand.

## 18. Time or Cost Savings (If Evident)

The video shows several distinct questions — a venue lookup, a multi-step navigation request, a nearest-venue search, and a specific cabin accessibility check — each answered clearly within seconds. It doesn't demonstrate large-scale usage volume or a direct cost comparison against staff-handled inquiries, so no specific dollar or hour savings figure is claimed here. That said, deflecting routine wayfinding and cabin questions to a self-service, grounded AI assistant is a well-established way to reduce guest service workload, particularly for repetitive, factual questions.

## 19. Skills Demonstrated

- Designing a knowledge-grounded AI agent in Microsoft Copilot Studio
- Connecting an AI agent to structured source documentation with citation support
- Building multi-step reasoning capability (navigation) on top of grounded facts
- Designing for precise, specific lookups (individual cabin accessibility) rather than only general answers
- Structuring agent instructions to cover a defined, practical scope (deck layouts, cabin types, ship classes, cabin selection tips)

## 20. Real-World Enterprise Use Cases

This kind of grounded, navigation-capable assistant pattern applies broadly, including:

- **Cruise and hospitality wayfinding** — exactly as demonstrated here
- **Large venue navigation** — stadiums, convention centers, airports, or hospitals, where wayfinding between points is a common need
- **Product or facility documentation assistants** — answering specific, grounded questions from technical or reference documentation
- **Accessibility verification tools** — checking specific rooms, seats, or facilities against accessibility requirements
- **Retail or campus wayfinding** — helping visitors find specific locations within a large, complex space

## 21. Lessons Learned

- Grounding answers in actual source documentation, with citations, is what makes an AI assistant trustworthy for questions where accuracy genuinely matters (like accessibility).
- Multi-step reasoning (like synthesizing directions between two points) is far more useful than simple fact lookup — it's the difference between "here's where things are" and "here's how to actually get there."
- Precise, specific lookups (down to an individual cabin number) demonstrate real practical value beyond general Q&A.
- Proactively offering a relevant next step keeps a conversation useful without requiring the user to know what else to ask.

## 22. Possible Future Enhancements

- Add **visual deck plan rendering**, showing a highlighted map alongside text directions.
- Extend cabin guidance to include **personalized recommendations** based on stated preferences (quiet, mid-ship, near elevators), as referenced in the agent's own instructions.
- Add **ship class comparison** support (e.g., Pinnacle vs. Signature Class), also referenced in the agent's instructions but not shown in this demonstration.
- Include **motion sensitivity guidance**, helping guests choose cabins based on how much ship movement they're comfortable with.
- Expand coverage to **additional ships** in the fleet, beyond the Rotterdam shown here.
- Integrate directly with the **booking system**, allowing guests to check cabin availability alongside layout and accessibility information.

---

*This project is part of an Automation Playground portfolio, built to demonstrate how a grounded, reasoning AI agent can turn static reference documentation into practical, conversational guidance.*
