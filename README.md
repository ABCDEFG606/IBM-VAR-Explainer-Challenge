# IBM-VAR-Explainer-Challenge
An intelligent conversational application built in Langflow that explains football (soccer) rules, fouls, and VAR protocols clearly to fans using the official IFAB Laws of the Game.


# NEXUSPITCH — Understand Every Moment of the Beautiful Game

Built for the **IBM June Innovation Challenge 2025**.

## Problem Statement
3.5 billion fans watch football but most don't understand VAR decisions, offside rules, tactical changes, or controversial moments. No accessible AI tool exists to explain these moments clearly and accurately.

## Our Solution
NEXUSPITCH is an AI-powered soccer analysis web app that takes any match scenario, rule question, or VAR controversy and breaks it down from multiple expert perspectives with dynamic 2D pitch animations.

## Key Features
*   **Multi-expert AI breakdown:** Rules Expert, Tactical Analyst, VAR Official, Referee POV, and Match Impact.
*   **RAG pipeline:** Grounded in official FIFA Laws of the Game.
*   **Dynamic 2D pitch animations:** Unique to every scenario via HTML5 Canvas.
*   **Conversation memory:** For follow-up drill-down questions.
*   **Real historic World Cup examples:** Embedded in every explanation.
*   **Live football news ticker:** Powered via NewsAPI.
*   **Intent routing:** Intelligently switches between casual chat, real scenarios, and follow-up questions.

## Tech Stack
*   **Frontend:** Pure HTML5, CSS3, JavaScript, Canvas API (single file)
*   **AI Orchestration:** LangFlow (IBM supported tool)
*   **LLM:** LLaMA 3.3-70B via Groq API *(Note: This node can be swapped directly for an **IBM watsonx.ai** node)*
*   **RAG Pipeline:** Chroma DB + Embeddings *(Note: Fake Embeddings were used for local development due to hardware limitations and lack of IBM cloud access, but this can be swapped for **any** standard embedding node)*
*   **Knowledge Base:** Official FIFA Laws of the Game
*   **Memory:** LangFlow Message History (Store + Retriever modes)
*   **News:** NewsAPI.org

## Architecture Flow
```text
User Input → LangFlow → Intent Classification → Chroma DB RAG Search → LLM → Structured JSON → Frontend Renders Dynamic Sections + Canvas Animations

JSON Response Schema

JSON
{
  "response_type": "string",
  "text_response": "string",
  "incident_steps": ["string"],
  "rules_expert": ["string"],
  "law_reference": "string",
  "rule_visual": "string",
  "tactical_analyst": ["string"],
  "referee_pov": ["string"],
  "alternative_outcome": ["string"],
  "real_example": "string",
  "var_official": ["string"],
  "match_impact": ["string"],
  "dynamic_visuals": "string",
  "follow_up_prompt": "string",
  "animation_type": "string",
  "why_it_matters": "string"
}

How To Run
Clone the repository.

Install and open LangFlow locally.

Import the provided LangFlow flow JSON file.

Configure LangFlow:

Open the flow and add your Groq API key into the Groq LLM node. (Alternatively, you can replace the Groq node with an IBM watsonx.ai node).

Embedding Note: The flow currently uses a "Fake Embedding" node to accommodate lower-end local hardware. You can easily replace this with any proper embedding node of your choice.

Configure Frontend:

Open index.html in your code editor.

Add your LANGFLOW_API_URL at the top of the <script> section.

Add your NEWS_API_KEY at the top of the <script> section.

Inside the fetch(LANGFLOW_API_URL, {...}) call, paste your actual LangFlow/Groq API key in the x-api-key header.

Open a terminal in the project folder and run: python -m http.server 8080

Open your browser and navigate to: http://localhost:8080/index.html

IBM Tool Used
LangFlow — used as the core AI orchestration layer for intent classification, RAG pipeline management, memory handling, and structured JSON output generation.

Why NEXUSPITCH Matters
World Cup 2026 will be watched by billions. NEXUSPITCH makes football understandable for everyone — across languages, cultures, and knowledge levels — using explainable, transparent AI at global scale.

Future Scope
Multilingual support

Live match data API integration

Voice narration of explanations

Mobile app version

IBM Granite model integration for full IBM compliance


