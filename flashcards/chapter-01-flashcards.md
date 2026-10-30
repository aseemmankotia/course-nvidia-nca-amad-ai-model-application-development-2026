## Chapter 1: NCA-AMAD Exam Blueprint and the AI Application Lifecycle — Flashcards

| # | Front (Question) | Back (Answer) |
|---|-----------------|---------------|
| 1 | NCA-AMAD exam question count and time limit? | 50-60 multiple-choice questions, 60 minutes total. Exam tip: budget ~1 min/question, flag unsure ones for review. |
| 2 | NCA-AMAD certification validity period? | 2 years from pass date. Exam tip: recertification requires retaking the current exam version — no fee-only renewal. |
| 3 | What proctoring platform is used for NVIDIA NCA exam delivery? | Certiverse — online remote-proctored, requires photo ID + webcam/room check before exam start. |
| 4 | Does the NCA-AMAD exam include a live hands-on lab during the test itself? | No. It is multiple-choice only. Hands-on labs are for preparation/training, not scored during the exam session. |
| 5 | AI lifecycle stage: 'Train' | Builds foundational model weights from large-scale raw data (pretraining). Exam tip: heaviest compute/data stage, not where most app developers work. |
| 6 | AI lifecycle stage: 'Customize' | Adapts an existing pretrained model to a specific task/domain via fine-tuning, LoRA/PEFT, or prompt customization — no training from scratch. |
| 7 | AI lifecycle stage: 'Serve' | Deploys a trained/customized model as a running, callable inference endpoint optimized for latency/throughput (e.g., via NIM, Triton). |
| 8 | AI lifecycle stage: 'Consume' | Application layer that calls a served model endpoint (prompting, RAG, orchestration) to deliver end-user functionality. |
| 9 | NVIDIA TAO Toolkit vs NeMo Customizer — when to use which? | TAO Toolkit: transfer learning mainly for vision/perception models. NeMo Customizer: fine-tuning (LoRA/PEFT) for LLMs/generative models. Exam tip: match modality to tool. |
| 10 | NVIDIA NIM vs Triton Inference Server — key difference? | NIM: prepackaged, optimized inference microservices for specific foundation models (fast to deploy). Triton: general-purpose model serving runtime supporting multiple frameworks/backends. Exam tip: NIM = speed-to-deploy, Triton = flexibility/control. |
| 11 | What must happen for an expired NCA-AMAD certification to become active again? | Candidate must pass the current version of the exam (or its official successor). No grace extension or auto-renewal exists. |
| 12 | How should study time be allocated across exam domains? | Proportionally to each domain's published exam weight (per official exam guide) — heavier-weighted domains get more study hours, not equal time per domain. |
