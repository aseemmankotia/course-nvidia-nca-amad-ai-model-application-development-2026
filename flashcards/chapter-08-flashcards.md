## Chapter 8: Sizing and Configuration: Right-Sizing GPUs for AI Workloads — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | FP32 memory cost per parameter? | 4 bytes/parameter. Exam tip: baseline for memory math — everything else is compared as a multiple reduction from this. |
| 2 | FP16 / BF16 memory cost per parameter? | 2 bytes/parameter — a 2x reduction from FP32. Exam tip: BF16 and FP16 have identical memory footprint; they differ in numerical range, not size. |
| 3 | INT8 memory cost per parameter? | 1 byte/parameter — a 4x reduction from FP32, 2x reduction from FP16. Exam tip: common quantization target for inference-only deployment. |
| 4 | INT4 memory cost per parameter? | 0.5 bytes/parameter — 8x reduction from FP32. Exam tip: lowest common precision tier tested; largest accuracy risk. |
| 5 | Quick formula for inference GPU memory estimate? | params × bytes_per_param × ~1.1–1.2 overhead (KV cache + activations). Exam tip: always add overhead — raw weight size alone underestimates real requirement. |
| 6 | Rule-of-thumb GPU memory for full fine-tuning with Adam, mixed precision? | ~16 bytes/parameter (weights + gradients + optimizer moment estimates) — roughly 4x the FP16 inference-only estimate. Exam tip: training ALWAYS needs far more memory than inference for the same model. |
| 7 | NVIDIA H100 vs H200 memory capacity? | H100: 80GB HBM. H200: 141GB HBM3e. Exam tip: H200's larger memory is the key differentiator for fitting bigger models per GPU without added tensor parallelism. |
| 8 | Training vs inference: which needs high-bandwidth GPU interconnect (NVLink/NVSwitch)? | Training — gradient synchronization across GPUs demands high bandwidth. Inference (single GPU or simple replication) usually does not need it. Exam tip: PCIe-only multi-GPU is a major training bottleneck, not usually an inference one. |
| 9 | Horizontal vs vertical scaling for inference traffic spikes — which is preferred? | Horizontal scaling (add/remove replicas) for bursty, unpredictable, stateless traffic. Vertical scaling (bigger GPU) is for when the MODEL itself doesn't fit, not for traffic volume. |
| 10 | Model doesn't fit on a single GPU — what's the scaling approach? | Use tensor/model parallelism across multiple GPUs (vertical + multi-GPU scaling), not horizontal replication. Exam tip: horizontal scaling only helps with request volume, not with a model too large for one GPU's memory. |
| 11 | Which GPU tier fits small (1-3B param) latency-sensitive inference cost-effectively? | Lower/mid-tier GPUs like NVIDIA L4 or A10 (24GB). Exam tip: using H100/H200-class GPUs for small models is a common 'overkill' wrong answer on cost-optimization scenarios. |
| 12 | Cost/accuracy tradeoff of lowering precision (e.g., FP32 → INT8)? | Lower precision = smaller memory footprint, lower cost, faster inference, but increased risk of accuracy degradation. Exam tip: scenario questions testing 'cheapest option that still meets accuracy' usually point to INT8 over FP32/FP16. |
