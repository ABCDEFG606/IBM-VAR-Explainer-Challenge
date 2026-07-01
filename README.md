NEXUSPITCH — Understand Every Moment of the Beautiful Game
An intelligent conversational web application built with Langflow that explains football (soccer) rules, fouls, and VAR protocols clearly to fans using the official IFAB Laws of the Game. Built specifically for the IBM June Innovation Challenge 2025.

🛑 The Problem Statement
Football is the world's most popular sport, with over 3.5 billion viewers globally, yet it suffers from a massive information gap during live play. While fans watch the games, zero real-time explanations are provided for complex refereeing decisions.

Key pain points include:

VAR Delays: Video Assistant Referee (VAR) decisions often take minutes, leaving fans in the stadium and at home completely in the dark with zero explanation.

Rule Confusion: Intricate regulations like the double-infraction offside or the ever-changing handball rules are fundamentally misunderstood by the majority of viewers.

Tactical Blindspots: Crucial tactical substitutions and formational shifts go largely unexplained during live match broadcasts.

Global Friction: As we approach World Cup scale events, severe cultural and language barriers prevent casual fans from fully understanding and enjoying the nuances of the game.

💡 Our Solution
NEXUSPITCH is an AI-powered soccer analysis web app that takes any match scenario, rule question, or VAR controversy and breaks it down from multiple expert perspectives. By combining advanced Retrieval-Augmented Generation (RAG) with dynamic 2D pitch animations, NEXUSPITCH transforms abstract, confusing rules into accessible, visual intelligence.

Key Features
Multi-Expert AI Breakdown: Get analysis from distinct personas—Rules Expert, Tactical Analyst, VAR Official, and the on-field Referee's POV—along with the Match Impact.

RAG Pipeline: Responses are strictly grounded in a vector database containing the official FIFA/IFAB Laws of the Game to prevent hallucination.

Dynamic 2D Pitch Animations: Unique, real-time tactical board animations generated for every scenario via the HTML5 Canvas API.

Conversation Memory: Context-aware memory enables users to ask follow-up, drill-down questions about specific plays.

Real Historic Examples: Classic World Cup incidents and famous match analogies are embedded into every explanation.

Live Football News Ticker: Powered via NewsAPI to inject trending real-world context into the AI's prompts.

Intelligent Intent Routing: The LangFlow orchestration layer intelligently switches between casual chat, complex match scenarios, and conversational follow-ups.

⚙️ How It Works (The Pipeline)
User Input: The user types a football scenario or question into the HTML dashboard.

Intent Classification: LangFlow receives the input and classifies the intent (casual / scenario / follow_up).

Knowledge Retrieval: For scenarios, Chroma DB performs a semantic similarity search against chunked documents of the official FIFA Laws of the Game.

Context Injection: The retrieved law chunks, live trending news context (via NewsAPI), and chat history are securely injected into the Prompt Template.

Generation: LLaMA 3.3-70B evaluates the rich context and generates a strictly formatted JSON response containing 17 specific analytical fields.

Frontend Parsing: The HTML/JS frontend parses the JSON ("Nuclear Scrub" method) and dynamically renders the 7-card expert dashboard.

Dynamic Visuals: The animation_type and coordinate data trigger a unique 2D pitch animation on the HTML5 Canvas, showing exactly how the play unfolds spatially.

🛠️ Tech Stack
Frontend: Pure HTML5, CSS3, JavaScript, Canvas API (optimized into a single-file delivery).

AI Orchestration: LangFlow (IBM supported platform).

LLM: LLaMA 3.3-70B accessed via Groq API for ultra-fast inference.

RAG Pipeline: Chroma DB + Vector Embeddings.

Knowledge Base: Official FIFA Laws of the Game (Markdown/PDF).

Memory Management: LangFlow Message History (Store + Retriever modes).

Live Context: NewsAPI.org.

Architecture Notes & IBM Compatibility:

Enterprise Ready: The current Groq LLM node in the LangFlow pipeline can be directly and seamlessly swapped for an IBM watsonx.ai node for enterprise-grade deployments.

Local Development: Fake Embeddings were utilized for local development to bypass hardware limitations, but this node can be easily swapped for any proper embedding model (e.g., IBM Granite or nomic-embed-text).

Live Context: NewsAPI provides live, real-world football context that is injected into every prompt, ensuring the AI is aware of current events.

📄 JSON Response Schema
The LLM is strictly constrained to output the following 17 fields to populate the UI:

response_type: Intent routing flag (casual, scenario, follow_up).

text_response: Conversational reply for casual intents.

follow_up_prompt: A suggested next logical question for the user.

incident_steps: Array detailing the chronological play-by-play sequence.

rules_expert: Array containing the exact IFAB rule interpretation.

law_reference: The specific FIFA Law number and clause title.

rule_visual: Text description of the Director's Cue/Visual layout.

tactical_analyst: Array explaining formational or tactical impacts.

referee_pov: Array detailing the referee's physical positioning and line of sight.

alternative_outcome: What legally happens if the infraction didn't occur.

real_example: Historical match precedent (e.g., a famous World Cup moment).

var_official: Array detailing VAR review parameters and protocols.

match_impact: Array detailing how the decision alters game momentum.

dynamic_visuals: Nested object containing coordinate mapping for the Canvas:

pitch_zone: (e.g., defensive_third, middle_third)

ball_start: (e.g., penalty_spot)

ball_end: (e.g., top_corner)

attacker: Position of attacking chip.

defender: Position of defending chip.

visual_caption: Short caption for the Canvas.

why_it_matters: Punchy summary of why this specific rule exists.

animation_type: String trigger for the CSS/Canvas animation block.

🎬 Animation Types
The UI supports 7 distinct 2D Canvas animations triggered by the LLM:

offside: Renders a moving offside line, an attacker mistiming a run, and a pop-up flag.

handball: Shows a defender blocking a shot trajectory with a flashing hand icon.

red_card: Animates the referee walking toward the offending player and presenting a red card.

penalty: Focuses on the penalty box, showing a goalkeeper dive and the ball hitting the net.

foul: Depicts a high-speed collision between two player chips with an impact graphic.

goal_review: Switches to a dark "VAR Monitor" view showing a ball hovering over a goal line.

generic: A standard tactical board showing basic player movement and ball passing.

💬 Sample Interaction
User Input:

"A defender deliberately handles the ball inside the penalty box to stop a goal. What is the correct call and does VAR review this?"

System Output Summary:

rules_expert: "Under Law 12, handling the ball to deny an obvious goal-scoring opportunity (DOGSO) results in a penalty kick and a red card for the defender."

law_reference: "Law 12: Fouls and Misconduct"

var_official: "VAR automatically reviews all penalty decisions and potential straight red cards. The check will confirm if the handling was deliberate and inside the 18-yard box."

animation_type: "penalty"

real_example: "Luis Suárez (Uruguay) vs Ghana, 2010 World Cup Quarter-Final."

🚀 How To Run Locally
Prerequisites
Python 3.x installed.

LangFlow installed (pip install langflow).

Groq API Key (Free tier available at console.groq.com).

NewsAPI Key (Free tier available at newsapi.org).

Optional: Ollama installed with nomic-embed-text for running local embeddings.

Installation Steps
Clone the repository:

Bash
git clone https://github.com/yourusername/IBM-VAR-Explainer-Challenge.git
cd IBM-VAR-Explainer-Challenge
Start LangFlow:

Bash
python -m langflow run
Configure the AI Backend:

Open LangFlow in your browser (usually [http://127.0.0.1:7860](http://127.0.0.1:7860)).

Import the flow.json file provided in this repository.

Click on the Groq LLM node and paste your Groq API Key.

Build/Compile the flow.

Configure the Frontend:

Open index.html in a code editor.

Locate the <script> section at the bottom.

Update the LANGFLOW_API_URL to match your local LangFlow endpoint.

Paste your NEWS_API_KEY into the designated variable.

Launch the App:

Bash
python -m http.server 8080
Play: Open http://localhost:8080/index.html in your browser.

📁 Project Structure
Plaintext
IBM-VAR-Explainer-Challenge/
├── index.html              # Complete frontend dashboard, UI, and Canvas logic (Single File)
├── flow.json               # LangFlow pipeline export (Import this into LangFlow)
├── fifa_rules_clean.md     # RAG Knowledge Base: The official FIFA/IFAB Laws of the Game
└── README.md               # Project documentation
🏆 IBM Tool Spotlight: LangFlow
LangFlow acts as the absolute backbone of NEXUSPITCH. We utilized it to visually orchestrate a complex, multi-agent AI workflow. It handles the heavy lifting of:

Intent Classification: Dynamically routing the prompt based on conversational context.

RAG Pipeline Management: Chunking the FIFA rulebook, generating embeddings, and executing similarity searches via Chroma DB.

Memory Handling: Utilizing Store and Retriever modes to keep track of follow-up questions.

Structured Output Generation: Forcing the LLM to strictly adhere to the massive 17-field JSON schema required by our frontend.

🌍 Why NEXUSPITCH Matters
The 2026 FIFA World Cup will be the largest sporting event in human history, projected to be watched by over 4 billion people across North America and the globe. NEXUSPITCH is designed to democratize the rules of the game. By translating dense, bureaucratic referee regulations into transparent, visual, and easily digestible insights, we make football understandable for everyone—regardless of their prior knowledge level, culture, or native language. It represents the perfect use-case for explainable AI at a global scale.

🔭 Future Scope (Roadmap)
IBM Granite Integration: Swapping the current LLM for natively hosted IBM Granite models via watsonx.ai for maximum enterprise compliance.

Live Match Data API: Connecting to premium APIs (like Opta) to automatically ingest live foul locations and player coordinates without user text input.

Multilingual Support: Auto-translating the IFAB rules and AI outputs to support the global World Cup audience.

Native Voice Narration: Generating AI text-to-speech commentary to read the "Play-by-Play" breakdown aloud for accessibility.

Mobile Application: Porting the HTML5 Canvas logic into a React Native wrapper for iOS and Android deployment.
