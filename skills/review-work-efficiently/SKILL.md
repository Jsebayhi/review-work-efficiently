---
name: review-work-efficiently
description: >-
  MANDATORY. Execute situation-tailored adversarial reviews on artifacts (code, architecture, legal contracts, tax declarations, or strategic memos). Dispatches quarantined, read-only specialist sub-agents with strict Proof-of-Failure contracts to eliminate sycophancy and Degeneration-of-Thought (DoT).
---

# Adversarial Reviewer Protocol

This runbook guides the primary agent through the 4-phase protocol for formulating, dispatching, and synthesizing situation-tailored adversarial sub-agents.

## Core Operational Invariants

1. **The Creator Does Not Review**: The agent that authored or modified the artifact MUST NOT perform the adversarial review. Self-review suffers from Degeneration-of-Thought (DoT) and confirmation bias.
2. **Context Quarantine**: Never pass conversational apologies, internal monologue, or author rationalizations to reviewer sub-agents. The reviewer must evaluate the raw artifact against objective domain specifications.
3. **The Proof-of-Failure (PoF) Mandate**: Reviewers must output concrete failure vectors or remain silent. Cosmetic compliments, formatting nits, and speculative worries without an exploit or failure path are forbidden.
4. **Read-Only Falsification**: Reviewer agents are strictly read-only. They are forbidden from mutating files or executing state-altering commands.

---

## The 4-Phase Review Process

### Step 1: Intake Artifact & Identify Domain

Inspect the artifact under review and classify it into its domain. Load the corresponding attack catalog from `references/domains/`:

- **Software Engineering & Architecture**: Load [software-engineering.md](references/domains/software-engineering.md).
- **Commercial Contracts & Legal Agreements**: Load [legal-and-contracts.md](references/domains/legal-and-contracts.md).
- **Personal Finance, Taxes & Wealth Strategy**: Load [finance-and-tax.md](references/domains/finance-and-tax.md).
- **Argumentative Essays, Research & Strategy Memos**: Load [writing-and-research.md](references/domains/writing-and-research.md).

### Step 2: Calibrate Scope & Select Adversarial Lenses

Evaluate the blast radius of the artifact to select the appropriate number of orthogonal lenses:

- **Targeted Audit (1–2 Lenses)**: For low-risk or narrow edits (e.g., Security + Test Verification for a minor bug fix).
- **Standard Review (2–3 Lenses)**: For standard feature releases or contract updates.
- **Comprehensive Crucible (4–7 Lenses in Parallel)**: Mandatory for high-stakes milestones, public open-source releases, cryptographic/auth changes, or major statutory filings.

*Principle:* Never summon all specialists for trivial edits; adjust the review depth to match the blast radius and token budget.

### Step 3: Quarantined Parallel Dispatch

Spawn the selected specialist sub-agents concurrently in isolated contexts using your harness's sub-agent primitives. For platform-specific invocation syntax, consult [harness-adapters](references/harness-adapters/).

Every sub-agent prompt must include:
1. **The Focus Attack Targets**: Injected from the domain reference file.
2. **The Quarantined Artifact**: The exact code diff, document text, or ledger.
3. **The Anti-Sycophancy Directive**:
   > *"You are evaluated on finding concrete, actionable failures and invariants breached. Zero compliments, zero cosmetic suggestions. If no defects are found, return NO_FAILURES_FOUND."*

### Step 4: Chief Justice Synthesis

When sub-agent reports return, do not output raw disjointed feedback. Act as the Chief Justice:

1. **Filter False Positives**: Discard cosmetic nits, styling preferences, or ungrounded theoretical concerns.
2. **De-Duplicate**: Merge overlapping findings flagged across multiple lenses.
3. **Resolve Tensions**: Pragmatically balance trade-offs (e.g. security friction vs user experience).
4. **Emit the Unified Adversarial Dossier**:
   - **P0 (Critical Blockers)**: Must be remediated immediately. Exploitable vulnerabilities, core business invariant breaches, uncapped liabilities, or statutory violations.
   - **P1 (Severe Flaws & Gaps)**: Critical missing edge-case verification, unhandled failure paths, ambiguous contractual clauses, or mathematical inconsistencies.
   - **P2 (Ergonomics & Hardening)**: Non-blocking operational friction or minor structural decoupling.
