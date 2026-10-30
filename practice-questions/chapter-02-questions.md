## Chapter 2: Agentic AI: Tool Use, Planning, and Multi-Agent Orchestration — Practice Questions

**Q1.** A support team wants an AI system that checks order status via an internal REST API, looks up return policy from a document set, and then decides whether to approve a refund. Which approach BEST fits this requirement?

A) A single large prompt containing all policy text and asking the model to answer in one shot
B) Fine-tune a model on historical support transcripts and deploy it as a static Q&A bot
C) An agentic system that uses function calling to hit the order API and a retrieval tool for policy docs, orchestrated through a planning loop
D) Deploy a NIM microservice with no tool integration and increase the context window size

<details>
<summary>Answer</summary>

**Correct: C**

The task requires live data (order status), external knowledge (policy docs), and a multi-step decision — this is the canonical case for an agent with function calling and tool orchestration rather than a single static response.

**Why the others are wrong:**
- A single prompt cannot call a live API for real-time order status; it can only reason over text given to it.
- Fine-tuning bakes in static knowledge and cannot fetch live order data or adapt to new orders.
- A model without tool access cannot perform actions like checking an external order status API, regardless of context size.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A developer needs the agent to recall facts stated earlier in the same conversation (e.g., the user's name and the ticket number) but does not need this information to persist after the session ends. Which memory type satisfies this requirement with the least added complexity?

A) Short-term (working) memory held in the conversation context
B) Long-term memory backed by a vector database
C) A fine-tuned model that memorizes user data permanently
D) A separate knowledge graph updated after every session

<details>
<summary>Answer</summary>

**Correct: A**

Short-term/working memory, typically the rolling context window or an in-session scratchpad, is sufficient and simplest when persistence beyond the session is not required.

**Why the others are wrong:**
- A vector database adds persistence and retrieval overhead that isn't needed for single-session recall.
- Fine-tuning is not a mechanism for session-specific memory and would leak data across all users.
- A knowledge graph is built for long-term structured recall, which is unnecessary overhead here.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team wants to classify a single incoming email as 'spam' or 'not spam' using an LLM. There are no external tools, no multi-step reasoning, and latency must be minimal. What is the BEST architectural choice?

A) A single direct LLM call with a well-crafted classification prompt
B) A multi-agent system with a planner, a classifier agent, and a verifier agent
C) A ReAct loop that reasons, calls a tool, and observes before answering
D) An agent with long-term memory to track prior classifications

<details>
<summary>Answer</summary>

**Correct: A**

When the task is single-step, requires no external tools, and latency matters, a direct single model call is correct — agent overhead (planning loops, orchestration) adds cost and latency without benefit.

**Why the others are wrong:**
- Multi-agent orchestration adds unnecessary latency and cost for a single classification decision.
- A ReAct loop is designed for tasks needing tool calls and iterative reasoning; there is no tool to call here.
- Long-term memory is irrelevant to a stateless single classification task and adds complexity.

</details>

---

**Q4.** A company has a fine-tuned LLM and wants to deploy it behind a standardized, OpenAI-compatible API with optimized inference, so it can be called as a tool by their agent framework. Which NVIDIA offering is designed for this?

A) NVIDIA NIM (Inference Microservice)
B) NeMo Guardrails
C) NVIDIA AI Blueprints
D) NeMo Curator

<details>
<summary>Answer</summary>

**Correct: A**

NIM packages optimized models into containerized microservices exposing a standard, OpenAI-compatible API, making them easy to call as tools from an agent orchestration layer.

**Why the others are wrong:**
- NeMo Guardrails adds programmable safety/control rails to conversational flows; it does not serve inference.
- AI Blueprints are reference workflow templates for building applications, not an inference-serving mechanism.
- NeMo Curator is used for large-scale data curation/preprocessing for training, not for deploying inference endpoints.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** An agentic application must prevent the LLM from executing off-topic requests, leaking system prompts, or being manipulated via prompt injection, using a configurable rails-based approach rather than only prompt engineering. Which tool is purpose-built for this?

A) NVIDIA NIM
B) A vector database for long-term memory
C) A larger context window
D) NeMo Guardrails

<details>
<summary>Answer</summary>

**Correct: D**

NeMo Guardrails is NVIDIA's toolkit for adding programmable guardrails (topical, safety, jailbreak/injection rails) to LLM-based conversational and agentic systems.

**Why the others are wrong:**
- NIM is for serving model inference; it has no built-in rails/policy engine of its own.
- A vector database stores and retrieves memory/embeddings; it does not enforce behavioral guardrails.
- Increasing context window size has no effect on topic control or prompt injection resistance.

</details>

---

**Q6.** In a ReAct-style agent loop, what is the correct order of a single iteration?

A) Action, Observation, Thought
B) Observation, Thought, Action
C) Thought, Action, Observation
D) Action, Thought, Observation

<details>
<summary>Answer</summary>

**Correct: C**

ReAct interleaves reasoning and acting: the agent first produces a Thought (reasoning about what to do), takes an Action (e.g., a tool/function call), then receives an Observation (the tool's result) which feeds the next Thought.

**Why the others are wrong:**
- Starting with Action skips the reasoning step that determines which action to take.
- Starting with Observation implies a result exists before any action was taken, which breaks the loop logic.
- Thought must precede Action, not follow it, since the action is chosen based on the thought.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** When configuring a function-calling schema for an agent's tool, which field is REQUIRED to let the model know what arguments the function accepts and their types?

A) The function's 'parameters' field defined as a JSON Schema object
B) The function's 'description' field only
C) A natural-language comment inside the system prompt
D) The model's temperature setting

<details>
<summary>Answer</summary>

**Correct: A**

Standard function/tool-calling schemas (e.g., OpenAI-style, used broadly including via NIM-served models) require a 'parameters' object expressed as JSON Schema, defining argument names, types, and required fields, so the model can generate valid structured calls.

**Why the others are wrong:**
- 'description' helps the model decide when to use the tool but does not define its input structure.
- Putting argument info only in a prompt comment is unstructured and unreliable for the model to produce valid JSON arguments.
- Temperature controls output randomness and has no bearing on parameter structure.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** How does Retrieval-Augmented Generation (RAG) function as an 'agentic' pattern rather than a purely static pipeline?

A) The agent decides, at reasoning time, whether and what to retrieve by invoking a retrieval tool before generating the final answer
B) The entire knowledge base is always concatenated into every prompt regardless of relevance
C) RAG replaces the need for any LLM reasoning since retrieval alone produces the answer
D) RAG only works with fine-tuned models and cannot be combined with tool use

<details>
<summary>Answer</summary>

**Correct: A**

In the agentic framing, retrieval is treated as a callable tool the agent decides to invoke based on reasoning (e.g., 'I need more context') rather than always being statically injected, making RAG one instance of tool use within a planning loop.

**Why the others are wrong:**
- Always concatenating the full knowledge base is a static/non-agentic pattern and is also impractical at scale.
- RAG supplies context for generation; the LLM still performs reasoning and synthesis over retrieved content.
- RAG is independent of fine-tuning and is commonly combined with other tool calls in agent workflows.

</details>

---

