# Official Prompt Guidance (Latest Reasoning Models)

### 1. Outcome-First Prompts
*   **Stop detailing the steps:** Do not force the model through rigid "first do A, then do B" frameworks. Let the model choose its own efficient path to the solution. 
*   **Describe the destination:** Focus on defining what "done" looks like. Clearly describe the target outcome, success criteria, constraints, available evidence, and what the final answer should contain.

### 2. Personality vs. Collaboration Behavior
*   **Personality:** Define tone (warmth, directness, formality, empathy). Keep it concise.
*   **Collaboration Style:** Define task behavior (assumptions vs. questions, proactivity, risk handling).
*   **Rule of thumb:** Ask for clarification only when missing information would materially change the answer or cause a high-risk mistake. Otherwise, make reasonable assumptions to move the task forward.

### 3. The "Preamble" Trick
*   Prompt the model to emit a short, 1-2 sentence user-visible "preamble" before it executes any tools. 
*   This preamble should acknowledge the request and state the first concrete step it is taking, which massively improves perceived responsiveness (Time-to-First-Token) during tool calls.

### 4. Formatting Guidelines
*   **Default to plain text:** Use plain paragraphs by default. 
*   **Minimize heavy structure:** Use headers, bold text, bullets, and numbered lists sparingly. Reserve them for comparisons, checklists, or steps.
*   **Structure of argument:** Prioritize the conclusion first, followed by the reasoning. Include caveats only if they materially affect the answer.

### 5. Creative Drafting Guardrails
*   **Strict facts:** Concrete metrics, product roadmaps, dates, and claims must be pulled strictly from retrieved context and cited with inline links.
*   **Handling missing data:** Do not invent names or metrics to make a draft sound stronger. Write a generic draft with clearly labeled placeholders rather than hallucinating.

### 6. Grounding and Citations
*   Specify exact rules for citations (e.g., inline links placed immediately next to the claims they support).
*   If retrieved sources conflict, state the conflict and attribute each side.
*   If evidence is completely missing, state exactly what is missing rather than guessing. 

### 7. Avoid Absolutes
*   Avoid screaming absolutes like "ALWAYS" or "NEVER" unless it is a strict schema requirement or hard safety invariant. 
*   Use conditional logic instead ("If X, then Y. Otherwise Z.") so you do not lock down the model's ability to make judgment calls.

### 8. Stopping Conditions for Agents
*   Prompt looping agents to ensure they are giving a complete and grounded answer before stopping.
*   Condition example: "Resolve the query in the fewest useful tool loops, but do not let loop minimization outrank correctness. After each result, ask: 'Can I answer the user's core request now with useful evidence?' If yes, answer."

### 9. Reasoning Effort & State Management
*   **Reasoning Effort:** Test workflows on "Low" or "Medium" before escalating to "High" to prevent unnecessary budget burn and latency.
*   **Phase Parameter:** If manually managing state (passing output items back each turn), preserve the `phase` parameter on returned assistant items to maintain preambles and multi-step reasoning.