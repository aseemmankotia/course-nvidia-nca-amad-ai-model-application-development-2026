## Chapter 3: Data Pipelines, RAG, and the Data Flywheel — Practice Questions

**Q1.** A company has millions of raw documents scraped from the web for LLM pretraining, containing many near-duplicate pages with minor reordering and edits. Which approach BEST reduces redundant training data at scale?

A) Exact string hash matching only
B) Manual review by data annotators
C) Increasing the model's learning rate during training
D) GPU-accelerated fuzzy deduplication using MinHash LSH (e.g., NeMo Curator)

<details>
<summary>Answer</summary>

**Correct: D**

Fuzzy dedup via MinHash LSH is purpose-built to catch near-duplicates (reordered/edited text) at web scale using GPU acceleration.

**Why the others are wrong:**
- Exact hash matching only catches byte-identical content, missing near-duplicates
- Manual review does not scale to millions of documents
- Learning rate is a training hyperparameter, unrelated to data quality

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** Which component should you choose to perform GPU-accelerated approximate nearest neighbor search over millions of embedding vectors in a RAG pipeline?

A) cuDF
B) NeMo Guardrails
C) cuVS (CUDA Vector Search)
D) TensorRT-LLM

<details>
<summary>Answer</summary>

**Correct: C**

cuVS is NVIDIA's library purpose-built for GPU-accelerated vector similarity search and integrates with vector DBs like Milvus and FAISS.

**Why the others are wrong:**
- cuDF accelerates dataframe/tabular processing, not vector search
- NeMo Guardrails enforces conversational safety policies, not retrieval
- TensorRT-LLM optimizes LLM inference, not vector similarity search

</details>

---

**Q3.** When embedding long documents that exceed the embedding model's context window for a RAG pipeline, which practice BEST preserves retrieval quality?

A) Truncate the document and embed only the first portion
B) Embed the entire document as a single vector regardless of length
C) Chunk the document into overlapping segments sized within the model's max context, then embed each chunk
D) Skip embedding and rely only on keyword search

<details>
<summary>Answer</summary>

**Correct: C**

Overlapping chunking fits within context limits while preserving semantic continuity across chunk boundaries.

**Why the others are wrong:**
- Truncation discards information from later sections of the document
- Exceeding the model's context window degrades or clips the resulting embedding
- Keyword-only search loses semantic matching, defeating the purpose of RAG

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A production support chatbot generates thousands of conversations daily. The team captures this data, curates it, uses it to retrain a smaller fine-tuned model, and redeploys it — repeating this cycle continuously. Which concept does this describe?

A) The data flywheel
B) Transfer learning
C) Quantization
D) Zero-shot prompting

<details>
<summary>Answer</summary>

**Correct: A**

This continuous capture → curate → retrain → redeploy cycle driven by production data is the textbook definition of the data flywheel.

**Why the others are wrong:**
- Transfer learning is reusing a pretrained model for a new task, not a recurring feedback loop
- Quantization reduces model precision/size and is unrelated to data loops
- Zero-shot prompting is an inference-time technique, not a data cycle

</details>

---

**Q5.** Which approach is designed to generate high-quality synthetic training data, such as instruction and Q&A pairs, to augment a scarce labeled dataset?

A) TensorRT model optimizer
B) Synthetic data generation pipelines using large generator models (e.g., Nemotron) within a curation toolkit
C) Triton Inference Server
D) NeMo Guardrails

<details>
<summary>Answer</summary>

**Correct: B**

Curation toolkits include synthetic data generation pipelines that use large generator models to produce instruction/QA pairs for fine-tuning.

**Why the others are wrong:**
- The model optimizer targets inference speed/size, not data generation
- Triton serves models for inference; it does not generate training data
- Guardrails enforces conversational policy constraints, not data generation

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** In a data flywheel, what is the PRIMARY purpose of combining human-in-the-loop feedback with automated evaluation?

A) To eliminate the need for any future model retraining
B) To replace the need for a vector database
C) To continuously identify low-quality or incorrect model outputs and route them into curated training data for improvement
D) To reduce GPU costs during inference

<details>
<summary>Answer</summary>

**Correct: C**

Human and automated feedback signals surface poor outputs so they can be curated and fed back into training, driving continuous improvement.

**Why the others are wrong:**
- The feedback loop supports retraining; it doesn't eliminate it
- Vector databases are unrelated to feedback evaluation
- This is a quality mechanism, not primarily a cost-optimization technique

</details>

---

**Q7.** After six months in production, a RAG system increasingly retrieves outdated and duplicate chunks, lowering answer quality. Which action addresses the ROOT cause before re-embedding anything?

A) Run a data curation pass: deduplicate, filter low-quality content, and refresh stale documents in the source corpus
B) Switch to a larger LLM
C) Increase the number of retrieved chunks (top-k)
D) Disable retrieval and rely solely on the LLM's parametric knowledge

<details>
<summary>Answer</summary>

**Correct: A**

The root cause is a degraded knowledge base; curating (dedup, quality filter, refresh) the source corpus fixes the data feeding the retriever.

**Why the others are wrong:**
- A larger LLM does not fix poor-quality retrieved context
- Retrieving more low-quality chunks does not improve relevance
- Disabling retrieval increases hallucination risk and defeats the purpose of RAG

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which data governance check should be applied BEFORE ingesting customer support transcripts into a corpus used for fine-tuning?

A) Increasing training batch size
B) Converting weights to FP16
C) PII detection and redaction
D) Adding more attention heads to the model

<details>
<summary>Answer</summary>

**Correct: C**

PII detection and redaction is a governance/compliance step required before sensitive user data enters a training corpus.

**Why the others are wrong:**
- Batch size is a training hyperparameter, not a governance check
- FP16 conversion is a model precision/performance setting, not governance
- Attention head count is a model architecture decision, not a data governance step

</details>

---

