# GDIT Hackathon Participant Guide: Building Effective AI Agents

Welcome, hackers! This guide will help you think creatively, explore possibilities, and get the most out of the SeekrFlow platform during the hackathon.

For each challenge, we’ve provided key considerations, creative prompts, and tips to guide your thinking and spark innovative solutions—without limiting your creativity.

Let’s dive in!

---

## General Pro Tips Across All Challenges

- **Start Simple, Then Iterate:** Begin with straightforward queries, gradually increasing complexity. This quickly isolates issues.  
- **Clear & Concise Instructions:** Short, numbered instructions help guide agent actions clearly.  
- **Leverage Tool Strengths:**  
  - **FileSearch:** Best for internal documentation and specific historical data.  
  - **WebSearch:** Ideal for quick external context checks or background verification.  
- **Creative Prompting:** Thoughtful, precise questions dramatically improve agent outcomes.  
- **Evaluate Critically:** Agents need oversight; always double-check critical outcomes.  

---

## Chunking & Embedding Strategies (Foundational Considerations)

- **Balanced Chunk Sizes:** Aim for 300–1,000 tokens for optimal retrieval.  
- **Overlap Tokens:** Maintain ~10–20 % overlap for continuity.  
- **Extreme Chunk Sizes:** Avoid very large (>1,000 tokens) or very small (<300 tokens) chunks.  
- **Excessive Overlap:** Avoid redundant overlap that impacts efficiency.  
- **Match to Model:** Align chunk sizes with your chosen model’s context window.  
- **Test and Adjust:** Experiment to identify the best chunk size for your case.  

---

## Challenge 1: Water Quality Monitoring

**Key Considerations**

- Sensor Data: How might sensor readings relate to contamination or maintenance issues?  
- Historical Patterns: Can past incidents predict future problems?  

**Tips for Creativity**

- Craft targeted questions for effective retrieval.  
- Clearly specify how sensor data should be interpreted in agent instructions.  

**Potential Pitfalls**

- Avoid overly broad queries; be specific.  
- Web search provides short snippets; useful for context but not detailed analyses.  

---

## Challenge 2: Medicaid Work Requirements

**Key Considerations**

- Eligibility Factors: Which indicators confirm Medicaid work requirements?  
- Job Training: How might you identify suitable training opportunities?  

**Tips for Creativity**

- Frame structured queries clearly outlining individual profiles.  
- Consider breaking down complex scenarios into follow-up questions.  

**Potential Pitfalls**

- Vague eligibility questions yield weaker results—clarity is key.  
- Web search snippets are brief; use them for quick verifications, not policy details.  

---

## Challenge 3: USPS Fraud Detection

**Key Considerations**

- Suspicious Patterns: What oddities (weights, addresses, shipping times) could suggest fraud?  
- Historical Patterns: How might past cases inform identification of new fraud?  

**Tips for Creativity**

- Ask the agent to compare suspicious package details to known fraudulent examples.  
- Use web search strategically—perhaps to validate suspicious addresses.  

**Potential Pitfalls**

- Web search is supplementary—don’t rely solely on it for definitive proof.  
- Avoid overly vague “fraud” queries; specificity improves outcomes.  

---

## Challenge 4: Refugee Interview Analysis

**Key Considerations**

- Consistency: Identify clear inconsistencies within refugee interviews.  
- External Context: Verify geopolitical or historical claims through external sources.  

**Tips for Creativity**

- Frame focused questions around specific claims.  
- Use web searches for quick contextual checks (dates, events).  

**Potential Pitfalls**

- Web search snippets are brief; ideal for quick fact-checks, not in-depth analysis.  
- Ensure your vector store queries clearly reference specific interview details.  

---

## Challenge 5: Military OPORD Analysis

**Key Considerations**

- Actionable Information: What parts of the OPORD contain critical, actionable tasks?  
- Summarization Styles: Which summary formats (bulleted, narrative, timeline) best support rapid decision-making?  

**Tips for Creativity**

- Reference specific sections clearly in your queries.  
- Experiment with summarization styles for clarity.  

**Potential Pitfalls**

- Avoid overly broad requests (“Summarize entire OPORD”)—focus on actionable items.  
- Clearly specify military terms if their meaning might be ambiguous to the agent.  

---

## Tool Configuration and Usage

### File Search Tool

**Best Practices**

- Clearly define tool descriptions aligning with expected behavior.  

**Pitfalls**

- Missing or unclear descriptions can reduce accuracy.  

**Tips**

- Explicitly instruct the agent on when to use file search (e.g., “Search internal policies for …”).  

### Web Search Tool

**Best Practices**

- Formulate clear, concise search queries with specific keywords.  

**Pitfalls**

- Results are short snippets—important details might be missed.  

**Tips**

- Clearly instruct agents on when to leverage web search for external context.  

---

## Crafting Effective Agent Instructions

**Best Practices**

- Clearly define roles and tasks using simple, structured language (bullet points, numbered lists).  

**Pitfalls**

- Avoid contradictory instructions or overly complex directives.  

**Tips**

- Provide conditional instructions explicitly (e.g., “IF asked about X, THEN use Y tool.”)  
- Specify exact output formats for clarity.  

---

## Model Selection Considerations

**Best Practices**

- Select models according to task complexity and resources.  

**Pitfalls**

- Larger models aren’t always better; consider context window and cost.  

**Tips**

- Test smaller and larger models to balance performance, speed, and cost effectively.  

| Model | Tool-calling reliability | Notes |
|-------|--------------------------|-------|
| Mistral-7B-Instruct v0.3 / v0.2 | ★★★★ | Very consistent; low latency. |
| Llama-3.1-8B-Instruct | ★★★★ | Larger context window (32 K) helps with multi-step plans. |
| Llama-3.1-70B-Instruct | ★★★★★ | High reasoning depth; handles complex tool chains. |
| Llama-3.3-70B-Instruct | ★★★★★ | Latest tuning; same strong tool adherence. |
| Llama-2-70B-chat-hf | ★★★ | Stable legacy option; needs a bit more prompt explicitness but works fine. |

---

## Effective Prompting Strategies

**Best Practices**

- Encourage step-by-step reasoning with clear prompts (“Let’s think through this step-by-step”).  

**Pitfalls**

- Overly complex prompts can confuse agents; integrate retrieved info clearly.  

**Tips**

- Use a structured “Thought-Action-Observation” approach to guide responses.  
- Refine prompts continually based on observed agent behavior.  

---

## General Caveats and Tips

- **No Fine-Tuning:** Your agent relies solely on clarity and specificity of instructions.  
- **Web Search Limitations:** Use web search snippets for quick checks; supplement with detailed sources if needed.  
- **Critical Review:** Always cross-verify agent outputs, using reasoning and citations as checkpoints rather than absolute facts.  

---

## Good Luck and Have Fun!

Your creativity and innovative thinking will make the difference. Happy hacking!
