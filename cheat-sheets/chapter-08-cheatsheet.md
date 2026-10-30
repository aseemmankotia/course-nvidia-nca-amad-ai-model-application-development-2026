## Chapter 8 Cheat Sheet: Sizing & Configuration

### Precision → Memory per Parameter
| Precision | Bytes/Param | Reduction vs FP32 |
|---|---|---|
| FP32 | 4 | 1x (baseline) |
| FP16 / BF16 | 2 | 2x |
| INT8 | 1 | 4x |
| INT4 | 0.5 | 8x |

**Exam rule:** lower precision = smaller memory + faster inference, but more accuracy risk. BF16 and FP16 are equal in size; they differ only in numeric range/stability.

### Memory Estimation Formulas
- **Inference:** `params × bytes/param × ~1.1–1.2 overhead` (KV cache + activations)
- **Full fine-tuning (Adam, mixed precision):** `~16 bytes/param` (weights + gradients + optimizer states) — roughly **4x** the FP16 inference estimate

Example: 7B model, FP16 inference ≈ 7B × 2B × 1.15 ≈ **16GB**. Full fine-tune of same model ≈ 7B × 16B ≈ **112GB**.

### GPU Memory Reference
| GPU | Memory |
|---|---|
| T4 | 16GB |
| A10 / L4 | 24GB |
| A100 | 40GB or 80GB |
| H100 | 80GB |
| H200 | 141GB |

### Training vs Inference Hardware
| Factor | Training | Inference |
|---|---|---|
| Memory need | Very high (weights+grads+optimizer) | Lower (weights + small overhead) |
| Interconnect | Critical — NVLink/NVSwitch for gradient sync | Usually not critical |
| GPU count | Often multi-GPU/multi-node | Often single GPU (or sharded only if model too large) |
| Priority | Throughput over large batches | Low latency, steady throughput |

**Common mistake:** choosing a PCIe-only multi-GPU setup for training — gradient all-reduce becomes the bottleneck without NVLink/NVSwitch.

### Scaling Strategies
| Scenario | Use |
|---|---|
| Bursty/unpredictable inference traffic | **Horizontal** scaling (add/remove replicas) |
| Model too large for one GPU's memory | **Vertical**/multi-GPU scaling (tensor/model parallelism) |
| Steady, predictable load | Right-size a single instance tier, avoid overprovisioning |

**Common mistake:** using vertical scaling (bigger GPU) to fix a traffic-volume problem when the model already fits — wastes cost without solving concurrency.

### Cost/Capacity Tradeoff Checklist
1. Does the model **fit** on one GPU at target precision? If not → multi-GPU (vertical) before anything else.
2. Is the workload **training** or **inference**? Training needs ~4x the memory and high-bandwidth interconnect.
3. Is traffic **spiky**? → horizontal scaling of replicas.
4. Can precision be lowered (FP16→INT8) to shrink footprint and cost without breaking accuracy requirements?
5. Avoid both under-provisioning (OOM errors) and over-provisioning (idle expensive GPUs) — exam scenarios test both directions.
