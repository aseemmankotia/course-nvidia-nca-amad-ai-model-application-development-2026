# Answer Key — Practice Test 1

**Q1. Correct: B**

This requires live external data retrieval, comparison across multiple sources, and reasoning before synthesis — the exact scenario where an agentic workflow with tool calling is needed instead of a single model call.

---

**Q2. Correct: C**

NeMo Guardrails provides programmable rails (topical, safety, jailbreak) specifically designed to constrain conversational AI behavior.

---

**Q3. Correct: B**

Tool use/function calling is the model producing a structured call to an external function or API and incorporating the returned result into its reasoning or response.

---

**Q4. Correct: A**

Setting a max iteration limit is the standard safeguard in agent frameworks to prevent infinite reasoning/tool-call loops and force a final response.

---

**Q5. Correct: B**

Distinct specialized roles with iterative critique and revision map directly to a multi-agent orchestration pattern, where each agent handles one responsibility and an orchestrator coordinates handoffs.

---

**Q6. Correct: C**

This is the agentic RAG pattern: the agent decides at runtime whether retrieval is necessary and conditionally calls a retrieval tool, optimizing cost/latency while still handling knowledge-base-specific queries correctly.

---

**Q7. Correct: B**

NVIDIA frames agentic patterns as appropriate when a task needs multi-step reasoning, tool use, or iterative planning. A single factual lookup from a static document is a one-shot retrieval-augmented generation task — one retrieval plus one inference call is sufficient and avoids unnecessary latency and complexity.

---

**Q8. Correct: A**

NVIDIA NIM microservices expose an OpenAI API-compatible endpoint, including support for structured function/tool calling via a tool_calls field, allowing agent frameworks (e.g., LangChain) to integrate without custom parsing logic.

---

**Q9. Correct: A**

The data flywheel concept is defined by a continuous loop: production usage generates data, that data is curated and used to improve the model, and the improved model generates better production data — compounding value over time.

---

**Q10. Correct: D**

Embedding microservices packaged as NIMs are purpose-built to take text input and return dense vector embeddings, which is exactly what's needed to populate a vector store for RAG retrieval.

---

**Q11. Correct: D**

Chunks that are too large can exceed the embedding model's context window or dilute semantic focus, while chunks that are too small can lose context; the correct strategy balances coherence with the model's input limits.

---

**Q12. Correct: C**

Synthetic data is generated to fill gaps in real datasets — covering rare scenarios, balancing class distributions, or substituting for data that is hard to collect due to privacy or scarcity — improving model robustness.

---

**Q13. Correct: D**

Deduplication removes redundant or near-identical documents, which reduces the model's tendency to memorize repeated content verbatim and avoids spending compute cycles training on the same data multiple times.

---

**Q14. Correct: B**

A responsible flywheel requires a governance layer that validates and filters feedback (removing noise, abuse, or low-quality signals) before it is used to retrain or fine-tune models, protecting model quality and safety.

---

**Q15. Correct: C**

Vector databases are purpose-built to store high-dimensional embeddings and perform fast approximate nearest neighbor (ANN) search, which is exactly what's needed to retrieve semantically similar chunks at scale with low latency for RAG.

---

**Q16. Correct: C**

The data flywheel describes the continuous cycle where production usage data and feedback are captured, curated, and fed back into training/fine-tuning pipelines, driving progressively better models that in turn attract more usage and more data.

---

**Q17. Correct: C**

Dynamic batching with a small max batch size and short delay allows some throughput benefit from batching while keeping per-request latency low enough to meet the 200ms SLA.

---

**Q18. Correct: A**

NVIDIA NIM packages an optimized inference engine with a standardized, OpenAI-compatible API and container-based deployment, minimizing custom integration effort.

---

**Q19. Correct: C**

The KV cache stores the Key and Value attention tensors for all previously processed tokens so they don't need to be recomputed for each new generated token, significantly speeding up autoregressive decoding.

---

**Q20. Correct: A**

INT8 quantization substantially reduces model memory footprint and compute requirements, making it well suited for memory-constrained edge devices, at the cost of a small, generally acceptable accuracy loss.

---

**Q21. Correct: C**

Dynamic batching is the Triton Inference Server feature that groups individual incoming requests into batches on the fly to improve GPU utilization and throughput.

---

**Q22. Correct: D**

Training involves both forward passes and backward passes (backpropagation) to compute gradients and update weights, while inference only performs a forward pass to produce predictions from a fixed, already-trained model.

---

**Q23. Correct: B**

During autoregressive generation, the model caches the key and value tensors from the attention mechanism for every previously processed token so they don't need to be recomputed at each new step. This KV cache grows linearly with sequence length and multiplies with batch size, making it a major consumer of GPU memory during long-context or high-concurrency inference, independent of the fixed size of the model weights.

---

**Q24. Correct: A**

RAG decouples knowledge freshness from model weights by retrieving current documents at query time, so updating the index (not the model) keeps answers current with near-zero retraining cost.

---

**Q25. Correct: B**

LoRA/PEFT freezes the base model and trains small low-rank adapter matrices, drastically reducing GPU memory and compute needs while still durably encoding style/format behavior from a modest dataset — ideal for single-GPU budgets.

---

**Q26. Correct: A**

Instruction tuning with PEFT directly teaches the model the desired input-output format using the available labeled examples at low compute cost, which is the standard approach for reliable structured output.

---

**Q27. Correct: C**

LoRA inserts low-rank matrices of dimension r into frozen weight layers; a higher r increases trainable parameters and expressive capacity but costs more memory/compute, while a lower r is cheaper but may underfit complex adaptations.

---

**Q28. Correct: B**

DPO reformulates preference alignment as a direct supervised-style loss over chosen/rejected response pairs, skipping the reward-model training and RL rollout steps that RLHF requires, simplifying the pipeline while targeting the same alignment goal.

---

**Q29. Correct: A**

When the required capability doesn't exist in any foundation model and the organization has the data scale and compute budget, full pretraining/training is the appropriate (and only) path to instill fundamentally new reasoning abilities, as opposed to surface-level adaptation.

---

**Q30. Correct: D**

Embedding models are purpose-built to convert text into dense vector representations that capture semantic meaning, enabling similarity search (e.g., cosine similarity) against a vector database — exactly what semantic search requires.

---

**Q31. Correct: C**

Diffusion models are generative vision models trained to synthesize new images from text prompts by progressively denoising random noise, making them the standard model type for text-to-image generation tasks.

---

**Q32. Correct: B**

Multimodal (vision-language) models are trained to jointly process image and text inputs, enabling tasks like visual question answering where the model must reason over both an image and an accompanying text prompt.

---

**Q33. Correct: A**

Self-attention computes relevance scores between every pair of tokens in the input, letting the model capture long-range dependencies and context regardless of token distance — this is the key innovation that differentiates transformers from earlier sequential architectures.

---

**Q34. Correct: C**

Open-weight models provide downloadable model parameters that can be hosted, fine-tuned, and run on self-managed infrastructure, satisfying the requirement to keep data and inference entirely on-premises.

---

**Q35. Correct: D**

NIM microservices are prebuilt, containerized inference endpoints (built on Triton/TensorRT-LLM) that expose a standard API and run consistently across cloud, data center, and workstation with minimal setup — exactly the 'minimal customization, portable, optimized inference' use case.

---

**Q36. Correct: D**

NeMo Curator is the NeMo framework component purpose-built for large-scale data curation — deduplication, filtering, quality scoring, and PII removal — before fine-tuning or pretraining models.

---

**Q37. Correct: C**

NVIDIA Blueprints are reference workflows that provide pre-architected, customizable reference implementations (like RAG chatbots) combining NIM microservices, vector databases, and orchestration — the fastest path to a proven starting architecture.

---

**Q38. Correct: A**

NIM microservices for LLMs expose an OpenAI-compatible REST API by default, allowing applications already built against OpenAI-style endpoints to switch to a self-hosted NIM with little to no code change.

---

**Q39. Correct: D**

NVIDIA AI Enterprise is the overarching, licensed software layer that packages NIM, NeMo, and other AI tools with enterprise support, security patching, and certification for deployment across cloud, data center, and edge environments.

---

**Q40. Correct: D**

13B params x 2 bytes (FP16) = 26 GB for weights alone. Adding ~20% overhead for KV cache and activations brings the requirement to roughly 31 GB, which exceeds 24 GB but fits comfortably within a 40 GB GPU.

---

**Q41. Correct: A**

Large-scale distributed training requires high-bandwidth, low-latency communication both within a node (NVLink/NVSwitch for GPU-to-GPU) and across nodes (InfiniBand), which minimizes the communication overhead that dominates training time at scale.

---

**Q42. Correct: B**

TensorRT provides post-training quantization with INT8 calibration, converting FP32 weights to lower precision to reduce memory usage and increase inference throughput while controlling accuracy loss.

---

**Q43. Correct: A**

Full fine-tuning requires storing gradients and optimizer states (e.g., momentum and variance for Adam) in addition to the model weights, often multiplying per-parameter memory requirements by 3-4x compared to inference-only memory needs.

---

**Q44. Correct: B**

Triton Inference Server with dynamic batching improves GPU utilization per request, and pairing it with autoscaling behind a load balancer allows capacity to scale up during spikes and back down during normal traffic, balancing performance and cost.

---

**Q45. Correct: B**

Isaac Sim is NVIDIA's robotics simulation application, built on Omniverse, purpose-built for training and testing robot policies in photorealistic, physically accurate virtual environments, including synthetic data generation with domain randomization for sim-to-real transfer.

---

**Q46. Correct: D**

NVIDIA Omniverse is a platform built around the OpenUSD framework for creating and connecting physically accurate 3D simulations and digital twins, serving as the underlying foundation for tools like Isaac Sim.

---

**Q47. Correct: D**

Physical AI refers to AI systems embedded in robots or autonomous machines that perceive their surroundings through sensors, reason about the environment, and act on the physical world, as opposed to AI that only operates on digital data like text or images in isolation.

---

