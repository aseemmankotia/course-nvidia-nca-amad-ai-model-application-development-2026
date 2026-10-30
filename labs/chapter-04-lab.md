# Chapter 4 Lab: Inference Concepts: Serving Models at Scale

**Estimated time:** 20 minutes

## Exercise

Given a target of 200ms p99 latency and 500 requests/sec, decide on batch size, precision (FP16 vs INT8), and whether to deploy via a single NIM endpoint or a Triton ensemble — document the tradeoffs

## Key takeaway

Inference optimization is a constant latency-throughput-cost tradeoff tuned via batching, precision, and the right serving layer (Triton/NIM).
