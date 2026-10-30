## Chapter 7: The NVIDIA AI Stack: AI Enterprise, NIM, NeMo, and Blueprints — Practice Questions

**Q1.** A company wants to deploy a pre-optimized LLM inference endpoint with minimal custom coding, exposing an OpenAI-compatible API, while keeping access to enterprise security patches. Which NVIDIA component should they use?

A) NVIDIA NIM
B) NeMo Curator
C) RAPIDS cuDF
D) NVIDIA Blueprint for RAG

<details>
<summary>Answer</summary>

**Correct: A**

NIM packages optimized models as ready-to-run containerized microservices with standard APIs, requiring no custom inference code.

**Why the others are wrong:**
- NeMo Curator handles data curation for training, not inference serving.
- RAPIDS cuDF accelerates dataframe operations for data science, not LLM inference.
- A Blueprint is a full reference app workflow, heavier than needed for just an inference endpoint.

</details>

---

**Q2.** Which NVIDIA offering provides the enterprise-grade support, security patching, and certification needed to run AI software in production across cloud, on-prem, and edge environments?

A) NVIDIA AI Enterprise
B) NIM
C) NeMo
D) RAPIDS

<details>
<summary>Answer</summary>

**Correct: A**

NVIDIA AI Enterprise is the supported software platform layer delivering certified builds, patching, and SLAs for the full stack.

**Why the others are wrong:**
- NIM is a packaged inference microservice, not the overarching support platform.
- NeMo is a model-building/customization framework, not a support/certification layer.
- RAPIDS is a data-science acceleration library suite, unrelated to enterprise support.

</details>

---

**Q3.** A team needs to fine-tune a foundation model on proprietary company data and add safety guardrails before deployment. Which framework is designed for this?

A) NIM
B) NVIDIA Blueprints
C) NeMo
D) RAPIDS

<details>
<summary>Answer</summary>

**Correct: C**

NeMo includes Customizer for fine-tuning and Guardrails for alignment/safety, matching exactly this requirement.

**Why the others are wrong:**
- NIM is for serving an already-built model, not training or aligning it.
- Blueprints are reference app workflows, not a model customization toolkit.
- RAPIDS accelerates data science workloads like dataframes and ML, not LLM fine-tuning.

</details>

---

**Q4.** Which NVIDIA offering provides a customizable reference architecture (e.g., for a RAG chatbot) that teams adapt instead of building the entire application from scratch?

A) NIM
B) NeMo
C) AI Enterprise
D) NVIDIA Blueprint

<details>
<summary>Answer</summary>

**Correct: D**

Blueprints are pre-built, end-to-end reference workflows for common GenAI/agentic use cases that developers customize.

**Why the others are wrong:**
- NIM is one serving component, not a full application reference architecture.
- NeMo builds/customizes individual models, not complete app workflows.
- AI Enterprise is the support/platform layer underneath these components, not an app template.

</details>

---

**Q5.** When deploying a NIM microservice container for an LLM, which API format is typically exposed by default to maximize compatibility with existing LLM application tooling?

A) gRPC only, no REST
B) OpenAI-compatible REST API
C) GraphQL
D) SOAP

<details>
<summary>Answer</summary>

**Correct: B**

NIM exposes industry-standard, OpenAI-compatible endpoints so applications built for OpenAI-style APIs can swap in NIM with minimal code changes.

**Why the others are wrong:**
- NIM does support gRPC in addition to REST, so 'gRPC only' is incorrect.
- GraphQL is not the standard interface NIM exposes for LLM inference.
- SOAP is a legacy protocol not used by NIM microservices.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A company wants to deploy a chatbot using a packaged, pre-optimized LLM with minimal DevOps overhead, as a Docker container with a standard API, running on their own on-prem GPU cluster. Which is the BEST fit?

A) Build a custom inference server directly with TensorRT-LLM
B) NVIDIA NIM microservice
C) NeMo Customizer for fine-tuning
D) RAPIDS cuML for inference

<details>
<summary>Answer</summary>

**Correct: B**

NIM is exactly this: a prebuilt, optimized, containerized inference microservice with a standard API, minimizing DevOps work.

**Why the others are wrong:**
- Building directly on TensorRT-LLM recreates what NIM already provides, adding unnecessary engineering effort.
- NeMo Customizer is for fine-tuning/training, not for deploying a ready model for inference.
- RAPIDS cuML is a GPU-accelerated ML algorithm library for data science, not an LLM inference server.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** What is the primary distinction between NVIDIA NIM and NeMo?

A) NIM is for data curation while NeMo is for inference
B) NIM packages optimized models for inference deployment; NeMo is for building, customizing, and aligning models
C) NIM and NeMo are identical products marketed under different names
D) NIM is open-source while NeMo requires an enterprise license

<details>
<summary>Answer</summary>

**Correct: B**

This captures the lifecycle split: NeMo covers build/train/align, NIM covers packaged deployment/inference.

**Why the others are wrong:**
- This reverses the actual roles — NeMo handles data curation/training, not NIM.
- They serve distinct purposes in the AI lifecycle and are not interchangeable.
- Licensing details are not the defining technical distinction tested by the exam here.

</details>

---

**Q8.** An enterprise wants to quickly build an agentic customer-service application that already integrates an LLM, retrieval, and guardrails, then customize it for their brand. Which NVIDIA offering should they start from?

A) NVIDIA AI Enterprise license alone
B) RAPIDS accelerator suite
C) A single standalone NIM microservice
D) An NVIDIA Blueprint (e.g., customer service reference workflow)

<details>
<summary>Answer</summary>

**Correct: D**

Blueprints are complete, pre-integrated reference workflows for exactly these multi-component GenAI/agentic scenarios.

**Why the others are wrong:**
- AI Enterprise provides support/certification but not an integrated application workflow itself.
- RAPIDS accelerates data science pipelines, unrelated to agentic app orchestration.
- A single NIM microservice handles inference only, not the full RAG + guardrails + orchestration stack.

</details>

---

