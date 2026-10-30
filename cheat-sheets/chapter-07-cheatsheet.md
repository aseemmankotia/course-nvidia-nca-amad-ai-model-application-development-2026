## Chapter 7 Cheat Sheet: The NVIDIA AI Stack

### Component Roles (know this table cold)
| Component | Role | Lifecycle Stage | Exam Keyword |
|---|---|---|---|
| **NVIDIA AI Enterprise** | Supported, secure software platform layer | Underpins everything | "support," "security patching," "certification" |
| **NIM** | Packaged, optimized inference microservices | Deployment/Inference | "containerized," "OpenAI-compatible API," "deploy fast" |
| **NeMo** | Build, customize, align models | Training/Fine-tuning/Alignment | "curate," "fine-tune," "guardrails" |
| **Blueprints** | Reference architectures for GenAI/agentic apps | App-level workflow | "reference workflow," "customize," "RAG chatbot" |
| **RAPIDS** | GPU-accelerated data science | Data prep/ETL | "cuDF," "cuML," "cuGraph" |

### NeMo Sub-Tools
| Sub-tool | Purpose |
|---|---|
| NeMo Curator | Data curation/cleaning for training |
| NeMo Customizer | Fine-tuning foundation models |
| NeMo Evaluator | Model evaluation/benchmarking |
| NeMo Guardrails | Safety/alignment controls |

### NIM Deployment Model
- Delivered as a **container** (Docker) — deploy on cloud, on-prem, or workstation GPUs.
- Built on **Triton Inference Server + TensorRT/TensorRT-LLM** under the hood (abstracted away).
- Exposes **standard REST/gRPC APIs**, often **OpenAI-compatible**, for drop-in integration.
- Goal: minimize custom inference engineering — "pull and run."

### Mapping Requirements → Component (exam pattern)
| Requirement in Scenario | Correct Component |
|---|---|
| "Deploy a model fast with minimal code" | NIM |
| "Fine-tune/align on our own data" | NeMo |
| "Need a full reference app (RAG, agent, digital human)" | Blueprint |
| "Accelerate dataframe/ML preprocessing" | RAPIDS |
| "Need enterprise SLA, patching, certification" | AI Enterprise |

### Typical Pipeline Order
RAPIDS (data prep) → NeMo (train/customize/align) → NIM (serve/infer) — all running on/under NVIDIA AI Enterprise for support, with Blueprints as the app-level template tying components together.

### Common Traps
- Confusing **NIM (serve)** with **NeMo (train)** — most frequently missed distinction.
- Thinking **AI Enterprise** is a product/model — it's the support/certification *platform layer*, not a deployable app.
- Assuming **Blueprints** are runtime services — they are *reference designs/templates* to customize, not components you "install" like NIM.
- Forgetting RAPIDS is about **data science acceleration**, not LLM inference or training alignment.
