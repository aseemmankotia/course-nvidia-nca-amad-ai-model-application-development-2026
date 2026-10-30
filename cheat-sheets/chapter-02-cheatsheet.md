# Chapter 2 Cheat Sheet: Agentic AI

## Agent vs Single Model Call
| Use Single Call | Use Agent |
|---|---|
| One-step task | Multi-step task |
| No external data needed | Needs live data/tools |
| Latency-critical | Can tolerate loop overhead |
| Fixed, known answer format | Requires planning/decisions |

**Exam note:** Default bias should be toward the simplest solution — agents are chosen only when justified by tool use or multi-step reasoning.

## ReAct Loop
```
Thought -> Action (tool/function call) -> Observation -> (repeat) -> Final Answer
```
**Common mistake:** Ordering Action before Thought, or assuming the loop terminates after one Action.

## Function Calling Schema (core fields)
| Field | Purpose |
|---|---|
| name | Identifies the function |
| description | Tells model WHEN to use it |
| parameters | JSON Schema defining args/types (REQUIRED) |

Model output = structured JSON call, not free text or executed code. The application layer executes the function and returns the Observation.

## Agent Memory
| Type | Scope | Storage | Use Case |
|---|---|---|---|
| Short-term | Current session | Context window / scratchpad | Track in-conversation facts |
| Long-term | Across sessions | Vector DB / knowledge store | User preferences, history recall |

**Common mistake:** Using a vector DB for data that only needs to live for one session — unnecessary complexity.

## RAG as Agentic Pattern
RAG = retrieval treated as a callable tool invoked when the agent's reasoning determines more context is needed — not static full-document stuffing into every prompt.

## Guardrails
NeMo Guardrails = programmable rails for topic control, safety, and jailbreak/prompt-injection resistance in conversational/agentic systems. Distinct from prompt engineering alone.

## NVIDIA Agentic Stack
| Component | Role |
|---|---|
| NIM | Containerized, optimized inference microservice, standard API |
| NeMo (Guardrails/Retriever/Customizer) | Guardrails, retrieval embeddings/reranking, fine-tuning |
| AI Blueprints | Reference end-to-end workflow templates for agentic apps |

**Exam note:** Know the ROLE separation — NIM serves, NeMo components secure/customize/retrieve, Blueprints provide the reference architecture.

## Multi-Agent Orchestration
Planner/orchestrator agent decomposes a task and delegates to specialized sub-agents (retriever, executor, verifier), then aggregates results.

**Common mistake:** Choosing multi-agent orchestration for tasks solvable by a single tool call — adds unjustified latency/cost.
