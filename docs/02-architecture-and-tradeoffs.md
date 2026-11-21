# Architectural Design & Economic Trade-Offs

This document explores the operational mechanics, economic constraints, and evolutionary path of multi-agent adversarial evaluation.

---

## 1. In-Prompt Summoning vs. Deterministic Workflow Pipelines

When building agentic evaluation, teams face a choice between **in-prompt discretionary summoning** and **deterministic workflow pipelines**:

### Pattern A: In-Prompt Discretionary Summoning (The Skill Approach)
* **How it works:** The primary agent reads a skill and autonomously decides whether, when, and how many sub-agents to dispatch using its native tooling (`invoke_subagent`, sub-process calls, or API forks).
* **Strength:** Highly dynamic and adaptable. Requires zero workflow engine infrastructure. Can be embedded into any chat assistant or CLI harness.
* **Critical Vulnerabilities:**
  * **Model Willingness Variance:** The model may arbitrarily decide not to summon specialists, collapsing into a single-turn self-review.
  * **Domain Misclassification:** The model may fail to recognize that a change impacts security, database locking, or legal liability, omitting critical lenses.
  * **Fragile Formatting:** Output depends on prompt compliance; agents may emit conversational text instead of structured machine-readable findings.

### Pattern B: Deterministic Workflow Pipelines (The Production Engine)
* **How it works:** Orchestration code (Python, LangGraph, Antigravity Workflows) controls the execution graph.
* **Strength:** 100% deterministic execution, strict JSON schema validation, parallel background processing, and hard budget gates.
* **Architecture:**
  * **Phase 1: Complexity Assessment Gate:** An evaluation model or static analysis pass measures diff size, cyclomatic complexity, and file boundaries.
  * **Phase 2: Budget & Composition Gate:** Calculates required agents based on a strict token/cost budget.
  * **Phase 3: Parallel Execution:** Dispatches selected foci concurrently in isolated processes.
  * **Phase 4: Synthesis:** An aggregator deduplicates findings and emits an actionable dossier.

---

## 2. The Quota and ROI Principle

> *"You don't want to summon your entire army to conquer a small village: the ROI is bad and you rapidly reach your rate limits and token quotas."*

A common pitfall in multi-agent system design is **indiscriminate fan-out**. Running 7 parallel reasoning models (e.g. `pro` tier) on a 3-line README edit or CSS tweak causes:
* Excessive token burn with zero risk reduction.
* Premature rate limit and API quota exhaustion.
* Developer latency fatigue (waiting minutes for an audit of a trivial change).

### The Dynamic Tiering Model

To optimize ROI, evaluation must dynamically tier according to artifact blast radius:

* **Tier 0: Low Risk (1 Sanity Agent, Light Tier)**
  * Trigger: Typo fixes, internal documentation, non-functional cosmetic updates.
  * Lenses: Basic reliability or syntax sanity check.
* **Tier 1: Medium Risk (2–3 Targeted Specialists, Inherited Tier)**
  * Trigger: Feature changes, internal logic refactors, CLI tool updates.
  * Lenses: Test Verification Auditor + Code Reliability Specialist.
* **Tier 2: High Blast Radius / Public Surface (Full Ensemble: 6–7 Specialists in Parallel, Pro Tier)**
  * Trigger: Cryptographic logic, authentication/authorization middleware, public open-source releases, statutory tax/legal filings, database migrations.
  * Lenses: Full parallel ensemble covering Security, Testing, Reliability, Architecture, DX, Business Correctness, and Public Release.

---

## 3. The Chief Justice Synthesis Pattern

When multiple specialist agents audit an artifact, they generate domain-specific findings that can conflict:
* Security may demand paranoid input validation that degrades User Experience (DX).
* Architecture may demand strict modular decoupling that increases short-term code complexity.

The **Chief Justice** synthesis stage resolves these tensions:
* **Filter False Positives:** Discards theoretical nitpicks lacking concrete failure vectors.
* **Deduplicate:** Merges findings flagged by multiple lenses.
* **Enforce Invariant:** An artifact is marked `PASSED` if and only if blocking P0 and P1 defects are zero.
