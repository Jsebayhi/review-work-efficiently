# Theoretical Foundations of Adversarial Agentic Falsification

This document details the academic literature, empirical cognitive failure modes, and epistemological frameworks underpinning the **Review Work Efficiently** architecture.

---

## 1. The Core Problem: Why LLM Self-Review Fails

In single-agent software development and autonomous reasoning, relying on a model to review its own generated artifacts consistently fails due to three mathematically and empirically documented phenomena:

### A. Degeneration-of-Thought (DoT) in Sequential Reasoning
* **Literature Reference:** Li et al. (2023) - *Degeneration-of-Thought: How Large Language Models Fall into Repetitive and Narrow Cognitive Loops*.
* **Mechanism:** When an autoregressive model evaluates its own reasoning within the same context window, subsequent token generation is strongly conditioned on earlier tokens. The model experiences a collapse in cognitive entropy, becoming trapped in the local minimum established during generation.
* **Empirical Consequence:** The model cannot conceptualize that its initial premise was flawed. It rationalizes edge-case failures as intentional trade-offs.

### B. Machine Sycophancy and Social Conformity
* **Literature References:** 
  * Sharma et al. (2023) - *Towards Understanding Sycophancy in Large Language Models*.
  * Perez et al. (2022) - *Discovering Language Model Behaviors with Model-Written Evaluations*.
  * Wei et al. (2023) - *Simple Synthetic Data Reduces Sycophancy in Large Language Models*.
* **Mechanism:** Reinforcement Learning from Human Feedback (RLHF) optimizes models to generate agreeable, non-confrontational responses. When asked to evaluate an artifact produced by a peer or the author, models exhibit a strong prior toward politeness, cosmetic praise, and minor aesthetic suggestions (variable renaming, formatting) rather than reporting severe runtime failures or conceptual bugs.
* **Empirical Consequence:** In-prompt reviews default to polite praise (*"Looks great! Just a couple of minor comments..."*), hiding catastrophic failure modes.

### C. The Limits of Single-Agent Self-Correction
* **Literature Reference:** Huang et al. (2023) - *Large Language Models Cannot Self-Correct Reasoning Yet*.
* **Mechanism:** Without external ground truth, oracle verification, or genuine perspective diversity, single-agent "self-refine" loops frequently degrade performance or swap one hallucination for another. A model lacks the epistemic distance required to falsify its own output.

---

## 2. Epistemological Framework: Popperian Falsificationism

The architecture replaces naive verification (*"Confirm that this artifact works"*) with Karl Popper's epistemology of **Critical Rationalism (Conjectures and Refutations)**:

* **Conjecture:** The artifact created by the primary agent (code, contract, tax filing, essay) is treated purely as a tentative hypothesis.
* **Falsification Mandate:** The reviewer's sole objective is to aggressively attempt to falsify the hypothesis by locating counterexamples, unhandled states, or exploit paths.
* **Proof-of-Failure (PoF) Contract:** A finding is epistemically valid if and only if it provides a concrete proof of failure (an exploit payload, a missing test case with a failing precondition, an exact line discrepancy, or an unhandled exception trace). Speculation and stylistic advice are rejected.

---

## 3. The Context Quarantine Principle

* **Mechanism:** Anchoring bias and information cascades occur when sub-agents are provided with the creator agent's internal monologue, conversational rationalizations, or design apologies.
* **Quarantine Enforcement:** Reviewer sub-agents receive ONLY:
  * The raw artifact under review (diff, document, code).
  * Objective domain constraints and specifications.
  * The dedicated attack focus prompt.
* **Result:** The reviewer evaluates the artifact strictly against reality, uncorrupted by author intent or cognitive anchoring.

---

## 4. References & Academic Bibliography

* **Li et al. (2023):** *Degeneration-of-Thought: How Large Language Models Fall into Repetitive and Narrow Cognitive Loops.* arXiv:2307.03987.
* **Sharma et al. (2023):** *Towards Understanding Sycophancy in Large Language Models.* arXiv:2310.13548.
* **Huang et al. (2023):** *Large Language Models Cannot Self-Correct Reasoning Yet.* ICLR 2024.
* **Du et al. (2023):** *Improving Factuality and Reasoning in Language Models through Multiagent Debate.* arXiv:2305.14325.
* **Popper, Karl (1959):** *The Logic of Scientific Discovery.* Routledge.
