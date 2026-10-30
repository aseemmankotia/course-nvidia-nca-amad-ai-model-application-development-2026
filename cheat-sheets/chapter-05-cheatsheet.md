# Customization Spectrum Cheat Sheet

## Decision Framework (cost/complexity ascending)
| Technique | Data Needed | Training Required | Updates Knowledge? | Updates Behavior/Style? | Best For |
|---|---|---|---|---|---|
| Prompt Engineering | None–few examples | No | No | Limited (via instructions) | Quick prototypes, low budget |
| RAG | Document corpus (any size) | No (just indexing) | Yes (external, current) | No | Frequently changing facts, citations needed |
| PEFT (LoRA/Adapters) | Hundreds–thousands examples | Yes (lightweight) | Partial | Yes | Domain adaptation, limited compute |
| Instruction Tuning | Thousands of (instruction, response) pairs | Yes (full or PEFT) | Partial | Yes (strong) | Consistent task-following/format |
| Alignment (RLHF/DPO) | Preference-ranked pairs | Yes (post-SFT) | No | Yes (preference-shaped) | Helpfulness/safety tuning |
| Full Fine-Tuning | Large labeled dataset | Yes (expensive) | Yes | Yes | Deep task specialization |
| Full Pretraining | Massive raw corpus | Yes (extremely expensive) | Yes (foundational) | Yes (foundational) | Building a new base model |

## LoRA Essentials
- Freezes base weights W; trains low-rank matrices A, B: `W' = W + BA`
- Rank `r` controls trainable params: higher r → more capacity, more overfitting/compute risk
- Merge-able post-training → zero added inference latency
- Adapters differ: add new bottleneck layers with nonlinearities → adds inference latency, not mergeable

## Alignment: RLHF vs DPO
| Aspect | RLHF | DPO |
|---|---|---|
| Reward model | Required (separate) | Not required |
| Optimization | RL loop (e.g., PPO) | Direct supervised-style loss on preference pairs |
| Complexity/Stability | Higher complexity, less stable | Simpler, more stable |
| Data | Preference pairs | Preference pairs (same format) |

## Quick Decision Rules
- Facts change often, no training infra → **RAG**
- Need consistent format/behavior across tasks, have labeled pairs → **Instruction Tuning**
- Limited compute/memory, want reusable base model → **LoRA/PEFT**
- Model follows tasks but output lacks helpfulness/safety, have preference data → **RLHF/DPO**
- Tiny dataset, no budget, need prototype fast → **Prompt Engineering**
- Need new foundational capability not in any pretrained model → **Full Pretraining** (last resort, highest cost)

## Common Exam Traps
- Choosing fine-tuning when RAG fits better (frequently changing data = RAG signal)
- Confusing instruction tuning (behavior) with RAG (knowledge)
- Thinking DPO requires a reward model (it does not)
- Believing higher LoRA rank always improves results without acknowledging overfitting/compute trade-off
- Assuming adapters and LoRA are interchangeable (adapters add latency; LoRA can be merged)
