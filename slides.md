# LLMs, Agents & Retrieval – GDIT Hackathon Deep-Dive

*A 60-minute, business-friendly crash-course that arms you with enough AI know-how to design, test, and demo your own **agents** during the event.*

---

## Slide 1 ▸ Welcome & Goals
- **Why we’re here** – turn raw text + AI into useful business answers.
- **What you’ll learn**
  1. Core building blocks: LLM → Embeddings → Agent → Tools.
  2. When an agent outperforms a chatbot or a bespoke ML model.
  3. How to prep data, phrase prompts, and read the agent’s “thinking”.
- **Session flow** – Theory (30 min) ▸ Demo walk-through (15 min) ▸ Q&A (15 min).

---

## Slide 2 ▸ What *Is* a Large Language Model?
- Trained on **billions** of sentences → predicts the next token.
- *Analogy:* a super-charged “auto-complete” that’s absorbed Wikipedia + the open web.
- **Strengths**
  - Fluent summaries, first-draft writing, code stubs, Q-and-A.
  - Can generalise to brand-new topics (zero-shot ability).
- **Limitations**
  - Knowledge cut-off date (no baked-in “today”).
  - Can *hallucinate* – state plausible but untrue facts.
  - Needs clear instructions; vague in → vague out.

---

## Slide 3 ▸ Talking to an LLM: Prompts & Tokens
- **Prompt** – your plain-English task (“Summarise this in 3 bullets”).
- **Tokens** – word pieces the model reads; each model has a max window (e.g., 8 k tokens ≈ ~6 pages).
- **Prompt craft tips**
  - Prefer specific verbs (“List”, “Prioritise”, “Compare”).
  - Give examples when possible (few-shot).
  - Specify style & length (“<150 words, bullets”).
- *Garbage-in ⇒ garbage-out.* Good prompts ≈ good answers.

---

## Slide 4 ▸ Embeddings – GPS Coordinates for Text
- Converts any text into a 1 024-dimensional vector.
- Similar meaning → vectors *close* (small cosine distance).
- Enables **semantic search** – find “income support” even if doc says “financial aid”.
- Used for: clustering, deduping, recommendation, **vector search**.

---

## Slide 5 ▸ Agents ≠ Chatbots
- **Agent = LLM + memory + tools + control loop.**
- Can *plan* multi-step reasoning (“search → compare → calculate → respond”).
- Calls **tools** (search, calculators, APIs) like a junior analyst would.
- Maintains thread memory → coherent follow-ups across a session.
- *Outcome:* answers are sourced, actionable, less hand-wavy.

---

## Slide 6 ▸ Why Agents vs. Fine-Tuning or “One-Shot” Search
| Approach | Pros | Cons | Best For |
|----------|------|------|----------|
| **Fine-tune a model** | Domain mastery | Weeks, $$$, static | Massive, stable corpora |
| **Single-shot search** | Easy, cheap | No multi-step logic | Simple fact lookups |
| **Agent** | Plans, tools, adaptable | Needs good prompts & infra | Complex workflows, data mash-ups |

*Take-away:* Agents give you *flexibility* and *freshness* without re-training giant models.

---

## Slide 7 ▸ Agent Frameworks in the Wild
- **ReAct** *(Reason ↔ Act)* – think → call tool → observe result → think …
- **Plan–Evaluate–Execute** – draft a plan, self-critique, then run.
- **Router / Mixture-of-Experts** – pick specialised sub-agents by topic.
- **Retriever-Reader Loops** – iterate fetch-&-refine for long docs.
- We’ll focus on a lean **ReAct-style** pattern (great for business Q&A).

---

## Slide 8 ▸ Anatomy of an Agent
1. **Planner** – breaks request into steps.
2. **Router** *(optional)* – sends task to a sub-agent or picks best tool.
3. **Tools** – File Search, Web Search, calculators, CRM APIs, etc.
4. **Memory / Thread** – stores conversation or workflow state.
5. **Evaluator / Guardrail** – sanity-checks answers before user sees them.

---

## Slide 9 ▸ Where Agents Shine & Where They Struggle
### ✅ Excel at
- Synthesising info across documents.
- Repetitive analysis (metric → threshold → action).
- “Bread-crumb” tasks no single doc answers.
### ⚠ Fail when
- Data isn’t in the vector store or web snippet.
- Prompts are vague: “Tell me everything about shipping.”
- Need live, numeric data but no calculator/API tool.
- Over-long context > model window.

---

## Slide 10 ▸ Vector Stores – Your Private Library
- **Document chunks** + **embeddings** stored as rows.
- Think of it as “Google for your PDFs” – but semantic.
- Fast nearest-neighbour search (< 300 ms over 1 M chunks).
- Supports metadata filters (date, author, doc type).

---

## Slide 11 ▸ Chunking & Loading – Golden Rules
- **300–1 000 tokens** per chunk (≈ 1–3 paragraphs).
- **10–20 % overlap** so a sentence on the boundary isn’t lost.
- Pre-clean docs: remove headers/footers, OCR images to text.
- Tag with metadata → “policy_type: EPA”, “year: 2024”.
- *Test:* run sample query; if retrieval looks noisy, tweak size/overlap.

---

## Slide 12 ▸ Under the Hood of Vector Search
1. Embed user query → vector Q.  
2. *k-NN* search finds closest vectors.  
3. Return top-N chunks (+ metadata).  
4. Agent cites or quotes those chunks.  
*Mathematics:* cosine similarity on GPU-accelerated index.

---

## Slide 13 ▸ Web Search Workflow (BraveSearch Example)
1. **search_query** – returns titles + 150-char snippets for top 10 hits.  
2. Agent skims titles/snippets → chooses promising URL(s).  
3. **open / click** – fetches ~300 lines of cleaned HTML text for context.  
4. Agent can scroll further with another *open* call if needed.  
*Great for*: breaking news, official .gov/.org guidelines, recent stats.

---

## Slide 14 ▸ Tool Playbook – Which Tool, When?
| Scenario | File Search | Web Search | Neither (LLM only) |
|----------|------------|------------|--------------------|
| Quote contract clause 5.3 | ✔ | | |
| “Latest FY24 USPS shipping rates?” | | ✔ | |
| Explain difference between parcel & flat mail | | | ✔ |

---

## Slide 15 ▸ Mini Demo – Agent Lifecycle
1. **User:** “Is pump #12 showing abnormal pH?”  
2. **Plan:** search → compare threshold → answer.  
3. **Tool call:** File Search query “sensor 12 last 24 h pH”.  
4. **Observation:** chunk shows pH = 8.9 (threshold > 8.5).  
5. **Answer:** “Yes – exceeds limit, schedule flush within 2 hours.”  
*(Logs show each step & citation.)*

---

## Slide 16 ▸ Managed Agent Platforms (Example Features)
- Hosted vector store (auto-scales, encrypted).  
- Drag-and-drop ingestion UI + progress dashboard.  
- Sandbox chat for human-in-the-loop testing.  
- API & SDK for batch runs, automation, extensions.  
- Pluggable tools: web search, SQL, e-mail, other agents.

---

## Slide 17 ▸ From Dataset to Demo – Step Checklist
1. **Choose dataset** → verify it contains answers you’ll need.  
2. **Ingest & index** → pick chunk size/overlap.  
3. **Define tools** → File Search (DB ID) + optional Web Search.  
4. **Write agent instructions** → role, tool rules, tone, format.  
5. **Dry-run** simple Qs → iterate prompt & data.  
6. **Prepare 3–4 killer demo queries** → show value fast.

---

## Slide 18 ▸ Hackathon QA & Performance Tips
- Keep answers < 200 words unless user asks for full report.  
- Aim for total run-time < 15 s (tool calls dominate).  
- Monitor logs – if top chunk isn’t relevant, tweak query or data.  
- Version your prompt: **v1-short**, **v2-with-examples**, etc.  
- Build a “cheat sheet” of go-to queries to stress-test your agent.

---

## Slide 19 ▸ Resources & Support
- Participant Guide  
- Slack **#hack-help** – mentors online, 5 min response target.  
- Quick-start code snippets (Python) for ingestion & agent creation.  

---

## Slide 20 ▸ Let’s Build Great Agents!
- **Experiment boldly** – iterate, measure, refine.  
- **Verify facts** – trust but verify every citation.  
- **Collaborate** – share tricks & blockers; hackathons are team sports.  
- Good luck, have fun, and wow the judges!