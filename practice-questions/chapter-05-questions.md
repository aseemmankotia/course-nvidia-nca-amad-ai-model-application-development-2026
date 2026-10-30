## Chapter 5: Customization Spectrum: Prompting, RAG, PEFT, and Alignment — Practice Questions

**Q1.** A company's internal knowledge base is updated daily with new policy documents. They need a chatbot that answers questions using the latest content, with zero GPU training budget. Which approach BEST meets these requirements?

A) Full fine-tuning the base model weekly on the updated documents
B) Retrieval-Augmented Generation (RAG) over a vector store of the documents
C) LoRA fine-tuning retrained nightly on the document diffs
D) Prompt engineering with the entire document set pasted into every prompt

<details>
<summary>Answer</summary>

**Correct: B**

RAG injects current knowledge at query time via retrieval, so updates require only re-indexing documents, not retraining — matching the daily-update, zero-training-budget constraint.

**Why the others are wrong:**
- Full fine-tuning weekly is extremely costly and still stale between retraining cycles, violating the budget constraint.
- LoRA still requires a training pipeline and GPU compute nightly, which the budget does not allow.
- Pasting entire document sets into every prompt is not scalable, exceeds context window limits, and increases latency/cost per call.

</details>

---

**Q2.** A team has 5,000 labeled (instruction, desired-response) pairs and needs the model to consistently follow a specific JSON output format across many different task types. Which technique directly addresses this requirement?

A) Few-shot prompting with two examples per request
B) RAG with the format spec stored as a retrievable document
C) Training a new model from scratch on the 5,000 pairs
D) Instruction tuning (supervised fine-tuning on the instruction-response pairs)

<details>
<summary>Answer</summary>

**Correct: D**

Instruction tuning uses labeled instruction-response pairs to teach consistent behavior and formatting across tasks, which is exactly the available data and the stated goal.

**Why the others are wrong:**
- Few-shot prompting is less reliable at scale across many task types and doesn't persist the behavior without repeating examples each call.
- RAG injects knowledge, not behavioral/formatting consistency — retrieving the spec doesn't guarantee the model follows it.
- Training from scratch with only 5,000 examples is wildly insufficient data and unnecessarily expensive.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** An engineering team wants to adapt a 70B-parameter pretrained LLM to a niche legal domain but has only a single GPU with limited memory and wants to preserve the ability to reuse the original base weights for other tasks. Which technique should they select?

A) Full fine-tuning of all 70B parameters
B) LoRA (parameter-efficient fine-tuning)
C) Pretraining a new 70B model on legal text
D) Prompt engineering only, with no parameter updates

<details>
<summary>Answer</summary>

**Correct: B**

LoRA freezes the base weights and trains small low-rank adapter matrices, drastically reducing memory/compute needs while keeping the original model reusable for other tasks.

**Why the others are wrong:**
- Full fine-tuning of all 70B parameters requires far more GPU memory than a single limited-memory GPU can provide.
- Pretraining from scratch is astronomically more expensive and unnecessary for domain adaptation.
- Prompt engineering alone cannot inject the deep domain-specific behavior needed for a specialized legal task at this scale of adaptation requirement.

</details>

---

**Q4.** After instruction tuning, a model follows tasks correctly but sometimes produces responses that are technically correct yet unhelpful or mildly unsafe. The team has collected pairs of human preference rankings (response A preferred over response B). Which technique category should be applied next?

A) Additional RAG indexing of safety guidelines
B) Increase prompt length with more few-shot examples
C) Alignment via RLHF or DPO using the preference data
D) Retrain from scratch with a larger pretraining corpus

<details>
<summary>Answer</summary>

**Correct: C**

RLHF and DPO are alignment techniques designed specifically to shape model behavior using human preference comparison data, improving helpfulness and safety beyond instruction tuning.

**Why the others are wrong:**
- RAG addresses knowledge retrieval, not behavioral alignment toward human preferences.
- More few-shot examples cannot reliably instill preference-based behavior changes across diverse unseen prompts.
- Retraining from scratch is cost-prohibitive and does not directly leverage the preference-ranked data collected.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** In a LoRA configuration, what is the direct effect of increasing the rank parameter r?

A) It increases the number of trainable parameters, giving more capacity but higher overfitting/compute risk
B) It reduces the number of trainable parameters and lowers overfitting risk
C) It has no effect on parameter count, only on inference latency
D) It converts the LoRA adapter into a full fine-tuning update

<details>
<summary>Answer</summary>

**Correct: A**

Rank r controls the dimensionality of the low-rank matrices A and B; higher r means more trainable parameters, increasing model capacity but also increasing compute cost and overfitting risk on small datasets.

**Why the others are wrong:**
- This is the opposite effect — increasing r increases, not reduces, trainable parameters.
- Rank directly scales parameter count, so it is not parameter-count-neutral.
- LoRA remains a low-rank update regardless of r; it does not become full fine-tuning since the base weights stay frozen.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** A startup wants to validate whether an LLM can summarize support tickets but has only 15 example tickets, zero fine-tuning budget, and needs a working prototype by tomorrow. Which approach should they start with?

A) Few-shot prompt engineering using the 15 examples as in-context demonstrations
B) Full fine-tuning on the 15 examples
C) LoRA fine-tuning on the 15 examples
D) Train a reward model and run RLHF

<details>
<summary>Answer</summary>

**Correct: A**

With minimal data, zero budget, and a tight timeline, prompt engineering (few-shot) is the lowest-cost, fastest-to-deploy option and is appropriate given the data volume is far too small for training-based approaches.

**Why the others are wrong:**
- Full fine-tuning on only 15 examples would badly overfit and requires training infrastructure the team doesn't have time/budget for.
- LoRA still requires a training loop and GPU access; 15 examples is also insufficient for meaningful adapter training.
- RLHF requires substantial preference data and a multi-stage pipeline, far exceeding the available time and budget.

</details>

---

**Q7.** What is the key conceptual difference between DPO (Direct Preference Optimization) and RLHF (Reinforcement Learning from Human Feedback)?

A) DPO requires more human-labeled data than RLHF
B) DPO only works on vision models while RLHF only works on language models
C) DPO optimizes the policy directly on preference pairs without training a separate reward model or running an RL loop, while RLHF requires both
D) DPO and RLHF are identical techniques with different names

<details>
<summary>Answer</summary>

**Correct: C**

DPO reformulates preference optimization as a direct supervised-style loss on preference pairs, eliminating the need for a separate reward model and PPO-based RL loop that RLHF requires, making it simpler and more stable.

**Why the others are wrong:**
- DPO and RLHF typically use the same type of preference-pair datasets; data volume is not the distinguishing factor.
- Both techniques are applied to language models; neither is restricted to vision models.
- They are distinct methods — DPO is explicitly a simplification that removes RLHF's reward model and RL optimization stages.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** A team needs to customize a model's tone and reduce hallucinations on proprietary product specs that change weekly, with a small engineering team and no dedicated ML training infrastructure. Which decision-framework factor MOST strongly points them away from fine-tuning and toward RAG?

A) The model's parameter count being too small for fine-tuning
B) The need to reduce inference latency below 10ms
C) The high frequency of data change combined with lack of training infrastructure
D) The requirement for multi-language support

<details>
<summary>Answer</summary>

**Correct: C**

Frequently changing data paired with no training infrastructure is the classic signal in the decision framework favoring RAG, since retraining/fine-tuning cadence cannot keep pace and infra isn't available to support it.

**Why the others are wrong:**
- Parameter count is not the deciding factor here — even small models can be fine-tuned; the issue is data volatility and lack of infra.
- RAG typically adds retrieval latency compared to a purely fine-tuned model, so this factor would actually argue against RAG, not for it.
- Multi-language support isn't a factor distinguishing RAG from fine-tuning in the core decision framework for this scenario.

</details>

---

