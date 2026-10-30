## Chapter 1: NCA-AMAD Exam Blueprint and the AI Application Lifecycle — Practice Questions

**Q1.** A candidate preparing for NCA-AMAD is told by a colleague that the exam includes a live, proctor-watched coding lab where you must deploy a model on real GPU infrastructure. The candidate wants to confirm this before building a study plan. What is the correct format of the actual certification exam?

A) 50-60 multiple-choice questions delivered in a 60-minute online proctored session, with no live hands-on deployment required during the exam itself
B) A 2-hour practical exam where the candidate must deploy and fine-tune a model on NVIDIA DGX hardware
C) An open-book take-home project graded by NVIDIA engineers over one week
D) An in-person lab exam at an NVIDIA certified testing center requiring physical GPU access

<details>
<summary>Answer</summary>

**Correct: A**

NCA-AMAD, like other NVIDIA Certified Associate exams, is a scored multiple-choice test (50-60 items, 60 minutes) taken online via remote proctoring. Hands-on labs are part of exam preparation/training, not the scored exam event.

**Why the others are wrong:**
- There is no live GPU deployment task scored during the exam window
- NVIDIA NCA exams are not take-home or project-graded assessments
- The exam is delivered remotely online, not at a physical testing center requiring hardware access

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A candidate passed the NCA-AMAD exam exactly two years ago and has not retaken any NVIDIA exam since. Their badge status now shows as expired. What must they do to regain active certified status?

A) Retake and pass the current version of the NCA-AMAD exam (or its designated successor) to recertify
B) Submit a renewal fee only, with no retest required, since the badge auto-renews
C) Wait one additional year, after which the certification automatically reactivates
D) Complete a free online refresher course instead of retaking the exam

<details>
<summary>Answer</summary>

**Correct: A**

NVIDIA Certified Associate credentials carry a two-year validity period. Recertification requires passing the current exam again before or after expiration; there is no fee-only renewal path.

**Why the others are wrong:**
- NVIDIA does not offer a pay-to-renew option without retesting
- Certifications do not auto-reactivate with time; an exam attempt is required
- A refresher course alone does not satisfy recertification; a passing exam score is required

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A team has a fine-tuned LLM ready and now needs to expose it as a low-latency inference endpoint for a production chatbot, without writing custom serving infrastructure from scratch. Which lifecycle stage and corresponding NVIDIA tool BEST fit this need?

A) Train stage, using NVIDIA TAO Toolkit to retrain the model from scratch
B) Customize stage, using NeMo Customizer to apply additional LoRA adapters
C) Serve stage, using NVIDIA NIM microservices for optimized inference deployment
D) Consume stage, using a third-party chat UI framework with no NVIDIA tooling

<details>
<summary>Answer</summary>

**Correct: C**

Exposing an already-trained/customized model as a production inference endpoint maps to the 'Serve' stage of the lifecycle, and NVIDIA NIM is purpose-built prepackaged inference microservices for this.

**Why the others are wrong:**
- Retraining from scratch is unnecessary work and belongs to the Train stage, not what's needed here
- The model is already fine-tuned; Customize stage work is already complete
- Consume stage is where end-user applications call the endpoint, not where the endpoint itself is built

</details>

---

**Q4.** Which NVIDIA tool is purpose-built for applying parameter-efficient fine-tuning (such as LoRA/PEFT) to a foundation model during the Customize stage of the AI application lifecycle?

A) NVIDIA Triton Inference Server
B) NVIDIA TensorRT-LLM
C) NVIDIA RAPIDS
D) NVIDIA NeMo Customizer

<details>
<summary>Answer</summary>

**Correct: D**

NeMo Customizer is the NVIDIA microservice/toolkit designed specifically for fine-tuning and adapter-based customization (LoRA, PEFT) of foundation models.

**Why the others are wrong:**
- Triton is a model-serving runtime, used in the Serve stage, not for fine-tuning
- TensorRT-LLM optimizes trained models for fast inference, it does not perform fine-tuning
- RAPIDS is a GPU-accelerated data science/ETL library, unrelated to LLM fine-tuning

</details>

---

**Q5.** An application developer builds a RAG-based assistant that calls an already-deployed NIM inference endpoint and adds prompt templates and retrieval logic on top. Which lifecycle stage does this developer's work primarily belong to?

A) Train
B) Customize
C) Serve
D) Consume

<details>
<summary>Answer</summary>

**Correct: D**

Building application-layer logic (prompting, retrieval, orchestration) on top of an already-served model endpoint is the 'Consume' stage — using the model's capabilities within an end-user application.

**Why the others are wrong:**
- Train involves building/updating model weights from data, not calling an endpoint
- Customize involves adapting model weights or behavior via fine-tuning, not application logic
- Serve is the act of deploying/hosting the inference endpoint itself, already completed here

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** With 50-60 questions to answer within a 60-minute NCA-AMAD exam session, roughly how much time should a candidate budget per question to finish with review time remaining?

A) About 3 minutes per question
B) About 1 minute per question, leaving a buffer for flagged-question review
C) About 10 minutes per question
D) There is no time limit per question since the exam is untimed overall

<details>
<summary>Answer</summary>

**Correct: B**

60 minutes split across 50-60 questions averages roughly one minute per question; pacing near this rate leaves buffer time to flag and revisit uncertain items before submission.

**Why the others are wrong:**
- 3 minutes per question would require 150-180 minutes total, far exceeding the 60-minute limit
- 10 minutes per question is wildly outside the fixed 60-minute window
- The exam has a hard overall 60-minute time limit, it is not untimed

</details>

---

**Q7.** Before starting a remote-proctored NCA-AMAD exam session via Certiverse, which of the following is a standard requirement the candidate must satisfy?

A) Install a physical NVIDIA GPU on the testing machine to verify hardware competency
B) Submit a notarized letter from an employer confirming AI job experience
C) Pre-download and run a sample model inference script as a proctor checkpoint
D) Present a government-issued photo ID and allow webcam/room monitoring for identity and environment verification

<details>
<summary>Answer</summary>

**Correct: D**

Remote online proctoring (via Certiverse) requires standard identity verification with a photo ID and webcam-based monitoring of the candidate and testing environment before and during the exam.

**Why the others are wrong:**
- No local GPU hardware is required since the exam is multiple-choice, not a hands-on deployment task
- No employer letter or job experience proof is required to sit the exam
- There is no scripted inference task as part of the proctoring check-in process

</details>

---

**Q8.** In the AI application lifecycle taught in NCA-AMAD, what is the key distinction between the 'Train' stage and the 'Customize' stage?

A) Train and Customize are the same stage, just different names used interchangeably
B) Train only applies to NLP models while Customize only applies to vision models
C) Train builds a model's foundational weights from large-scale data; Customize adapts an already-trained model's behavior for a specific use case (e.g., fine-tuning, adapters) without building it from scratch
D) Customize always precedes Train in the lifecycle sequence

<details>
<summary>Answer</summary>

**Correct: C**

Train refers to creating a model's base weights via large-scale pretraining; Customize refers to adapting an existing pretrained/foundation model to a narrower task or domain, typically via fine-tuning, LoRA, or prompt-based techniques.

**Why the others are wrong:**
- They are distinct stages with different inputs, costs, and tooling, not interchangeable terms
- Both stages apply across modalities (text, vision, multimodal), not restricted by domain type
- Customize logically follows Train (you customize an already-trained base model), not the reverse order

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

