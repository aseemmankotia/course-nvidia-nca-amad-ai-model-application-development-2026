## Chapter 4: Inference Concepts: Serving Models at Scale — Practice Questions

**Q1.** A chat application must respond within 200ms P99. The serving config currently uses a large batch size, producing 800ms P99 latency with high throughput. Which change BEST meets the latency requirement?

A) Increase batch size further to amortize per-batch overhead across more requests
B) Switch all requests to CPU inference to avoid GPU queuing
C) Reduce max batch size and lower the batching queue delay to prioritize per-request latency over aggregate throughput
D) Convert the model to FP32 to improve numerical stability under load

<details>
<summary>Answer</summary>

**Correct: C**

Smaller batch size and shorter queue delay reduce the time requests wait to be grouped and executed, directly lowering per-request latency at the cost of some aggregate throughput — the correct tradeoff for interactive workloads.

**Why the others are wrong:**
- Increasing batch size further increases queuing time, worsening latency.
- CPU inference for LLMs is significantly slower than GPU and will not meet a 200ms bound.
- FP32 increases compute and memory load per request, increasing latency rather than reducing it.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A team must serve a 70B-parameter LLM on a single 80GB GPU. At FP16, weights alone require roughly 140GB, exceeding available memory, and no additional GPUs are available. Which change BEST allows the model to fit while preserving most accuracy?

A) Keep FP16 weights and reduce the KV cache allocation to zero
B) Quantize the model weights to INT8 or FP8, roughly halving the weight memory footprint
C) Switch the model to FP32 to improve precision and reduce parameter count
D) Run the model only in training mode to avoid needing a KV cache

<details>
<summary>Answer</summary>

**Correct: B**

INT8/FP8 use 1 byte per parameter vs FP16's 2 bytes, roughly halving weight memory (≈70GB), which fits the 80GB GPU while retaining most accuracy compared to more aggressive quantization.

**Why the others are wrong:**
- Zeroing the KV cache removes the ability to generate beyond the first token and doesn't fix the larger weight-memory bottleneck.
- FP32 uses 4 bytes/param (≈280GB), making the problem worse, and precision format doesn't change parameter count.
- Training mode is irrelevant to serving and does not reduce weight memory.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An inference service hits out-of-memory errors only when requests have very long input contexts (8K+ tokens) combined with large batch sizes, even though model weights alone fit comfortably in GPU memory. What is the MOST LIKELY cause?

A) The KV cache memory footprint, which scales with sequence length and batch size, is exhausting remaining GPU memory
B) A bug in the Triton Inference Server scheduler
C) The model must be running in FP32 weights
D) The GPU driver needs an upgrade to support longer sequences

<details>
<summary>Answer</summary>

**Correct: A**

KV cache memory grows with batch size × sequence length × layers × heads × head dim, so long contexts combined with large batches can exceed available memory even when static weights fit easily.

**Why the others are wrong:**
- A scheduler bug would not specifically correlate with long context and large batch combinations.
- Weights are already confirmed to fit; the OOM is from activation/cache memory, not weight precision.
- Driver version does not govern GPU memory capacity or KV cache sizing.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A company wants a pre-packaged, production-ready inference microservice for a supported foundation model, exposing an OpenAI-compatible API with minimal custom configuration, deployable as a single container. Which NVIDIA offering BEST fits this?

A) NVIDIA NIM (NVIDIA Inference Microservice)
B) Triton Inference Server configured manually with a custom backend
C) A TensorRT engine built and run with a custom Python wrapper
D) The CUDA Toolkit installed directly on bare metal

<details>
<summary>Answer</summary>

**Correct: A**

NIM provides pre-optimized, packaged containers for supported models with standardized APIs (often OpenAI-compatible), designed for minimal-configuration deployment.

**Why the others are wrong:**
- Triton requires manually building a model repository and backend configuration — more setup effort than 'minimal configuration'.
- Building a custom TensorRT engine and wrapper requires significant engineering work, not a packaged microservice.
- The CUDA Toolkit is a development/runtime library, not an inference serving solution.

</details>

---

**Q5.** A platform team needs to serve multiple frameworks (PyTorch, ONNX, TensorRT) from a single server, with dynamic batching and concurrent model execution across GPUs. Which tool is purpose-built for this?

A) NVIDIA NIM
B) A custom Flask REST API wrapping each model separately
C) NVIDIA DALI
D) Triton Inference Server

<details>
<summary>Answer</summary>

**Correct: D**

Triton is a general-purpose, multi-framework inference server with built-in dynamic batching, model ensembles, and concurrent model execution across GPUs.

**Why the others are wrong:**
- NIM packages a specific model (or model family) per microservice rather than hosting arbitrary mixed-framework models side by side.
- A Flask wrapper lacks built-in batching, concurrent execution, and multi-backend abstraction, requiring custom engineering.
- DALI is a data loading and preprocessing library, not a model-serving backend.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** In a Triton Inference Server model configuration file, which setting controls how long the server waits to accumulate additional requests into a batch before executing inference, trading a small amount of latency for higher throughput?

A) max_batch_size
B) instance_group count
C) model_warmup
D) dynamic_batching max_queue_delay_microseconds

<details>
<summary>Answer</summary>

**Correct: D**

max_queue_delay_microseconds inside the dynamic_batching block sets the maximum wait window for accumulating requests into a batch.

**Why the others are wrong:**
- max_batch_size sets the upper size limit of a batch, not how long to wait to fill it.
- instance_group controls how many model instances/replicas execute concurrently, not batching delay.
- model_warmup pre-runs sample requests at load time and is unrelated to batching delay.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A team deploying an LLM on NVIDIA H100 GPUs wants the lowest-precision floating-point format natively accelerated by the Transformer Engine, to maximize throughput while retaining floating-point dynamic range (not integer quantization). Which format should they choose?

A) INT8
B) FP32
C) FP8
D) INT4

<details>
<summary>Answer</summary>

**Correct: C**

FP8 is natively accelerated by Hopper's (and later generations') Transformer Engine and is a floating-point format, preserving dynamic range unlike integer quantization.

**Why the others are wrong:**
- INT8 is an integer format, not floating point, so it doesn't satisfy the dynamic-range requirement even though it's supported.
- FP32 is the highest-precision, highest-memory format — the opposite of 'lowest precision'.
- INT4 is an even lower-precision integer format, not a floating-point format, and isn't the Transformer Engine's native floating-point path.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement BEST describes a key difference between training and inference compute profiles?

A) Training requires only forward passes, while inference requires both forward and backward passes
B) Inference always uses higher numerical precision than training to guarantee accuracy
C) Training and inference have identical memory requirements because both use the same model weights
D) Training is typically throughput-oriented and performed in large batches offline, while inference is often latency-sensitive and may need to serve variable, smaller batch sizes in real time

<details>
<summary>Answer</summary>

**Correct: D**

Training is generally offline and batch-throughput oriented with large batches, while inference is frequently real-time and latency-sensitive, needing to handle variable and often smaller batch sizes.

**Why the others are wrong:**
- This is reversed — training requires both forward and backward passes (for gradients); inference needs only the forward pass.
- Inference commonly uses LOWER precision (FP16/INT8/FP8) than training for speed and memory savings, not higher.
- Inference has no gradients or optimizer states, so its memory profile is substantially different (lower) than training's, despite sharing weights.

</details>

---

