## Chapter 7: The NVIDIA AI Stack: AI Enterprise, NIM, NeMo, and Blueprints — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | What does NIM stand for and what does it provide? | NVIDIA Inference Microservices — containerized, pre-optimized model inference endpoints with standard (often OpenAI-compatible) APIs. Exam tip: NIM = deployment/inference, not training. |
| 2 | NIM vs NeMo — one-line distinction? | NIM = packaged, optimized inference microservice (deploy a model). NeMo = framework to build, customize, and align models (train/fine-tune). Exam tip: 'deploy fast' = NIM, 'customize/train' = NeMo. |
| 3 | What is NVIDIA AI Enterprise? | The supported, secure software platform layer for enterprise AI — certified builds, security patching, and support for NIM, NeMo, RAPIDS, Triton, TensorRT across cloud/on-prem/edge. Exam tip: it's the platform/support layer, not a model or app. |
| 4 | What are NVIDIA Blueprints? | Reference architectures/workflows for common GenAI and agentic use cases (RAG chatbot, digital human, customer service agent) that teams customize rather than build from scratch. Exam tip: Blueprint = starting template/workflow, not a runtime component. |
| 5 | What does RAPIDS accelerate? | GPU-accelerated data science: cuDF (dataframes), cuML (ML algorithms), cuGraph (graph analytics). Exam tip: RAPIDS fits the data preprocessing/ETL stage, not model inference serving. |
| 6 | Which NVIDIA component provides an OpenAI-compatible API for serving an LLM? | NIM microservices. Exam tip: standard API compatibility lets apps swap models with minimal code changes. |
| 7 | What NeMo sub-components handle data curation, fine-tuning, evaluation, and safety? | NeMo Curator (data curation), NeMo Customizer (fine-tuning), NeMo Evaluator (evaluation), NeMo Guardrails (safety/alignment). Exam tip: each sub-tool maps to one lifecycle stage. |
| 8 | Scenario: need fast, low-DevOps LLM deployment on-prem with container + API — which component? | NIM. It's prebuilt, optimized, and containerized for immediate deployment, unlike NeMo (training) or Blueprints (full app reference). |
| 9 | Scenario: need to quickly build an agentic RAG customer-service app using a proven design — which component? | NVIDIA Blueprint. Provides an end-to-end reference workflow combining LLM, retrieval, and guardrails that you customize. |
| 10 | What underlying tech does NIM build on for optimized inference? | Triton Inference Server and TensorRT/TensorRT-LLM. Exam tip: NIM abstracts these so you don't manually configure them. |
| 11 | Why choose NVIDIA AI Enterprise over open-source equivalents for production? | Enterprise support SLAs, security patching/CVE management, and certification across cloud/on-prem/edge — reduces operational and compliance risk. Exam tip: the value prop is support + security, not new features. |
| 12 | Where does RAPIDS sit relative to NIM/NeMo in a typical pipeline? | RAPIDS accelerates data preprocessing/feature engineering (pre-training/pre-inference); NeMo customizes/trains the model; NIM serves the model for inference. Exam tip: pipeline order is RAPIDS → NeMo → NIM. |
