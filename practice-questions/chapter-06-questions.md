## Chapter 6: The Model Landscape: LLMs, Multimodal, Embeddings, and Diffusion — Practice Questions

**Q1.** A retail company has 2 million product descriptions and wants to let customers search by meaning (e.g., 'warm jacket for hiking' returns relevant items even without exact keyword matches). Which model type should they deploy to power the search index?

A) A large language model fine-tuned for text generation
B) An embedding model to vectorize descriptions and queries
C) A diffusion model to visualize matching products
D) A multimodal model combining text and image inputs

<details>
<summary>Answer</summary>

**Correct: B**

Embedding models convert text into fixed-size vectors so semantic similarity can be computed via vector search — this is the purpose-built tool for retrieval tasks.

**Why the others are wrong:**
- An LLM generates text; it is not optimized to produce comparable numeric similarity scores for a large corpus efficiently.
- Diffusion models generate images from noise and have no role in text search relevance.
- A multimodal model adds image/audio handling the scenario doesn't require, adding cost and complexity without solving the core retrieval need.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A marketing team needs to generate novel product photos from text prompts (e.g., 'red sneaker on a beach at sunset') with no real photo source images. Which model family BEST fits this task?

A) Embedding model
B) Diffusion model
C) Large language model
D) Transformer-based classification model

<details>
<summary>Answer</summary>

**Correct: B**

Diffusion models are the current standard architecture for text-to-image synthesis, iteratively denoising random noise into a coherent image matching a prompt.

**Why the others are wrong:**
- Embedding models only produce vectors for similarity, not pixel output.
- LLMs generate text tokens, not images, unless paired with a separate image generator.
- A classification model assigns labels to existing inputs; it does not synthesize new images.

</details>

---

**Q3.** A company must deploy a model fully on-premises with no outbound internet access, and needs the ability to inspect and modify model weights for compliance auditing. Which approach meets these requirements?

A) Use an open-weight model downloaded and hosted on internal infrastructure
B) Use a proprietary API-based model with a signed enterprise agreement
C) Use a proprietary model through a private VPC endpoint
D) Use a multimodal proprietary model with data residency guarantees

<details>
<summary>Answer</summary>

**Correct: A**

Open-weight models provide downloadable weights that can run fully offline and be inspected/modified, satisfying both the no-internet and weight-audit requirements.

**Why the others are wrong:**
- Proprietary API models require network calls to the vendor, violating the no-internet constraint.
- A private VPC endpoint still depends on vendor-hosted infrastructure and does not expose weights for inspection.
- Data residency guarantees address storage location, not the requirement to inspect or modify model weights.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** An application must accept a photo of a receipt and answer natural-language questions about its contents (e.g., 'What was the total?') in a single model call. Which model type is the correct choice?

A) Embedding model
B) Diffusion model
C) Multimodal model
D) Single-modality text LLM

<details>
<summary>Answer</summary>

**Correct: C**

A multimodal model accepts both image and text inputs within one architecture, enabling direct visual question answering without a separate OCR or vision pipeline.

**Why the others are wrong:**
- Embedding models return vectors, not natural-language answers.
- Diffusion models generate images; they don't interpret or answer questions about image content.
- A text-only LLM cannot directly process the image input without an external vision component.

</details>

---

**Q5.** A team migrates their vector database to a new embedding model with a different output dimensionality than the previous model, but only re-embeds newly added documents going forward. What is the MOST likely result?

A) Search quality improves immediately for all documents
B) Old and new vectors become incompatible, degrading or breaking similarity search
C) The vector database automatically rescales dimensions to match
D) No impact occurs since embeddings are model-agnostic

<details>
<summary>Answer</summary>

**Correct: B**

Embedding vectors from different models occupy different geometric spaces and dimensionalities; mixing them in one index corrupts similarity comparisons.

**Why the others are wrong:**
- Mixing incompatible vectors does not improve quality — it introduces inconsistency.
- Vector databases do not automatically reconcile differing embedding spaces or dimensions.
- Embeddings are explicitly model-specific; they are not interchangeable across models.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A developer reduces a diffusion model's inference steps from 50 to 10 to speed up an image generation API. What tradeoff should they expect?

A) Faster generation with no change in image quality
B) Faster generation with likely reduced image quality/detail
C) Slower generation with improved image quality
D) No change in speed, only a change in output resolution

<details>
<summary>Answer</summary>

**Correct: B**

Diffusion models iteratively denoise an image; fewer steps mean less refinement, which generally trades speed for lower fidelity or more artifacts.

**Why the others are wrong:**
- Reducing steps virtually always impacts quality to some degree, so 'no change' is incorrect.
- Fewer steps reduces compute time, so generation becomes faster, not slower.
- Step count affects denoising iterations, not output resolution, which is typically a separate parameter.

</details>

---

**Q7.** What is the primary role of the self-attention mechanism within a transformer architecture?

A) Compressing input sequences into a single fixed-length vector before processing
B) Replacing the need for any numerical embeddings of input tokens
C) Allowing each token to weigh the relevance of every other token in the sequence, regardless of distance
D) Generating random noise vectors used for image synthesis

<details>
<summary>Answer</summary>

**Correct: C**

Self-attention computes relevance scores between all token pairs in a sequence, enabling the model to capture long-range dependencies without sequential processing.

**Why the others are wrong:**
- That describes older sequence-to-sequence compression approaches, not self-attention itself.
- Transformers still rely on token embeddings as input; attention operates on top of them, not instead of them.
- Noise generation is a diffusion model concept, unrelated to transformer attention.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A startup wants to minimize operational overhead and go to production quickly, accepting ongoing per-token usage costs and no access to model internals. Which approach BEST matches this priority?

A) Self-host an open-weight model on owned GPU servers
B) Call a proprietary model via a hosted API
C) Fine-tune an open-weight model and deploy it on a managed Kubernetes cluster
D) Train a custom transformer model from scratch

<details>
<summary>Answer</summary>

**Correct: B**

Proprietary API models require no infrastructure management and allow immediate integration, at the cost of per-usage fees and no weight access — matching the stated priorities.

**Why the others are wrong:**
- Self-hosting an open-weight model requires significant infrastructure setup and ongoing GPU management, contradicting 'minimize operational overhead.'
- Fine-tuning and managing Kubernetes adds substantial engineering overhead, not a quick path to production.
- Training a transformer from scratch requires massive data, compute, and time — the opposite of 'quickly.'

</details>

---

