## Chapter 6 Cheat Sheet: Model Landscape

### Match Model Type to Task (heavily tested)
| Task | Correct Model Family | Why |
|---|---|---|
| Generate/summarize/reason over text | LLM | Next-token prediction over language |
| Semantic search / retrieval / RAG backend | Embedding model | Converts text to comparable vectors |
| Generate novel images from text prompts | Diffusion model | Iterative denoising from noise |
| Understand/generate across text+image/audio in one call | Multimodal model | Single architecture spans modalities |

**Exam trap:** A scenario mentioning 'search' or 'find similar items' is an embedding question even if it mentions chat UI — the retrieval step is still embeddings; the LLM (if present) only generates the final answer (RAG).

### Transformers & Self-Attention
- Self-attention lets every token weigh relevance of every other token, regardless of position — enables long-range context.
- Processes tokens in parallel (unlike RNNs), enabling GPU-scale training.
- Attention cost grows roughly quadratically (O(n²)) with sequence length — longer context = more compute.
- Exam note: attention is the mechanism that lets transformers handle context; it is not unique to LLMs — vision transformers and multimodal models use it too.

### Open-Weight vs Proprietary Tradeoffs
| Factor | Open-Weight (e.g., Llama, Mistral, Gemma) | Proprietary (e.g., GPT, Claude, Gemini) |
|---|---|---|
| Weight access | Full — downloadable, inspectable, modifiable | None — API only |
| Deployment | Self-hosted, on-prem/offline possible | Vendor-hosted, requires network access |
| Cost model | Infra + ops cost (fixed/variable) | Usage-based (per-token/call) |
| Control/compliance | High — can audit, fine-tune freely | Low — governed by vendor terms |
| Time to production | Slower — requires infra setup | Fast — integrate via API |

**Exam trap:** 'No internet access' or 'must audit weights' requirements always point to open-weight, even if proprietary offers a private VPC endpoint — a VPC endpoint still doesn't expose weights.

### Diffusion Model Mechanics
- Training: learns to reverse a noise-adding process over many steps.
- Inference: starts from random noise, denoises over N steps guided by a text prompt.
- Fewer inference steps → faster generation, typically lower quality/detail.
- Diffusion ≠ GAN: diffusion = iterative denoising (stable, slower); GAN = single adversarial generator pass (faster, less stable).

### Embedding Model Rules
- Output: fixed-length numeric vector representing semantic meaning.
- Vectors from different embedding models are NOT interchangeable — different geometric spaces/dimensionality.
- Switching embedding models requires re-embedding the entire corpus, not just new data.
- Higher-dimensional embeddings capture more nuance but cost more to store/compute over.

### Quick Decision Checklist
1. Does the task need generated text/reasoning? → LLM
2. Does the task need similarity/search/ranking? → Embedding model
3. Does the task need new image pixels from a prompt? → Diffusion model
4. Does the task need text+image/audio handled together? → Multimodal model
5. Does the requirement mention air-gapped/no internet/weight audit? → Open-weight
6. Does the requirement prioritize speed-to-market over control? → Proprietary
