# Chapter 3 Cheat Sheet: Data Pipelines, RAG, and the Data Flywheel

## Pipeline Stages (in order)
| Stage | Purpose |
|---|---|
| Ingestion | Pull raw data from sources (web, logs, transcripts) |
| Governance check | PII detection/redaction, compliance filtering — **before** curation |
| Cleaning | Remove malformed/corrupt/low-quality records |
| Deduplication | Remove redundant records (see dedup table) |
| Synthetic augmentation | Generate instruction/QA pairs where labeled data is scarce |
| Embedding | Convert curated text to vectors |
| Indexing | Store vectors in a vector store for retrieval |

## Deduplication Types
| Type | Method | Catches |
|---|---|---|
| Exact | Hash match | Byte-identical duplicates |
| Fuzzy | MinHash LSH | Near-duplicates (reordered/edited text) |
| Semantic | Embedding similarity | Paraphrased/conceptually identical content |

## RAG Retrieval Stack
| Layer | Role |
|---|---|
| Embedding model | Text → vector (fast, approximate recall) |
| Vector store | Stores/searches vectors (consider scale, ANN index, GPU support) |
| Reranker | Re-scores top-k candidates for precision |
| GPU-accelerated ANN search | Use for large-scale, low-latency similarity search |

## Vector Store Selection Checklist
- Scale: how many vectors (thousands vs. hundreds of millions)?
- Index type: HNSW, IVF, etc.
- GPU acceleration available?
- Metadata filtering needed (e.g., filter by date/source)?
- Update frequency: static corpus vs. continuously growing?

## Chunking Rule of Thumb
- Chunk size ≤ embedding model's max context window
- Use overlap between chunks to preserve boundary context
- Never truncate silently — truncation = information loss

## The Data Flywheel Loop
```
Production usage → Capture data (prompts, responses, feedback)
       → Curate (dedup, filter, redact PII)
       → Retrain / fine-tune model
       → Redeploy improved model
       → More usage → repeat
```
**Exam framing:** "production data improving models over time" = data flywheel.

## Feedback Loop Components
| Source | Role |
|---|---|
| Human-in-the-loop | Manual annotation/labeling of flagged outputs |
| Automated evaluation | Metrics, guardrail checks, scoring at scale |
| Combined signal | Routes low-quality outputs back into curated training data |

## Common Exam Traps
- Treating "bigger model" as the fix for bad retrieval (root cause is usually stale/dirty data).
- Confusing exact dedup with fuzzy/semantic dedup.
- Forgetting governance (PII) checks must precede curation/training ingestion.
- Assuming synthetic data generation replaces real data entirely — it **augments** scarce datasets.
- Picking "a vector database" without matching scale/latency/GPU requirements to the scenario.
