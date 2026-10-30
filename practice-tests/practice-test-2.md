# Practice Test 2: NCA-AMAD: NVIDIA AI Model & App Dev Exam Prep

- **Questions:** 47
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-2.md`. Track results in `score-tracker.md`.

---

**Q1.** A customer support application needs to answer a single factual question about a product's return policy, retrieved from a static FAQ document. No multi-step reasoning, tool use, or external computation is required. Which approach is MOST appropriate?

A) Use a single NIM-hosted model call with the relevant FAQ passage injected as context (simple RAG, no agent loop)
B) Deploy a multi-agent orchestration system with a planner and researcher agent
C) Build a full agentic workflow with a reasoning loop and tool-calling
D) Use an agent with long-term memory and iterative self-reflection

---

**Q2.** A developer is building an agentic customer-facing chatbot that must refuse to discuss competitor pricing and must resist prompt-injection attempts embedded in retrieved documents. Which NVIDIA component should be integrated into the agent pipeline to enforce these behavioral constraints?

A) NeMo Guardrails
B) TensorRT-LLM
C) A NIM microservice for text embeddings
D) NeMo Customizer

---

**Q3.** When defining a tool for an LLM-based agent to call a weather API via function calling, which element is REQUIRED for the model to reliably decide when and how to invoke the tool correctly?

A) Fine-tuned model weights specific to the weather domain
B) A JSON schema specifying the function name, description, and typed parameters
C) A hardcoded API key embedded directly in the system prompt
D) A natural-language-only description of the tool with no parameter schema

---

**Q4.** In a multi-agent system where a 'planner' agent delegates sub-tasks to 'researcher' and 'coder' agents, the system enters an infinite loop because the planner keeps re-assigning the same failed sub-task without modification. Which design element is MISSING?

A) A termination/convergence mechanism with failure handling (e.g., max iteration limit and replanning on repeated failure)
B) A larger context window for the planner agent
C) Switching the entire system to a single model call
D) Adding more specialized agents to the orchestration

---

**Q5.** How does 'agentic RAG' differ from standard retrieve-then-generate RAG in NVIDIA's reference architectures?

A) Agentic RAG only functions when paired with NeMo Guardrails and cannot run without it
B) Agentic RAG uses an LLM-driven reasoning loop to decide whether, when, and how to retrieve — potentially issuing multiple or reformulated queries — rather than performing a single fixed retrieve-then-generate step
C) Agentic RAG replaces the vector database with a relational database
D) There is no meaningful difference between the two approaches

---

**Q6.** An agent handling multi-turn customer support conversations must recall details mentioned earlier in the SAME conversation (e.g., an order number) as well as details from the customer's PAST sessions from weeks ago. Which memory design addresses both requirements?

A) Only a vector-database-backed long-term memory store, with no conversational context window usage
B) Short-term memory within the context window combined with a persistent, retrievable long-term memory store
C) No memory architecture is needed if function calling is used
D) Only short-term memory within the model's context window

---

**Q7.** A team is building a customer support system that must look up real order statuses, issue refunds through an internal API, and remember details across a multi-turn conversation within the same session. Which architecture BEST meets these requirements?

A) Deploy a single large-context LLM call that includes the entire conversation history in each prompt, relying on the model's reasoning alone to decide when to issue a refund
B) Implement a RAG pipeline that retrieves order-status documents and feeds them to the model as context for every user turn
C) Chain multiple independent single-turn LLM calls, each stateless and unaware of prior turns, to handle different parts of the conversation
D) Build an agent with function-calling tools for order lookup and refund APIs, a reasoning/planning loop to decide which tool to call, and a memory module to persist session state across turns

---

**Q8.** A multi-agent orchestration pipeline uses an orchestrator that delegates to several specialized sub-agents (each backed by a NIM microservice) before synthesizing a final response. Where should NeMo Guardrails-style input/output checks be applied to reliably prevent unsafe or off-topic content from propagating through the pipeline?

A) Apply guardrail checks at every agent boundary — orchestrator input, each sub-agent's input/output, and the final synthesized response — so unsafe or off-topic content is caught at every hand-off
B) Apply guardrail checks only within the RAG retrieval step, since that is the only place external content enters the system
C) Apply guardrail checks only at the orchestrator's initial entry point, before any sub-agent is invoked, since validating the first message is sufficient
D) Apply guardrail checks only at the final aggregator agent, after all sub-agent outputs have been synthesized into one response

---

**Q9.** A team uses NVIDIA NeMo Curator to prepare a 50TB web-crawled text corpus for LLM pretraining. They need to remove near-duplicate documents that differ only slightly (e.g., boilerplate headers or minor edits) without relying on exact byte-for-byte matching. Which technique BEST accomplishes this at scale?

A) Randomly sampling and discarding documents smaller than 1KB
B) Running a quality classifier and discarding documents with low predicted scores
C) Exact-match deduplication using SHA-256 hashes of full documents
D) Fuzzy deduplication using MinHash with Locality-Sensitive Hashing (LSH) to cluster near-duplicate documents

---

**Q10.** A developer building a RAG application needs to convert document chunks into dense vector representations for semantic search and wants to deploy the embedding model as a scalable, OpenAI-API-compatible microservice. Which NVIDIA offering is purpose-built for this?

A) NVIDIA NeMo Retriever embedding NIM
B) NVIDIA Riva automatic speech recognition (ASR) NIM
C) NVIDIA TensorRT-LLM compiler and runtime
D) NVIDIA Morpheus cybersecurity pipeline

---

**Q11.** A team stores 2 billion document embeddings in a GPU-accelerated vector database and must perform approximate nearest-neighbor search with the best balance of query latency and memory footprint, accepting a small recall tradeoff. Which index type should they configure?

A) A flat (brute-force) exact-search index
B) A single hash-table exact-match index
C) A B-tree index built on embedding ID
D) An IVF-PQ (Inverted File with Product Quantization) index

---

**Q12.** In NVIDIA's data flywheel concept for AI applications, what is the primary mechanism that drives continuous model improvement over time?

A) Periodically retraining the base model from scratch using only the original pretraining corpus
B) Increasing GPU cluster size to reduce inference latency
C) Capturing production inference data, user feedback, and edge cases, then curating this into new fine-tuning datasets that feed back into model updates
D) Swapping to a newer, larger foundation model whenever one is released

---

**Q13.** A team has only 200 labeled examples of a rare defect class for a visual inspection model and plans to use NVIDIA Nemotron-generated synthetic data to augment training. What is the PRIMARY risk they must guard against when relying heavily on uncurated synthetic data?

A) Synthetic data generation is too slow to be useful at any practical scale
B) Synthetic data cannot be indexed or stored in a vector database
C) GPU drivers must be reinstalled before synthetic data can be generated
D) Model collapse / distribution drift, where the model overfits to synthetic artifacts and loses accuracy on real-world data

---

**Q14.** A healthcare AI company is curating a dataset of patient chat transcripts to fine-tune a customer-support LLM and must comply with data privacy regulations. Which step is MOST critical to include in the data pipeline BEFORE the data is used for fine-tuning?

A) Converting all transcripts into a single JSONL file for faster I/O
B) Applying PII/PHI detection and redaction or anonymization to remove protected health information
C) Increasing the batch size used during fine-tuning
D) Translating all transcripts into English for consistency

---

**Q15.** A company has deployed a large general-purpose LLM in production for customer support. Over several months they log user queries, model responses, and corrections made by human support agents when the model's answer was wrong. The team wants to apply the NVIDIA data flywheel concept to produce a smaller, cheaper model that matches the large model's accuracy on this specific support task. Which approach correctly implements the data flywheel here?

A) Discard the production logs because they were not collected for training purposes and risk introducing bias into any future model
B) Use the data flywheel exclusively to generate synthetic conversations and ignore the real production logs entirely
C) Continuously curate and filter the logged interactions and corrections, use them to fine-tune or distill a smaller candidate model, evaluate the candidate against the large model's outputs, and promote it to production only if it meets accuracy targets
D) Immediately replace the large model with a rules-based system since production logs are inherently too noisy to use for training

---

**Q16.** A RAG pipeline currently stores document embeddings generated by an embedding model that outputs 1024-dimensional vectors in a vector database. The team switches to a newer embedding model that outputs 4096-dimensional vectors to improve retrieval quality. What must they do to the existing vector store before the new model can be used effectively for retrieval?

A) Simply raise the vector index's dimension setting and let the old 1024-dimensional vectors coexist with the new 4096-dimensional ones in the same index
B) Re-embed all previously ingested documents using the new model and re-index them, since vectors produced by different embedding models or with different dimensionality are not compatible for similarity search
C) Average each old 1024-dimension vector with a new query's 4096-dimension vector to produce a compatible 2560-dimension comparison on the fly
D) Leave the old vectors untouched since cosine similarity search automatically normalizes differences in embedding dimensionality

---

**Q17.** A team deploys an LLM chatbot that supports long conversation histories (8K+ tokens). Despite using a small batch size, the GPU repeatedly runs out of memory mid-conversation as context grows. Which optimization BEST addresses this specific problem?

A) Enable paged/chunked KV cache management in the inference backend
B) Increase the batch size to amortize memory overhead per request
C) Switch model weights from FP16 to FP32 for numerical stability
D) Enable MIG to partition the GPU into isolated smaller instances

---

**Q18.** An inference service receives a continuous stream of LLM requests with highly variable output lengths. The team wants to maximize GPU utilization and throughput without forcing new requests to wait for an entire batch to finish before starting. Which technique BEST fits this requirement?

A) Continuous (in-flight) batching, which allows new requests to join a running batch and completed sequences to exit immediately
B) Static batching, where all requests in a batch must complete before the next batch starts
C) Single-request sequential processing with no batching
D) Pipeline parallelism, which splits the model across multiple GPUs

---

**Q19.** In Triton Inference Server's model configuration file, which setting enables request batching with a configurable wait window for incoming inference requests?

A) dynamic_batching with the max_queue_delay_microseconds parameter, which batches concurrent requests within a configurable wait window
B) instance_group, which sets the number of model instances per GPU
C) sequence_batching, used only for stateful models with implicit state management
D) optimization { execution_accelerators }, which configures hardware-specific execution backends

---

**Q20.** Which statement correctly distinguishes latency optimization from throughput optimization in model inference serving?

A) Latency and throughput scale identically, so improving one always improves the other by the same margin
B) Throughput optimization reduces GPU memory consumption and has no relationship to batch size
C) Latency optimization minimizes response time (or time-to-first-token) for individual requests, while throughput optimization maximizes total requests or tokens processed per unit time, often by increasing batch size
D) Latency optimization only applies to model training workloads, not to inference serving

---

**Q21.** A team must deploy an LLM on an edge device with severely limited VRAM. A few percentage points of accuracy loss are acceptable in exchange for the smallest possible memory footprint and fastest inference. Which precision/quantization choice BEST fits these constraints?

A) INT4 quantization, which gives the largest memory and compute reduction while tolerating a modest accuracy drop
B) FP32, which preserves full precision at the cost of the largest memory footprint
C) FP16, which halves memory versus FP32 but is often still too large for severely constrained edge devices
D) FP8, which is primarily used for training on Hopper-class GPUs and provides no inference-specific memory benefit

---

**Q22.** A development team needs to deploy a pre-optimized, production-ready LLM with a standardized REST/gRPC API, running either on-prem or in the cloud, with minimal custom serving infrastructure to build. Which NVIDIA offering BEST fits this requirement?

A) Building a custom TensorRT engine and writing a bespoke serving layer from scratch
B) A manually configured Triton Inference Server instance with a custom backend written from scratch
C) An NVIDIA NIM microservice, which packages an optimized model with a standardized REST/gRPC API for fast on-prem or cloud deployment
D) A RAPIDS cuDF data processing pipeline

---

**Q23.** A team deploys a 70B-parameter LLM behind NVIDIA Triton Inference Server with the TensorRT-LLM backend for a customer support chatbot. As concurrent user requests increase, GPU memory is exhausted and new requests queue even though GPU compute (SM) utilization stays well below 100%. Which approach BEST resolves this bottleneck while maximizing achievable throughput?

A) Switch all model weights and activations from FP16 to FP32 to improve numerical stability under load
B) Increase the static batch size to a fixed maximum so every batch fully utilizes GPU compute
C) Enable paged KV cache management with continuous (in-flight) batching so memory for the attention cache is allocated and reclaimed per-sequence as requests arrive and finish
D) Reduce the number of attention heads in the deployed model to shrink per-token memory usage

---

**Q24.** A team has 500 labeled examples of input-output pairs where outputs must follow a strict JSON schema. They have access to a single A100 GPU and need the model to reliably produce schema-compliant output within two weeks. Which approach BEST meets these constraints?

A) Full fine-tuning of all model parameters on the 500 examples
B) Prompt engineering alone with few-shot examples in the system prompt
C) LoRA-based instruction fine-tuning on the 500 examples
D) Build a RAG pipeline that retrieves similar JSON examples at inference time

---

**Q25.** Which statement accurately differentiates Direct Preference Optimization (DPO) from classic RLHF in model alignment pipelines?

A) DPO directly optimizes the policy on preference pairs using a closed-form loss, eliminating the separate reward model and RL loop used in RLHF
B) DPO requires training a separate reward model before optimizing the policy, while RLHF does not
C) DPO can only be applied to vision models, while RLHF is exclusive to language models
D) DPO and RLHF are identical techniques with different names for the same training loop

---

**Q26.** In a LoRA configuration, increasing the rank (r) parameter from 8 to 64 primarily results in which trade-off?

A) Reduced trainable parameters and lower adaptation capacity, but faster training
B) No change to trainable parameters since rank only affects the base model
C) The base model weights become fully trainable, converting LoRA into full fine-tuning
D) Increased trainable parameters and higher adaptation capacity, with greater risk of overfitting and higher memory/compute cost

---

**Q27.** A healthcare startup wants to fine-tune a foundation model on proprietary clinical notes while minimizing the risk of the model losing its general reasoning ability (catastrophic forgetting). Compute budget allows only partial retraining. Which technique best addresses this requirement?

A) Full fine-tuning on all clinical notes with a high learning rate
B) Continue pretraining from scratch on a mixed dataset of clinical and general text
C) Parameter-efficient fine-tuning (e.g., LoRA) that freezes base weights and trains small adapter layers
D) Increase the context window and rely purely on in-context learning

---

**Q28.** An application must answer customer questions using product documentation that changes daily (prices, inventory, specs). Latency must stay low and the team cannot retrain the model every day. Which customization strategy BEST fits this requirement?

A) Full fine-tuning the model nightly on the updated documentation
B) Retrieval-Augmented Generation (RAG) that queries an updated vector index of the documentation at inference time
C) LoRA fine-tuning retrained weekly on a snapshot of the documentation
D) RLHF using daily user feedback to steer the model toward recent facts

---

**Q29.** QLoRA enables fine-tuning of large language models on a single consumer or data-center GPU primarily by which mechanism?

A) Converting the entire model to 4-bit precision, including the trainable LoRA adapters, to maximize training speed
B) Removing the attention layers entirely to shrink the parameter count before training
C) Distributing the full-precision model across multiple GPUs using tensor parallelism instead of quantization
D) Quantizing the frozen base model weights to 4-bit precision while keeping LoRA adapter computations in higher precision

---

**Q30.** A company is building a RAG (retrieval-augmented generation) pipeline and needs a model to convert both documents and user queries into dense vector representations for nearest-neighbor similarity search in a vector database. Which model type BEST meets this requirement?

A) Diffusion model
B) Embedding model
C) Autoregressive decoder-only LLM
D) Vision-language multimodal model

---

**Q31.** A marketing team wants to generate photorealistic product images from text prompts, with the generation process built around progressively removing noise from a random starting signal to iteratively refine the output. Which model type are they using?

A) GAN (Generative Adversarial Network)
B) Encoder-only transformer (BERT-style)
C) Diffusion model
D) Embedding model

---

**Q32.** A support tool must accept a screenshot of a chart along with a natural-language question (e.g., 'What was the peak value in Q3?') and return a text answer describing the data shown. Which model type is required?

A) Text-only LLM
B) Embedding model
C) Diffusion model
D) Multimodal vision-language model

---

**Q33.** A healthcare company must keep all patient data on-premises due to strict regulatory data residency requirements, and also needs the ability to fine-tune the model's weights directly on proprietary clinical data. Which approach BEST satisfies these requirements?

A) Use a proprietary model via a cloud API
B) Use an open-weight model deployed on-prem
C) Use a proprietary model with a signed data processing addendum
D) Use an embedding model only

---

**Q34.** Which statement BEST describes the self-attention mechanism used in transformer-based models?

A) It processes tokens sequentially, maintaining and updating a hidden state at each step
B) It applies fixed-size filters that slide over local windows of the input
C) It only considers the most recently generated token when predicting the next token
D) It computes relevance weights between all pairs of tokens in a sequence, allowing the model to capture dependencies regardless of their distance apart

---

**Q35.** A retail company wants to deploy Llama 3 70B in production with an OpenAI-compatible REST API, optimized GPU inference (TensorRT-LLM backend), and automatic scaling, but has no internal MLOps team to build a custom inference stack. Which NVIDIA offering BEST meets this requirement?

A) A prebuilt NIM microservice for Llama 3 70B deployed as a container
B) A NeMo Customizer fine-tuning job configured for SFT
C) A raw TensorRT engine file compiled manually from the Hugging Face checkpoint
D) The NVIDIA RAPIDS Accelerator library for Apache Spark

---

**Q36.** An ML team has a NIM microservice serving a base foundation model but needs to adapt it to proprietary domain vocabulary using supervised fine-tuning (SFT) and then align it with human feedback (RLHF/DPO) before redeploying. Which NVIDIA component is designed specifically for this customization workflow?

A) Triton Inference Server
B) NVIDIA Riva
C) NVIDIA NeMo framework
D) NGC Container Registry

---

**Q37.** A software vendor wants to rapidly build a retrieval-augmented generation (RAG) customer support agent by combining an embedding NIM, an LLM NIM, a vector database connector, and a reference orchestration pipeline, instead of designing the architecture from scratch. Which NVIDIA resource is specifically intended for this?

A) An NVIDIA AI Enterprise driver branch release
B) An NVIDIA Blueprint reference workflow
C) A standalone NeMo Curator data pipeline
D) A bare-metal NGC base OS image

---

**Q38.** During a local NIM microservice deployment following NVIDIA's standard quickstart, which environment variable must be set to a valid NGC personal key so the container can authenticate to pull the model and run `docker login nvcr.io`?

A) CUDA_VISIBLE_DEVICES
B) NGC_API_KEY
C) NIM_MODEL_PROFILE
D) TRITON_SERVER_URL

---

**Q39.** A platform architect is explaining NVIDIA Blueprints to a new developer. Which statement BEST describes their primary purpose within the NVIDIA AI Enterprise ecosystem?

A) They are low-level GPU drivers that must be installed before any NIM microservice can run
B) They are the billing and licensing layer that tracks NVIDIA AI Enterprise subscription usage
C) They are customizable reference workflows that assemble NIM microservices and supporting components into a working application pattern for a specific use case
D) They are a replacement for NeMo used exclusively for pretraining foundation models from scratch

---

**Q40.** A team needs to deploy a 70-billion-parameter LLM for inference using FP16 precision (2 bytes per parameter). Ignoring KV cache and activation memory, which configuration provides enough GPU memory to hold just the model weights?

A) One NVIDIA H100 80GB GPU
B) One NVIDIA A10 24GB GPU
C) Two NVIDIA A100 80GB GPUs with tensor parallelism
D) One NVIDIA A100 80GB GPU with INT4 quantization enabled

---

**Q41.** An inference service must handle 500 requests per second. Each request takes 150ms of generation time on a single GPU instance, and each instance processes only one request at a time. What is the MINIMUM number of GPU instances needed to meet this demand?

A) 50 GPU instances
B) 75 GPU instances
C) 65 GPU instances
D) 100 GPU instances

---

**Q42.** A startup wants to fine-tune a 13-billion-parameter model using LoRA (Low-Rank Adaptation) on a single GPU with a limited budget. The base model stays frozen in FP16 during training. Which GPU is the BEST fit for this workload?

A) NVIDIA A10 24GB
B) NVIDIA H100 80GB
C) NVIDIA T4 16GB
D) NVIDIA L40S 48GB

---

**Q43.** A model's weights require 200GB of GPU memory in FP16 and must be served on GPUs with 80GB of memory each. Assuming even sharding with no extra overhead, what is the MINIMUM tensor-parallel degree needed to fit the model?

A) 2
B) 4
C) 5
D) 3

---

**Q44.** In LLM inference serving, GPU memory consumed by the KV cache grows primarily with which combination of factors?

A) Sequence length (context size) and batch size (concurrent requests)
B) Model's total parameter count and FP16 precision alone
C) Number of attention heads only, independent of sequence length
D) GPU clock speed and PCIe bandwidth

---

**Q45.** A robotics team must train a perception model to recognize warehouse obstacles under thousands of lighting, texture, and camera-angle variations, but collecting and labeling that much real-world footage is impractical. Which approach BEST addresses this requirement while minimizing the sim-to-real gap?

A) Fine-tune the model directly on a small set of real images using NeMo Customizer
B) Deploy Triton Inference Server with dynamic batching to collect more inference-time data
C) Use TAO Toolkit alone to retrain the model architecture from scratch on existing public datasets
D) Generate synthetic training data with domain randomization using Isaac Sim and Omniverse Replicator

---

**Q46.** A manufacturing plant builds a virtual replica of its production line in NVIDIA Omniverse. Sensor data from the physical line streams in continuously, and changes on the factory floor are reflected in the virtual model in near real time. Which characteristic distinguishes this from a standalone physics simulation?

A) It uses GPU-accelerated physics instead of CPU-based physics calculations
B) It only runs deterministic scenarios rather than probabilistic ones
C) It is continuously synchronized with live data from its real-world counterpart, functioning as a true digital twin
D) It requires no robot or machine learning model to operate

---

**Q47.** A company has validated a perception-and-control model in simulation and now needs to deploy it onto a mobile robot operating in a facility with no reliable internet connection, requiring real-time inference at the edge. Which combination of NVIDIA technologies is the BEST fit for this deployment?

A) DGX Cloud with Triton Inference Server for centralized low-latency inference
B) NVIDIA Jetson running Isaac ROS for on-device perception and control
C) NeMo Guardrails deployed on a CPU-only edge gateway
D) Omniverse Replicator running continuously on the robot to regenerate synthetic data

---

