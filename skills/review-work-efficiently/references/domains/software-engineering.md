# Domain Reference: Software Engineering & Architecture

When auditing code, software architectures, or technical pull requests, select from these 7 specialized adversarial lenses:

## Focus 1: Security (DevSecOps Exploiter)
* **Mission:** Uncover actionable vulnerabilities, data exfiltration paths, and authorization bypasses.
* **Attack Targets:**
  * Injection & parsing: SQL, command injection, SSRF, XSS, ReDoS, path traversal.
  * Secrets & tokens: Exposed API keys, tokens in code or logs.
  * Auth & permissions: Missing authorization, IDOR, privilege escalation, session fixation.
  * Data exposure: Unsanitized stack traces in error responses, leaked PII.
* **Proof-of-Failure Contract:** Must provide an exact exploit payload or attack sequence demonstrating the breach.

## Focus 2: Test Verification (The Test Auditor)
* **Mission:** Audit test suite integrity, verification paradigms, and mutant survival.
* **Attack Targets:**
  * Mocking internal code: Rejects mocking domain entities, internal services, or parsers. Mocks are restricted strictly to external system boundaries (third-party APIs, clock).
  * Surviving mutants: Condition flips (< to <=, == to !=) or omitted checks that pass tests undetected.
  * Testing trophy inversion: 100 mock-heavy unit tests with zero integrated component coverage.
  * Tautological assertions: Tests that assert mock calls without verifying real state transitions.
  * Missing boundary/failure tests: Null, empty, maximum size, network timeout, 500 error responses.
* **Proof-of-Failure Contract:** Must specify a concrete Given/When/Then test scenario or mutant that exposes the blind spot.

## Focus 3: Code & Craft Quality (Defect Specialist)
* **Mission:** Detect latent runtime bugs, unhandled exceptions, and fragile implementation logic.
* **Attack Targets:**
  * Unhandled exceptions, uncaught promises, swallowed errors.
  * Resource and memory leaks: Unclosed file descriptors, unreleased locks, dangling connections.
  * State corruption & off-by-one errors: Slicing bounds, loop boundaries, unintended type coercions.
  * Lifecycle glitches: Uninitialized variables, race conditions during teardown.
* **Proof-of-Failure Contract:** Must provide a line-by-line runtime failure trace showing how input X causes failure Y.

## Focus 4: Architecture (DDD & Vertical Slicing)
* **Mission:** Enforce Package-by-Feature (vertical slicing) and prevent technical layer coupling.
* **Attack Targets:**
  * Technical layer grouping: Root packages named models/, domain/, types/, entities/, services/ bundling unrelated domains.
  * Cross-domain technical hoarding: Grouping all parsers or helpers into generic packages.
  * Unverified state machines: Multi-step lifecycles with unmodeled transitions that reach illegal states.
  * Concurrency traps: Deadlocks, shared mutable state without synchronization.
* **Proof-of-Failure Contract:** Must identify the specific cross-domain entanglement or provide a statechart counterexample showing the invalid state transition.

## Focus 5: User Friendliness (DX / UX)
* **Mission:** Eliminate user friction, confusing APIs, and cognitive overload.
* **Attack Targets:**
  * Cryptic error diagnostics: Generic errors without actionable remediation guidance.
  * Unintuitive API contracts: Clunky function signatures, surprising defaults.
  * Silent failures: Dropped data or failed operations without warnings.
* **Proof-of-Failure Contract:** Must cite the exact user action that results in confusion, data loss, or stranded state.

## Focus 6: Business & Domain Correctness
* **Mission:** Ensure implementation satisfies business rules and domain invariants.
* **Attack Targets:**
  * Invariant breaches: Balances not netting to zero, inventory decremented without payment.
  * Spec divergence: Divergence from requirements or acceptance criteria.
  * Corner-case business states: Cancellations mid-settlement, duplicated refunds.
* **Proof-of-Failure Contract:** Must demonstrate the sequence of business events producing an invalid domain state.

## Focus 7: Public Release & Repository Sanitizer
* **Mission:** Cleanse repositories before external or public release.
* **Attack Targets:**
  * Credentials in git history (including commits where keys were added and later removed).
  * Internal infrastructure IPs, corporate domains (*.internal), and local absolute paths.
  * Missing LICENSE file, viral dependency licensing conflicts.
  * Broken README instructions or dead public links.
* **Proof-of-Failure Contract:** Must cite the exact commit hash, line number, or unreachable URL.
