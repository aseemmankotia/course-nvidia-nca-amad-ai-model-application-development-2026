# Chapter 4 Cheat Sheet: Inference Concepts

## Latency vs Throughput
| Goal | Batch Size | Queue Delay | Result |
|---|---|---|---|
| Low latency (interactive) | Small | Short | Lower throughput, fast responses |
| High throughput (batch/offline) | Large | Longer | Higher throughput, slower per-request |

**Exam note:** Scenario keywords "real-time chat", "P99 latency" → favor small batch/short delay. "Batch processing", "maximize GPU utilization" → favor large batch.

## Precision Formats
| Format | Bytes/param | Type | Notes |
|---|---|---|---|
| FP32 | 4 | Float | Highest precision, most memory, used in training |
| FP16/BF16 | 2 | Float | Common inference default, mixed precision training |
| FP8 | 1 | Float | Hopper+ Transformer Engine, retains dynamic range |
| INT8 | 1 | Integer | Needs calibration/QAT, faster, smaller |
| INT4 | 0.5 | Integer | Most aggressive compression, higher accuracy risk |

**Exam note:** Memory ≈ params × bytes/param. Quantization trades memory/speed for accuracy.

## KV Cache
- Stores attention K/V tensors per token to avoid recomputation during autoregressive generation.
- Memory scales with: `batch_size × seq_len × num_layers × num_heads × head_dim × 2 (K&V) × precision_bytes`.
- Long context + large batch = common OOM cause even if weights fit.

## Batching Strategies
| Strategy | Mechanism | Server/Backend |
|---|---|---|
| Dynamic batching | Groups requests within a time window | Triton |
| Continuous (in-flight) batching | New requests join an in-progress batch mid-generation | TensorRT-LLM, vLLM backend |

## Triton Inference Server
- Multi-framework backend: TensorRT, PyTorch, ONNX Runtime, Python, vLLM.
- Key config fields:
  - `max_batch_size` — upper bound on batch size.
  - `dynamic_batching { max_queue_delay_microseconds }` — wait window to fill batch.
  - `instance_group` — number of concurrent model instances/replicas.
- Supports model ensembles and concurrent model execution across GPUs.

## NIM (NVIDIA Inference Microservices)
- Pre-packaged, optimized containers for supported foundation models.
- Standardized (often OpenAI-compatible) API endpoints.
- Minimal configuration vs manually configuring Triton.
- Choose NIM for fast deployment of a single supported model; choose Triton for custom, multi-framework, multi-model serving.

## Training vs Inference Compute Profile
| Aspect | Training | Inference |
|---|---|---|
| Passes | Forward + backward | Forward only |
| Batch size | Large, offline | Variable, often smaller, real-time |
| Precision | Higher (FP32/BF16 mixed) | Lower (FP16/INT8/FP8) |
| Memory | Weights + activations + gradients + optimizer state | Weights + activations + KV cache |
