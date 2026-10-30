# Practice Test 1: NCA-AMAD: NVIDIA AI Model & App Dev Exam Prep

- **Questions:** 47
- **Time limit:** 90 minutes
- **Passing score:** 70%%

> Answers are in `answer-key-1.md`. Track results in `score-tracker.md`.

---

**Q1.** A travel booking application must: query live flight availability from an external API, compare prices across three providers, and generate a personalized itinerary summary. Which approach BEST meets these requirements?

A) A single large language model call with a long system prompt describing all three providers' pricing
B) An agentic workflow where the model uses tool calling to query each API, reasons over the results, then generates the summary
C) A model fine-tuned once on historical flight data
D) A static rules engine with no language model involved

---

**Q2.** A development team is building a customer-facing agent and must ensure the model cannot be jailbroken into discussing competitor pricing or generating harmful content. Which NVIDIA offering is purpose-built to enforce these conversational boundaries?

A) NVIDIA TensorRT-LLM
B) NVIDIA Triton Inference Server
C) NVIDIA NeMo Guardrails
D) NVIDIA NIM

---

**Q3.** In the context of agentic AI, what does 'tool use' (function calling) refer to?

A) A quantization technique for reducing model size before deployment
B) The ability of a model to output a structured request invoking an external function or API, with the results fed back into its context
C) The model's internal attention mechanism for weighting input tokens
D) The fine-tuning process using labeled tool-usage datasets

---

**Q4.** An agent built with a ReAct-style reasoning loop occasionally enters a cycle of repeated tool calls without reaching a final answer. Which configuration change directly addresses this?

A) Set a maximum number of reasoning/tool-call iterations before forcing a final response
B) Switch the agent to a model with a larger context window
C) Increase the model's temperature setting
D) Disable tool calling entirely

---

**Q5.** A content-generation pipeline requires one component to research a topic, another to draft an article, and a third to critique and request revisions before publishing. Which architecture pattern BEST fits this requirement?

A) A single monolithic prompt asking one model to research, write, and critique in one pass
B) A multi-agent orchestration pattern with specialized agents (researcher, writer, critic) coordinated by an orchestrator
C) A single fine-tuned model deployed with no orchestration layer
D) A batch inference job with no feedback loop between stages

---

**Q6.** A support agent must answer some questions directly from its trained knowledge (e.g., 'what is 2+2') but retrieve from an internal knowledge base for product-specific questions. Which agentic design BEST supports this dual behavior?

A) Always perform retrieval augmented generation (RAG) for every incoming query regardless of type
B) A single static prompt with the entire knowledge base embedded as context for every request
C) An agent that reasons about whether retrieval is needed, then conditionally invokes a retrieval tool before generating its answer
D) A model fine-tuned to memorize the entire knowledge base at training time

---

**Q7.** A support tool needs to answer a single, static factual question by looking up one company FAQ document. No follow-up actions, external tool calls, or multi-step planning are required. Which approach BEST fits NVIDIA's guidance on when to use agentic workflows versus a direct model call?

A) Build a multi-agent system with a planner agent that orchestrates sub-agents to retrieve and summarize the answer
B) Make a single inference call augmented with retrieved context from the FAQ document (RAG), without an agent loop
C) Deploy an agent with tool-calling and persistent memory so it can track the conversation across sessions
D) Apply NeMo Guardrails to the raw query with no retrieval step, relying on the model's parametric knowledge

---

**Q8.** A developer is building an agent that needs to invoke external functions (e.g., a weather API) based on model output, using an NVIDIA NIM-deployed LLM. Which interface does the NIM microservice expose to support this structured function/tool calling?

A) An OpenAI-compatible chat completions API that supports a tool_calls field in the response
B) A proprietary NIM-only schema that requires a custom NVIDIA SDK to parse function call outputs
C) Triton Inference Server's native dynamic batching API for scheduling concurrent requests
D) A raw gRPC protobuf interface used for low-level tensor input/output serialization

---

**Q9.** A company deploys a customer support chatbot powered by a fine-tuned LLM. They want to continuously improve the model using real user interactions over time. Which approach BEST describes implementing a 'data flywheel'?

A) Continuously collect, curate, and feed production interaction data back into retraining or fine-tuning pipelines to improve future model versions
B) Discard all production conversation logs immediately for privacy compliance
C) Rely solely on the original pretraining dataset and never update the model
D) Require a human to manually approve every single inference request before it is served to users

---

**Q10.** A development team is building a retrieval-augmented generation (RAG) pipeline and needs to convert document chunks into dense vector representations for similarity search. Which type of NVIDIA component should they use?

A) NeMo Curator, used for raw dataset deduplication and filtering
B) TensorRT-LLM configured purely for autoregressive text generation
C) Triton Inference Server configured only to serve a classification model
D) An NVIDIA NIM embedding microservice (such as an NV-Embed model) that outputs dense vector embeddings

---

**Q11.** When preparing documents for an embedding-based retrieval pipeline, what is the PRIMARY consideration when choosing a chunking strategy and chunk size?

A) Larger chunks always improve retrieval accuracy no matter the embedding model used
B) Chunk size has no measurable effect on embedding or retrieval quality
C) Every chunk must be reduced to exactly one sentence regardless of content
D) Chunk size must balance preserving semantic coherence against the embedding model's maximum context length

---

**Q12.** What is the PRIMARY purpose of incorporating synthetic data generation into an AI data pipeline?

A) To completely replace the need for evaluation and benchmarking metrics
B) To eliminate the need for any data governance or quality review process
C) To augment scarce, imbalanced, or sensitive real-world data and improve coverage of underrepresented edge cases
D) To reduce the amount of GPU memory consumed during model inference

---

**Q13.** A team is preparing a large web-crawled text corpus for model pretraining using NeMo Curator. Which curation step is MOST important for reducing model memorization of exact training examples and avoiding wasted compute?

A) Increasing the training batch size to speed up throughput
B) Converting all text in the corpus to uppercase before tokenization
C) Reducing the vocabulary size used by the tokenizer
D) Deduplication of near-identical or exact-duplicate documents across the corpus

---

**Q14.** An AI application logs user feedback (thumbs up/down) on generated responses, intending to use this feedback to improve the model through the data flywheel. Which practice is MOST important for responsibly operationalizing this feedback loop?

A) Immediately retrain the production model in real time on every single feedback item without any review
B) Establish a governance process that curates, validates, and filters feedback data before it enters retraining or fine-tuning pipelines
C) Ignore negative feedback entirely since it occurs infrequently compared to positive feedback
D) Store all feedback indefinitely and treat every entry as verified ground truth without quality checks

---

**Q15.** A team is building a RAG-based customer support application. They need to store document embeddings and retrieve the most semantically similar chunks at query time with low latency, at a scale of tens of millions of vectors. Which component should they add to their data pipeline to meet this requirement?

A) A relational database with full-text search indexing on raw document text
B) A message queue that batches documents for periodic offline processing
C) A vector database that performs approximate nearest neighbor search over embedding vectors
D) A key-value cache that stores documents indexed by filename

---

**Q16.** An AI team deploys a chatbot in production. They want to use real user interactions (queries, model responses, and user feedback like thumbs up/down) to continuously identify weak spots and retrain or fine-tune the model over time. This closed-loop process of using production data to drive ongoing model improvement is best described as:

A) Data augmentation
B) Zero-shot transfer
C) The data flywheel
D) Model distillation

---

**Q17.** A company is building a real-time voice assistant that must return responses within 200ms per request on a GPU-based inference server. Which serving strategy BEST meets this requirement?

A) Increase the batch size as much as possible to maximize GPU utilization
B) Queue incoming requests for several seconds to accumulate a large batch before processing
C) Use dynamic batching with a small maximum batch size and a short queue delay
D) Run inference exclusively in FP32 precision to maximize throughput

---

**Q18.** A team needs to deploy a fine-tuned LLM in production with an industry-standard inference API, an optimized runtime engine, and minimal custom integration work. Which NVIDIA offering BEST fits this need?

A) An NVIDIA NIM microservice
B) A raw PyTorch script wrapped in a Flask web server
C) A standalone TensorRT engine file with no serving layer
D) A hand-written custom backend for Triton Inference Server

---

**Q19.** In transformer-based LLM inference, what does the KV cache store to avoid redundant computation during autoregressive token generation?

A) The full vocabulary embedding lookup table
B) Quantized weights of the feed-forward network layers
C) Key and Value tensors from attention layers for previously generated tokens
D) Gradient values computed during backpropagation

---

**Q20.** A model must run on an NVIDIA Jetson edge device with limited onboard memory, requiring low latency, where a small accuracy tradeoff is acceptable. Which approach BEST fits these constraints?

A) Apply INT8 quantization to the model
B) Run the model in FP32 precision
C) Run the model in FP64 precision for maximum numerical stability
D) Keep full precision but offload computation to the CPU

---

**Q21.** Which Triton Inference Server feature automatically combines multiple incoming client inference requests into a single batch at runtime to improve GPU throughput?

A) Model ensemble
B) Model versioning
C) Dynamic batching
D) Concurrent model execution

---

**Q22.** Which statement correctly describes a key difference between training and inference workloads?

A) Inference requires more GPU memory than training because it uses larger batch sizes
B) Training is typically latency-sensitive while inference is throughput-sensitive
C) Inference always requires a distributed multi-node GPU cluster, while training can always run on a single GPU
D) Training requires forward and backward passes with gradient computation, while inference requires only a forward pass

---

**Q23.** A team deploys a large language model to handle customer support chats. As conversations grow longer (more turns, longer context), they observe GPU memory consumption climbing steadily during a single inference session, even though the model's weights are loaded once and never change. Which component is responsible for this growing memory usage?

A) The model weights, which are re-quantized at each new token generation step
B) The KV cache, which stores key and value tensors for every token in the growing context and scales with sequence length and batch size
C) Triton Inference Server's model repository, which caches a new copy of the model for each request
D) The tokenizer, which allocates new vocabulary embeddings as the conversation grows

---

**Q24.** A legal-tech company's internal policy documents change weekly, and their chatbot must always cite the latest version without constant retraining cycles. Which customization approach BEST meets this requirement?

A) Retrieval-Augmented Generation (RAG) that queries an updated document index at inference time
B) Full pretraining on the policy corpus every week
C) LoRA fine-tuning repeated weekly on the new documents
D) Prompt engineering with a static few-shot example set

---

**Q25.** A startup wants its LLM to consistently adopt a specific brand tone and structured output format. They have a small labeled dataset of 2,000 examples and only a single GPU with 24GB VRAM. Which technique is MOST appropriate?

A) Full fine-tuning of all model parameters
B) Parameter-efficient fine-tuning (e.g., LoRA)
C) Training a foundation model from scratch
D) Pure prompt engineering with no training

---

**Q26.** A team needs a model to output a new structured JSON schema reliably across thousands of varied inputs, but they only have limited compute and a small instruction dataset. Which customization path should they choose?

A) Instruction tuning via parameter-efficient fine-tuning (PEFT)
B) Full model pretraining on a new corpus
C) Increasing the context window size only
D) Switching to a larger foundation model with no tuning

---

**Q27.** In LoRA fine-tuning, what does the rank (r) hyperparameter primarily control?

A) The number of attention heads added to the model
B) The learning rate schedule used during training
C) The dimensionality of the low-rank update matrices, trading off adaptation capacity against trainable parameters and memory
D) The number of tokens retrieved from a vector database

---

**Q28.** How does Direct Preference Optimization (DPO) conceptually differ from classic RLHF for aligning a model to human preferences?

A) DPO requires significantly more labeled preference data than RLHF
B) DPO optimizes the policy directly on preference pairs without training a separate reward model or running reinforcement learning
C) DPO only works on vision models, while RLHF is text-only
D) DPO eliminates the need for any human feedback

---

**Q29.** A well-funded enterprise needs its model to acquire entirely new reasoning capabilities not present in any available foundation model, has a massive proprietary dataset, and has budgeted for large-scale GPU clusters over months. Which approach is justified here?

A) Full-scale training/pretraining of a custom model on the proprietary dataset
B) Prompt engineering with chain-of-thought templates
C) Lightweight LoRA adapters only
D) Retrieval-Augmented Generation over the proprietary dataset

---

**Q30.** A company wants to build a document search system that returns results based on semantic meaning rather than exact keyword matches, by converting text passages into dense vector representations for similarity comparison in a vector database. Which model type BEST meets this requirement?

A) A diffusion model fine-tuned on text metadata
B) A multimodal vision-language model
C) A large language model configured to summarize each document
D) An embedding model

---

**Q31.** A marketing team wants to generate photorealistic product images from short text descriptions for an upcoming ad campaign. Which model type should they use?

A) An embedding model trained on the product catalog
B) A multimodal classification model
C) A diffusion-based generative vision model
D) A transformer-based text embedding model

---

**Q32.** A developer is building an application where a user uploads a photo and asks, "What color is the car in this image?" The app must interpret both the image content and the natural-language question together to produce an answer. Which model type is the correct fit for this capability?

A) An embedding model
B) A multimodal (vision-language) model
C) A text-only large language model
D) A diffusion model

---

**Q33.** In the transformer architecture used by modern LLMs, what does the self-attention mechanism allow the model to do, and why is this central to how these models process context?

A) Dynamically weigh the relevance of every token to every other token in the input, regardless of their distance in the sequence
B) Compress the entire input sequence into a single fixed-length vector before any further processing
C) Apply convolutional filters to extract features only from immediately adjacent tokens
D) Assign fixed, unchanging weights to tokens based solely on their position in the sequence

---

**Q34.** A development team must fine-tune a model on sensitive proprietary data and deploy the resulting model entirely within their own on-premises infrastructure, with no data or inference requests sent to an external vendor's API. Which category of model MUST they select to meet this requirement?

A) A proprietary model accessed only through a vendor's hosted cloud API
B) An embedding-only model with no generative capability
C) An open-weight model whose parameters can be downloaded and run locally
D) A diffusion model specialized for image generation

---

**Q35.** A company wants to deploy a pretrained large language model into production with minimal customization, requiring an optimized, scalable inference API that can run consistently across cloud, data center, and workstation environments. Which NVIDIA AI Enterprise component BEST meets this requirement?

A) NVIDIA NeMo Curator
B) NVIDIA Triton Inference Server configured manually from scratch
C) NVIDIA Blueprint for customer service
D) NVIDIA NIM microservice

---

**Q36.** A data science team needs to deduplicate, filter, and quality-score massive text datasets before using them to fine-tune a custom LLM. Which NVIDIA AI Enterprise component is specifically designed for this data processing task?

A) NVIDIA NIM
B) NVIDIA Riva
C) NVIDIA TensorRT-LLM
D) NVIDIA NeMo Curator

---

**Q37.** An enterprise wants to quickly stand up a retrieval-augmented generation (RAG) chatbot connected to their internal documents, preferring a proven reference architecture over designing the pipeline from scratch. Which NVIDIA offering should they start with?

A) NVIDIA Triton Inference Server
B) NVIDIA CUDA Toolkit
C) NVIDIA AI Blueprint for RAG
D) NVIDIA cuDNN

---

**Q38.** When a developer deploys a large language model as a NIM microservice, what API format does NIM expose by default to ensure compatibility with existing application code?

A) OpenAI-compatible REST API
B) A proprietary NVIDIA-only API requiring custom SDKs
C) gRPC-only interface with no REST support
D) SOAP-based XML API

---

**Q39.** What is the primary purpose of NVIDIA AI Enterprise as a software platform?

A) It is a hardware-only GPU product line for data centers
B) A free, community-supported open-source AI toolkit with no enterprise support
C) A cloud-hosted SaaS chatbot product only
D) An end-to-end, enterprise-grade AI software suite providing certified, secure, and supported tools (including NIM and NeMo) for building and deploying AI across cloud, data center, and edge

---

**Q40.** A team needs to deploy a 13B-parameter LLM for inference using FP16 precision. Accounting for a typical 20% overhead for KV cache and activation memory, what is the MINIMUM GPU memory capacity they should provision from standard available options?

A) 16 GB
B) 24 GB
C) 80 GB
D) 40 GB

---

**Q41.** A company is training a new foundation model from scratch across multiple server nodes and needs to minimize communication bottlenecks between GPUs during distributed training. Which infrastructure choice BEST meets this requirement?

A) Multi-GPU servers connected via NVLink/NVSwitch within nodes and InfiniBand networking between nodes
B) A single-node server with one A100 GPU
C) A CPU-only cluster with high core counts
D) Edge devices such as Jetson modules clustered together

---

**Q42.** A deployment team wants to reduce the memory footprint of a trained FP32 model for faster, cheaper inference while minimizing accuracy loss. Which NVIDIA tool performs INT8 calibration and quantization for optimized inference deployment?

A) NCCL
B) TensorRT
C) DALI
D) cuDNN

---

**Q43.** When moving from running inference on a model to performing full fine-tuning of that same model, which factor causes the LARGEST increase in required GPU memory?

A) The addition of gradients and optimizer states during backpropagation
B) Increasing the input batch size
C) Switching from FP16 to INT8 precision
D) Updating to a newer GPU driver version

---

**Q44.** An inference application is experiencing a sudden 10x increase in request volume. The team must handle the spike reliably while controlling infrastructure cost. Which approach BEST meets these requirements?

A) Serve all traffic from a single, permanently provisioned high-memory GPU
B) Deploy NVIDIA Triton Inference Server with dynamic batching across an autoscaling pool of GPU instances behind a load balancer
C) Switch the model to run on CPU-only instances to reduce cost
D) Manually provision a fixed number of extra GPUs sized for peak traffic year-round

---

**Q45.** A robotics startup is developing a warehouse navigation robot. Before deploying to physical hardware, the team wants to train the robot's navigation policy in a photorealistic virtual environment, generate synthetic sensor data with domain randomization, and validate behavior safely at scale. Which NVIDIA platform BEST meets these requirements?

A) NVIDIA NeMo
B) NVIDIA Isaac Sim
C) NVIDIA Triton Inference Server
D) NVIDIA NIM

---

**Q46.** Which NVIDIA platform provides the foundation for building physically accurate, photorealistic digital twins of real-world environments and systems using OpenUSD?

A) NVIDIA Merlin
B) NVIDIA Riva
C) NVIDIA TAO Toolkit
D) NVIDIA Omniverse

---

**Q47.** Which statement BEST defines 'physical AI' as covered in the context of robotics and autonomous systems?

A) AI systems that are restricted to running only on edge hardware devices
B) AI models trained exclusively using synthetic data instead of real-world data
C) AI applications that exclusively process natural language without any sensor input
D) AI systems that perceive, reason about, and take actions within real-world physical environments

---

