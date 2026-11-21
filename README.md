# Review Work Efficiently

> Dynamic Multi-Agent Adversarial Review Architecture & Best Practice Reference

[![Validate Skill Integrity](https://github.com/Jsebayhi/review-work-efficiently/actions/workflows/validate-skill.yml/badge.svg)](https://github.com/Jsebayhi/review-work-efficiently/actions/workflows/validate-skill.yml)

---

## 1. Executive Summary & Purpose

This repository provides an operational blueprint and skill definition for conducting **dynamic, situation-tailored adversarial reviews** across software, legal contracts, financial declarations, and strategic memos.

Rather than relying on a single generalist model to self-review its own output, this protocol establishes a structured framework to compose specialized sub-agents with strict **Proof-of-Failure (PoF)** contracts and context quarantine.

---

## 2. Theoretical Foundations & Academic Provenance

This architecture is grounded in foundational research across cognitive science, multi-agent systems, and epistemology:

* **Why Single-Agent Review Fails:** Autoregressive models experience **Degeneration-of-Thought (DoT)** when reviewing their own output in the same context window ([Li et al., 2023](https://arxiv.org/abs/2307.03987)), display **Machine Sycophancy** from RLHF training priors ([Sharma et al., 2023](https://arxiv.org/abs/2310.13548); [Perez et al., 2022](https://arxiv.org/abs/2212.09251)), and fail to achieve genuine self-correction without external perspective diversity ([Huang et al., 2023](https://arxiv.org/abs/2308.03188)).
* **The Multi-Agent Debate Solution:** Deploying independent model instances to construct, critique, and debate candidate solutions over separate reasoning paths significantly outperforms single-agent generation and self-reflection ([Du et al., 2023](https://arxiv.org/abs/2305.14325); [Liang et al., 2023](https://arxiv.org/abs/2305.19118)). Differentiated reviewer personas prevent groupthink and achieve human-expert evaluation quality ([Chan et al., 2023](https://arxiv.org/abs/2308.07201)).
* **Agentic Falsification & Critical Rationalism:** Moving from confirmation bias (*"confirm this works"*) to active falsificationism as formalized in agentic literature ([Huang et al., Stanford 2025 - POPPER](https://arxiv.org/abs/2502.09858); [arXiv:2604.02485](https://arxiv.org/abs/2604.02485)), enforcing strict **Proof-of-Failure (PoF)** contracts and context quarantine.

👉 *For the complete epistemological and mathematical breakdown, see [docs/01-theoretical-foundations.md](docs/01-theoretical-foundations.md).*

---

## 3. The Core Trade-Off: Discretionary Prompting vs. Deterministic Workflows

While this skill demonstrates how an agent can dynamically compose and dispatch specialized reviewer sub-agents via prompt instructions, real-world deployment highlights a critical architectural trade-off:

### The Failure Modes of Discretionary In-Prompt Summoning
When multi-agent review is left entirely to the primary model's discretionary judgment:
* **Model Willingness Variance:** The model may arbitrarily decide not to summon sub-agents, or collapse multiple distinct perspectives into a single shallow pass.
* **Complexity Misclassification:** The model can easily misjudge task complexity or relevant domains (e.g. failing to summon a security exploiter when parsing untrusted input, or failing to summon an architecture auditor during domain model changes).
* **The ROI & Quota Trap:** Fanning out 7 parallel pro-tier agents to review a minor typo or one-line refactor produces negative return on investment, introduces severe latency, and rapidly exhausts API rate limits and token quotas. Summoning an entire army to conquer a small village is an anti-pattern: the level of verification must be proportional to the blast radius and risk of the task.

### The Reliable Evolution: Enforced Workflow Pipelines
A production-grade, highly reliable implementation moves beyond pure in-prompt prompting into a **deterministic workflow pipeline**:
* **Automated Task Complexity & Domain Assessment:** An initial evaluation step (or lightweight classifier) evaluates the diff's blast radius and architectural complexity.
* **Enforced Budget & Composition Gate:** A deterministic step calculates the required verification depth and decides:
  * How many agents are needed (e.g., 1 agent for low-risk changes, 2-3 for standard features, full ensemble for critical surfaces).
  * Which combined points of view (POVs) are required to verify the task.
  * How to enforce strict compliance with the allocated token budget.
* **Programmatic Parallel Execution:** Specialist agents run concurrently with validated JSON output schemas, guaranteeing that only concrete proofs of failure reach the synthesis step.

👉 *For architectural patterns and budget tiering matrices, see [docs/02-architecture-and-tradeoffs.md](docs/02-architecture-and-tradeoffs.md).*

---

## 4. Going Further: Augmenting Reviewers with Heterogeneous Tools (The TUMIX Paradigm)

While multi-agent debate establishes cognitive diversity in reasoning, the next capability frontier compounds this by equipping reviewer agents with **heterogeneous verification tools**.

Recent breakthroughs in multi-agent test-time scaling—notably the **TUMIX (Tool-Use Mixture)** framework ([Google Research, Google DeepMind, MIT, Harvard, 2025](https://arxiv.org/abs/2502.18685))—demonstrate that multi-agent teams achieve significantly higher task completion and verification accuracy when agents employ **diverse tool strategies and reasoning modalities** rather than relying on a single uniform approach.

Applying the TUMIX paradigm extends adversarial reviewers from analytical critics into active falsifiers:

### A. Empirical Sandbox Verification (Code Execution)
* **The Opportunity:** Moving from static code reading to empirical execution.
* **Tool-Augmented Verification:** Equipping reviewer agents with an isolated execution sandbox enables them to:
  * Synthesize and execute generative fuzz tests against the modified code.
  * Run mutation testing suites to verify if existing tests actually catch condition flips.
  * Empirically profile memory allocation and execution time under load.

### B. Formal Logic Verification (TLA+ & SMT Solvers)
* **The Opportunity:** Extending inspection of state machines, distributed locks, and retry/reconciliation protocols into mathematical proof.
* **Tool-Augmented Verification:** Equipping an architectural reviewer agent with formal methods tools:
  * Automatically translating stateful transitions into formal TLA+ specifications and verifying invariants via model checkers and agentic proof solvers ([arXiv:2606.05792](https://arxiv.org/abs/2606.05792); [arXiv:2610.14923](https://arxiv.org/abs/2610.14923)).
  * Running model checkers (e.g. TLC or Z3 SMT solvers) to mathematically verify safety invariants (*"invalid state is never reached"*) and liveness (*"protocol never deadlocks"*).

### C. Adaptive Early Termination via LLM-as-Judge
Running multiple tool-augmented verification rounds can become computationally expensive. As demonstrated in TUMIX, deploying an **LLM-as-Judge (Chief Justice)** monitoring cross-agent consensus allows the review loop to terminate early as soon as an indisputable bug is proven or consensus is reached, slashing token consumption and latency by up to 50%.

---

## 5. Multi-Domain Adversarial Catalogs

The core protocol is domain-agnostic. Dedicated attack vectors and Proof-of-Failure contracts are maintained in modular reference catalogs:

* **[Software Engineering & Architecture](skills/review-work-efficiently/references/domains/software-engineering.md):** 7 foci covering DevSecOps Exploitation, Test Verification & Mutation Blind Spots, Code Reliability, Package-by-Feature (DDD), DX, Business Invariants, and Public Release Sanitization.
* **[Commercial Contracts & Legal Agreements](skills/review-work-efficiently/references/domains/legal-and-contracts.md):** Liability traps, milestone ambiguity, clause contradictions, jurisdiction risks, and scope creep.
* **[Personal Finance, Taxes & Wealth Strategy](skills/review-work-efficiently/references/domains/finance-and-tax.md):** Statutory non-compliance, substantiation paper trails, formula precision, entity structuring leakage, and optimization intent.
* **[Argumentative Essays, Research & Strategy Memos](skills/review-work-efficiently/references/domains/writing-and-research.md):** Defamation/IP risk, citation verification, logical fallacies, narrative flow, and executive persuasiveness.

---

## 6. Author & License

Authored and maintained by Jeremy Sebayhi.
Distributed under the MIT License.
