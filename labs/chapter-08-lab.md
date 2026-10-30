# Chapter 8 Lab: Sizing and Configuration: Right-Sizing GPUs for AI Workloads

**Estimated time:** 20 minutes

## Exercise

Given a 13B-parameter model, calculate approximate GPU memory needed at FP16 (~2 bytes/param) for inference-only vs training (which also needs optimizer states/gradients), then pick an appropriately sized GPU configuration from a provided spec sheet

## Key takeaway

Always size GPU memory for the full workload — training needs gradients and optimizer states on top of weights, and inference serving needs headroom for traffic scaling.
