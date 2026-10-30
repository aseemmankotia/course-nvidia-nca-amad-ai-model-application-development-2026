## NCA-AMAD Chapter 1 Cheat Sheet: Exam Blueprint & Lifecycle

### Exam Logistics
| Item | Detail |
|---|---|
| Format | Multiple-choice only, no live hands-on lab during the exam |
| Questions | 50-60 |
| Duration | 60 minutes (~1 min/question budget) |
| Delivery | Online, remote-proctored via Certiverse |
| ID check | Government photo ID + webcam/room scan required |
| Validity | 2 years from pass date |
| Recert | Must retake current exam version — no fee-only renewal, no auto-reactivation |

**Exam note:** Hands-on labs are for *preparation*, not scored during the actual test — don't confuse training labs with exam content.

### AI Application Lifecycle — 4 Stages
| Stage | Purpose | Typical NVIDIA Tools |
|---|---|---|
| Train | Build foundational model weights from raw data | TAO Toolkit (vision), large-scale pretraining frameworks |
| Customize | Adapt an existing pretrained model to a task/domain | NeMo Customizer, LoRA/PEFT, prompt-tuning |
| Serve | Deploy model as a callable, optimized inference endpoint | NVIDIA NIM, Triton Inference Server, TensorRT-LLM |
| Consume | Build end-user application calling the served endpoint | RAG pipelines, agent frameworks, NVIDIA AI Blueprints |

**Memory trick:** Train → Customize → Serve → Consume = "build weights → adapt weights → host it → use it."

**Common mistake:** Students confuse Serve (hosting the endpoint) with Consume (calling the endpoint from an app). If the scenario mentions deploying infrastructure → Serve. If it mentions writing app/prompt logic that calls an existing endpoint → Consume.

### Tool Quick-Pick
| Need | Pick |
|---|---|
| Fine-tune an LLM with adapters | NeMo Customizer |
| Transfer learning for a vision model | TAO Toolkit |
| Fast, prepackaged model inference deployment | NVIDIA NIM |
| Flexible multi-framework model serving | Triton Inference Server |
| Maximize inference speed for a trained LLM | TensorRT-LLM |

### Study Strategy
- Allocate study hours **proportional to each domain's published weight** in the official exam guide — don't split evenly across domains.
- Treat this orientation chapter as a map: every later chapter content maps back to one of the four lifecycle stages above.
- Exam note: expect scenario questions that describe a task and ask you to identify *which lifecycle stage* and/or *which NVIDIA tool* applies — practice this mapping until it's automatic.

**Common mistake:** Assuming Train is the most-tested stage because it sounds foundational — most application-developer-focused exam questions actually center on Customize, Serve, and Consume, since that's where app developers operate day-to-day.
