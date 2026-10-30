## Chapter 8: Sizing and Configuration: Right-Sizing GPUs for AI Workloads — Practice Questions

**Q1.** A team must deploy a 70B parameter LLM for inference using FP16 precision. Estimated memory need is roughly params × 2 bytes plus 10-15% overhead for KV cache and activations (~155-160GB total). Which hardware configuration BEST meets this requirement?

A) Two NVIDIA H100 80GB GPUs with tensor parallelism (160GB combined)
B) Single NVIDIA A100 80GB GPU
C) Four NVIDIA A10 24GB GPUs (96GB combined)
D) Single NVIDIA T4 16GB GPU with INT4 quantization only

<details>
<summary>Answer</summary>

**Correct: A**

160GB combined memory across two H100 80GB GPUs with tensor parallelism covers the ~155-160GB requirement for FP16 weights plus overhead.

**Why the others are wrong:**
- A single 80GB GPU cannot hold ~160GB of required memory regardless of GPU model.
- 96GB across four A10s is still below the ~160GB requirement and A10s lack the interconnect bandwidth for efficient tensor parallelism at this scale.
- INT4 would change the memory math entirely and isn't what the scenario specifies (FP16 was required); swapping precision silently is not a valid sizing fix.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** An inference endpoint for a fixed model serves unpredictable, bursty traffic. The model already fits comfortably on a single GPU. Which scaling strategy is the BEST fit for handling the spikes cost-effectively?

A) Vertical scaling: move the single instance to a GPU with far more memory
B) Switch the model to FP32 precision to improve stability under load
C) Deploy a single large multi-GPU node permanently sized for peak traffic
D) Horizontal scaling: add or remove GPU inference replicas behind a load balancer based on demand

<details>
<summary>Answer</summary>

**Correct: D**

Horizontal scaling of stateless inference replicas matches elastic, unpredictable traffic without paying for peak capacity at all times.

**Why the others are wrong:**
- Vertical scaling adds memory the model doesn't need — the bottleneck here is request volume, not per-request memory.
- FP32 increases memory footprint and latency; it does not address throughput or traffic spikes.
- Permanently provisioning for peak wastes cost during low-traffic periods and isn't elastic.

</details>

---

**Q3.** A team training a 13B parameter model from scratch across 8 GPUs observes severe slowdowns during gradient synchronization steps. What is the MOST likely fix?

A) Increase the per-GPU batch size
B) Use GPUs connected via high-bandwidth interconnect (NVLink/NVSwitch) instead of PCIe-only connections
C) Switch training precision to INT8
D) Move the workload to CPU-based workers for more consistent performance

<details>
<summary>Answer</summary>

**Correct: B**

Multi-GPU training requires frequent gradient all-reduce operations; PCIe-only interconnects bottleneck this traffic, while NVLink/NVSwitch provide the bandwidth needed for efficient synchronization.

**Why the others are wrong:**
- Larger batch size changes compute per step but does not resolve an interconnect bandwidth bottleneck.
- INT8 is not used for training gradient computation due to numerical instability; it's an inference-time optimization.
- CPUs lack the parallel throughput and interconnect bandwidth GPUs provide, making training dramatically slower, not faster.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team needs to reduce GPU memory footprint by approximately 4x compared to FP32 for an inference deployment, with acceptable accuracy loss. Which precision should they choose?

A) FP16
B) BF16
C) INT8
D) TF32

<details>
<summary>Answer</summary>

**Correct: C**

INT8 uses 1 byte per parameter versus FP32's 4 bytes, giving the full 4x memory reduction.

**Why the others are wrong:**
- FP16 uses 2 bytes per parameter, only a 2x reduction from FP32.
- BF16 also uses 2 bytes per parameter, the same 2x reduction as FP16.
- TF32 is a compute mode used on Tensor Cores during matrix operations, not a storage format that reduces memory footprint.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A company needs to run latency-sensitive inference for a 1B parameter recommendation model at moderate throughput. Which option is the MOST cost-effective choice?

A) A cluster of 8x NVIDIA H100 80GB GPUs
B) A single NVIDIA A100 80GB GPU
C) A CPU-only instance with 64 cores
D) A single NVIDIA L4 24GB GPU

<details>
<summary>Answer</summary>

**Correct: D**

A 1B parameter model has a small memory footprint; a lower-tier GPU like the L4 provides sufficient memory and GPU acceleration for latency-sensitive serving at a fraction of the cost of larger GPUs.

**Why the others are wrong:**
- An 8x H100 cluster is massively overprovisioned for a 1B parameter model, wasting cost and capacity.
- A100 80GB offers far more memory and bandwidth than a 1B model requires, increasing cost without benefit.
- CPU-only inference lacks the parallel throughput needed to reliably meet latency-sensitive, moderate-throughput requirements in production.

</details>

---

**Q6.** A 7B parameter model is deployed in FP16 for inference, but GPU memory is still too constrained. The team wants further memory reduction while keeping the model's weights on GPU. Which precision change should they apply next?

A) INT8
B) FP32
C) BF16
D) FP64

<details>
<summary>Answer</summary>

**Correct: A**

INT8 quantization reduces footprint to 1 byte per parameter, half of FP16's 2 bytes, providing further memory savings.

**Why the others are wrong:**
- FP32 uses 4 bytes per parameter, doubling memory versus FP16 instead of reducing it.
- BF16 uses the same 2 bytes per parameter as FP16, providing no additional savings.
- FP64 uses 8 bytes per parameter and is never used for deployed inference workloads; it increases memory further.

</details>

---

**Q7.** For exam-level estimation, which approximation is commonly used to size GPU memory for full fine-tuning of a model with the Adam optimizer in mixed precision?

A) ~16 bytes per parameter (covering weights, gradients, and optimizer states)
B) ~2 bytes per parameter
C) ~1 byte per parameter
D) ~32 bytes per parameter

<details>
<summary>Answer</summary>

**Correct: A**

A common rule of thumb for mixed-precision full fine-tuning with Adam is roughly 16 bytes/parameter: FP16 weights and gradients plus FP32 optimizer moment estimates, roughly 4x the pure FP16 inference estimate.

**Why the others are wrong:**
- 2 bytes/parameter is the FP16 inference weight-only estimate, not a training estimate with optimizer states and gradients.
- 1 byte/parameter corresponds to INT8 inference storage, far too low for training which requires gradients and optimizer states.
- 32 bytes/parameter overstates typical mixed-precision training memory and is not the standard rule of thumb tested.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement correctly differentiates training hardware requirements from inference hardware requirements for AI workloads?

A) Training typically needs low-latency single-GPU setups, while inference needs high-bandwidth multi-GPU interconnects.
B) Both training and inference require identical hardware since they use the same model architecture.
C) Training requires high GPU-to-GPU interconnect bandwidth and larger aggregate memory for gradients and optimizer states, while inference typically prioritizes low latency and can often run on a single GPU or smaller cluster.
D) Inference always requires more total GPU memory than training for the same model.

<details>
<summary>Answer</summary>

**Correct: C**

Training's backward pass and optimizer states demand large memory and fast multi-GPU gradient synchronization, while inference (forward pass only) typically fits in less memory and favors low-latency, often single-GPU, serving.

**Why the others are wrong:**
- This reverses the actual requirements — it's training, not inference, that demands high-bandwidth multi-GPU interconnects.
- Memory, interconnect, and latency priorities differ significantly between training and inference, even for the same model.
- Training requires substantially more memory per parameter (weights + gradients + optimizer states) than inference, not less.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

