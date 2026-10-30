# Answer Key — Practice Test 2

**Q1. Correct: A**

When the task is a single lookup-and-answer with no decision points, branching, or tool orchestration, a single grounded model call is faster, cheaper, and equally accurate — agentic overhead adds latency and cost without benefit.

---

**Q2. Correct: A**

NeMo Guardrails is NVIDIA's dedicated toolkit for adding programmable rails (topical, safety, and jailbreak/injection protections) around LLM and agent pipelines, enforcing exactly this kind of behavioral boundary.

---

**Q3. Correct: B**

Function/tool calling relies on a structured JSON schema (name, description, parameter types) so the model can generate a valid, parseable call with correctly typed arguments.

---

**Q4. Correct: A**

Multi-agent orchestration loops must include explicit stopping conditions and failure-handling logic (iteration caps, replanning, escalation) to prevent infinite retry loops when a sub-task repeatedly fails.

---

**Q5. Correct: B**

Agentic RAG embeds retrieval inside an agent's reasoning loop, allowing dynamic, iterative, or conditional retrieval decisions instead of the single fixed retrieval pass used in standard RAG.

---

**Q6. Correct: B**

Robust agent memory design combines in-context short-term memory for the active conversation with an external persistent store (e.g., vector DB) for long-term recall across sessions, retrieved on demand.

---

**Q7. Correct: D**

The task requires real actions (refund execution, live order lookup) which only tool/function calling can perform, plus a planning loop to select the right tool and memory to persist state across the multi-step session — the defining traits of an agentic workflow.

---

**Q8. Correct: A**

Each hand-off in a multi-agent chain can independently introduce unsafe content, tool misuse, or topic drift (e.g., a sub-agent calling an inappropriate tool or returning off-policy text), so layered, defense-in-depth guardrails at every boundary are needed to reliably contain risk before it propagates further downstream.

---

**Q9. Correct: D**

MinHash LSH approximates Jaccard similarity between documents and scales to billions of documents, making it the standard GPU-accelerated technique in NeMo Curator for catching near-duplicates that exact hashing misses.

---

**Q10. Correct: A**

NeMo Retriever provides prebuilt embedding and reranking NIM microservices specifically designed for RAG semantic search with a standard API.

---

**Q11. Correct: D**

IVF-PQ partitions the vector space into clusters and compresses vectors via product quantization, drastically reducing memory and search time at scale while accepting a controlled recall tradeoff — the standard choice for billion-scale ANN search in GPU vector databases.

---

**Q12. Correct: C**

The data flywheel is a closed loop: production data and feedback are captured, curated, and used to continuously fine-tune and redeploy the model, so the system improves as it is used.

---

**Q13. Correct: D**

Training heavily on synthetic data without curation and grounding against real examples risks model collapse, where the model amplifies synthetic artifacts and biases instead of generalizing to real-world distributions.

---

**Q14. Correct: B**

Data governance for regulated domains requires detecting and redacting or anonymizing protected health information before the data is used for training, to comply with privacy regulations and avoid leaking sensitive data into the model.

---

**Q15. Correct: C**

The data flywheel pattern NVIDIA promotes (e.g., the NeMo data flywheel blueprint) is a closed loop: production traffic and feedback are curated, used to fine-tune/distill a smaller candidate model, the candidate is evaluated against the larger model on live or held-out data, and only promoted if it meets accuracy/quality bars. This cycle repeats as more data accumulates, continuously improving cost/accuracy trade-offs.

---

**Q16. Correct: B**

Embeddings from different models (and different dimensionalities) occupy different vector spaces and are not directly comparable via similarity search. Switching embedding models requires re-embedding and re-indexing the full corpus so all vectors are consistent and comparable in the new model's vector space.

---

**Q17. Correct: A**

KV cache grows linearly with sequence length and can fragment GPU memory over long contexts. Paged/chunked KV cache management (e.g., PagedAttention-style allocation used in TensorRT-LLM) allocates memory in fixed-size blocks on demand, eliminating fragmentation and OOM errors for long-context workloads.

---

**Q18. Correct: A**

Continuous (in-flight) batching dynamically admits new requests and removes finished sequences on a per-iteration basis, which is specifically designed for variable-length LLM generation and maximizes GPU utilization without the idle time static batching introduces.

---

**Q19. Correct: A**

The dynamic_batching block in a Triton model config enables automatic batching of incoming requests, and max_queue_delay_microseconds controls how long Triton waits to form a larger batch before dispatching, directly trading a small latency increase for higher throughput.

---

**Q20. Correct: C**

Latency and throughput are often in tension: larger batches increase GPU utilization and total throughput but add queuing delay that raises per-request latency. Understanding this tradeoff is core to configuring inference servers for production SLAs.

---

**Q21. Correct: A**

INT4 quantization compresses weights to 4 bits, giving the smallest memory footprint and fastest inference among common options, at the cost of some accuracy — exactly matching a severely VRAM-constrained edge scenario where a few percent accuracy loss is acceptable.

---

**Q22. Correct: C**

NVIDIA NIM (NVIDIA Inference Microservices) packages pre-optimized models (using TensorRT-LLM/Triton under the hood) with standardized APIs in containers, letting teams deploy production inference endpoints in minutes without building custom serving infrastructure.

---

**Q23. Correct: C**

The KV cache, not raw compute, is the limiting resource here — each active sequence holds a growing cache of key/value tensors for every generated token. Paged KV cache allocation (as used in TensorRT-LLM/Triton in-flight batching) breaks the cache into fixed-size blocks that are assigned on demand and freed immediately when a sequence finishes, eliminating memory fragmentation from over-reserving for worst-case sequence length. Combined with continuous batching, new requests can be slotted in as soon as memory frees up instead of waiting for a whole batch to complete, which raises throughput within the same memory budget.

---

**Q24. Correct: C**

LoRA/PEFT can reliably adapt output behavior and formatting with a small labeled dataset and limited compute, updating only a small set of adapter weights.

---

**Q25. Correct: A**

DPO reformulates the RLHF objective into a single supervised-style loss computed directly on preference pairs, removing the need for a separate reward model and the PPO reinforcement learning loop.

---

**Q26. Correct: D**

Rank controls the size of the low-rank adapter matrices; a higher rank increases trainable parameters and adaptation capacity, at the cost of more compute/memory and a higher chance of overfitting on small datasets.

---

**Q27. Correct: C**

PEFT methods like LoRA freeze the base model weights and train only small adapter layers, which limits catastrophic forgetting of general capabilities while adapting to the clinical domain within a limited compute budget.

---

**Q28. Correct: B**

RAG decouples factual knowledge updates from the model's weights by retrieving current information from an updated index at query time, keeping answers fresh without any retraining and with low added latency.

---

**Q29. Correct: D**

QLoRA quantizes the frozen base model weights (commonly to 4-bit NF4) to drastically reduce memory footprint, while the LoRA adapters remain trained in higher precision (e.g., bfloat16) to preserve gradient quality during fine-tuning.

---

**Q30. Correct: B**

Embedding models are purpose-built to map text (or other modalities) into fixed-length dense vectors that preserve semantic similarity, which is exactly what's needed for nearest-neighbor retrieval in RAG systems.

---

**Q31. Correct: C**

Diffusion models generate content by starting from random noise and iteratively denoising it over multiple steps, guided by a text prompt, to produce a final photorealistic image. This iterative denoising process is the defining characteristic described in the scenario.

---

**Q32. Correct: D**

A multimodal vision-language model can jointly process image input (the chart) and text input (the question) and generate a coherent text response, which is exactly the capability this scenario requires.

---

**Q33. Correct: B**

Open-weight models can be downloaded and deployed entirely within the company's own infrastructure, satisfying data residency requirements, and their weights can be directly fine-tuned on proprietary data since the full model is accessible.

---

**Q34. Correct: D**

Self-attention computes a weighted relevance score between every pair of tokens in the input sequence simultaneously, enabling the model to directly capture long-range dependencies without the sequential bottleneck of earlier architectures.

---

**Q35. Correct: A**

NIM microservices package a foundation model like Llama 3 70B as a prebuilt, optimized (TensorRT-LLM) container exposing a standard OpenAI-compatible API, requiring no custom inference engineering from the consuming team.

---

**Q36. Correct: C**

NeMo provides the end-to-end tooling for model customization, including SFT, LoRA/PEFT, and alignment techniques like RLHF and DPO, before the resulting model is exported for serving.

---

**Q37. Correct: B**

NVIDIA Blueprints are prepackaged, end-to-end reference workflows (e.g., for RAG chatbots) that wire together NIM microservices, vector databases, and orchestration logic so teams can customize rather than build from scratch.

---

**Q38. Correct: B**

NIM's standard setup requires exporting NGC_API_KEY, which is then used both for `docker login nvcr.io -u '$oauthtoken' -p $NGC_API_KEY` and for the container to download the optimized model artifacts at runtime.

---

**Q39. Correct: C**

Blueprints exist to accelerate development by providing pre-architected, customizable application patterns (e.g., RAG chatbot, digital human) that combine NIM microservices with orchestration and supporting services.

---

**Q40. Correct: C**

70B params x 2 bytes (FP16) = 140GB of weight memory. Two A100 80GB GPUs provide 160GB combined, and tensor parallelism shards the weights across them so each GPU only needs ~70GB.

---

**Q41. Correct: B**

Required capacity = requests/sec x latency per request = 500 x 0.15s = 75 concurrent 'slots', so 75 GPU instances are the minimum needed to sustain the load.

---

**Q42. Correct: D**

The frozen base weights alone require ~26GB (13B x 2 bytes FP16), plus activation and LoRA adapter overhead. An L40S with 48GB comfortably fits this with headroom, at a much lower cost than a data-center flagship GPU — matching the stated budget constraint.

---

**Q43. Correct: D**

200GB divided across GPUs must leave each shard at or below 80GB. 200/2=100GB (too much), but 200/3≈66.7GB fits within 80GB per GPU, so 3 is the minimum valid degree.

---

**Q44. Correct: A**

The KV cache stores key/value tensors per token, per layer, per request. Its memory footprint scales directly with how many tokens are cached (sequence length) and how many requests are processed concurrently (batch size).

---

**Q45. Correct: D**

Isaac Sim combined with Omniverse Replicator is purpose-built for generating large-scale, physically accurate synthetic datasets with randomized lighting, textures, and object placement, which directly reduces the sim-to-real gap for perception models.

---

**Q46. Correct: C**

A digital twin is defined by its ongoing live synchronization with a physical asset's real-world state, distinguishing it from a generic simulation that models behavior independently without a persistent real-time data link.

---

**Q47. Correct: B**

NVIDIA Jetson provides low-power, high-performance edge compute, and Isaac ROS supplies hardware-accelerated robotics perception and navigation packages, together enabling real-time, offline inference directly on the robot.

---

