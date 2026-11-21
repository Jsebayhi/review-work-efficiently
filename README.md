# Review Work Efficiently

> Dynamic Multi-Agent Adversarial Review Architecture & Best Practice Reference

[![Validate Skill Integrity](https://github.com/Jsebayhi/review-work-efficiently/actions/workflows/validate-skill.yml/badge.svg)](https://github.com/Jsebayhi/review-work-efficiently/actions/workflows/validate-skill.yml)

---

## 1. Executive Summary & Purpose

This repository provides an operational blueprint and skill definition for conducting **dynamic, situation-tailored adversarial reviews** across software, legal contracts, financial declarations, and strategic memos.

Rather than relying on a single generalist model to self-review its own output, this protocol establishes a structured framework to compose specialized sub-agents with strict **Proof-of-Failure (PoF)** contracts and context quarantine.

---

## 2. Theoretical Foundations & Academic Provenance

This architecture directly addresses three failure modes documented in AI safety and reasoning literature:

* **Degeneration-of-Thought (DoT):** Autoregressive models experience a collapse in cognitive entropy when reviewing their own output in the same context window, rationalizing their earlier mistakes ([Li et al., 2023](https://arxiv.org/abs/2307.03987)).
* **Machine Sycophancy:** Models trained via RLHF default to agreeable, polite padding rather than reporting severe runtime failures or structural bugs ([Sharma et al., 2023](https://arxiv.org/abs/2310.13548); [Perez et al., 2022](https://arxiv.org/abs/2212.09251)).
* **Single-Agent Self-Correction Limits:** Single-agent self-refine loops frequently swap one hallucination for another without genuine perspective diversity ([Huang et al., 2023](https://arxiv.org/abs/2308.03188)).

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

## 4. Going Further: Heterogeneous Tool-Augmented Verification (The TUMIX Paradigm)

The frontier of agentic evaluation moves beyond pure text-based debate into **heterogeneous, tool-augmented verification**.

Recent breakthroughs in multi-agent test-time scaling—notably the **TUMIX (Tool-Use Mixture)** framework ([Google Research, MIT, Harvard, 2025](https://arxiv.org/abs/2502.18685))—demonstrate that multi-agent ensembles achieve significantly higher task completion and verification accuracy when agents employ **diverse tool strategies and reasoning modalities** rather than homogeneous text analysis.

Applying the TUMIX paradigm to adversarial review transforms reviewers from passive readers into active falsifiers:

### A. Empirical Sandbox Verification (Code Execution)
* **Limitation of Text-Only Review:** A language model reading code can hallucinate that an algorithm has linear complexity or that an edge-case is handled.
* **Tool-Augmented Remedy:** Equipping reviewer agents with an isolated execution sandbox enables them to:
  * Synthesize and execute generative fuzz tests against the modified code.
  * Run mutation testing suites to verify if existing tests actually catch condition flips.
  * Empirically profile memory allocation and execution time under load.

### B. Formal Logic Verification (TLA+ & SMT Solvers)
* **Limitation of Text-Only Review:** Complex state machines, distributed locks, and retry/reconciliation protocols cannot be exhaustively verified by mental simulation.
* **Tool-Augmented Remedy:** Equipping an architectural reviewer agent with formal methods tools:
  * Automatically translating stateful transitions into formal TLA+ specifications.
  * Running model checkers (e.g. TLC or Z3 SMT solvers) to mathematically verify safety invariants (*"invalid state is never reached"*) and liveness (*"protocol never deadlocks"*).

### C. Adaptive Early Termination via LLM-as-Judge
Running multiple tool-augmented verification rounds can become computationally expensive. TUMIX addresses this by deploying an **LLM-as-Judge (Chief Justice)** monitoring cross-agent consensus:
* The review loop terminates early the moment a critical P0 exploit is concretely proven, or once high consensus is reached among diverse verification lenses.
* This preserves empirical verification rigor while slashing token consumption and inference overhead by up to 50%.

---

## 5. Multi-Domain Adversarial Catalogs

The core protocol is domain-agnostic. Dedicated attack vectors and Proof-of-Failure contracts are maintained in modular reference catalogs:

* **[Software Engineering & Architecture](skills/review-work-efficiently/references/domains/software-engineering.md):** 7 foci covering DevSecOps Exploitation, Test Verification & Mutation Blind Spots, Code Reliability, Package-by-Feature (DDD), DX, Business Invariants, and Public Release Sanitization.
* **[Commercial Contracts & Legal Agreements](skills/review-work-efficiently/references/domains/legal-and-contracts.md):** Liability traps, milestone ambiguity, clause contradictions, jurisdiction risks, and scope creep.
* **[Personal Finance, Taxes & Wealth Strategy](skills/review-work-efficiently/references/domains/finance-and-tax.md):** Statutory non-compliance, substantiation paper trails, formula precision, entity structuring leakage, and optimization intent.
* **[Argumentative Essays, Research & Strategy Memos](skills/review-work-efficiently/references/domains/writing-and-research.md):** Defamation/IP risk, citation verification, logical fallacies, narrative flow, and executive persuasiveness.

---

## 6. Repository Layout

```text
├── README.md
├── .gitignore
├── .github/
│   └── workflows/
│       └── validate-skill.yml
├── docs/
│   ├── 01-theoretical-foundations.md
│   └── 02-architecture-and-tradeoffs.md
└── skills/
    └── review-work-efficiently/
        ├── SKILL.md
        └── references/
            └── domains/
                ├── software-engineering.md
                ├── legal-and-contracts.md
                ├── finance-and-tax.md
                └── writing-and-research.md
```

---

## 7. Author & License

Authored and maintained by Jeremy Sebayhi.
Distributed under the MIT License.
